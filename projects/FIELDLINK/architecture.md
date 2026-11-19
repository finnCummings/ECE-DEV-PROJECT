# FIELDLINK — System Architecture (D03)

**Status:** Draft — pending review of [proposed requirements v0.3](requirements.md)  
**Date:** 2026-11-19  
**Current capability:** Planning only; TST-001 is drafted, not executed

## Mission and design rationale

FIELDLINK is a **modular communications, integration, diagnostics, and test platform** for independent embedded projects. It should connect supported interfaces, normalize measurements without hiding their source meaning, observe communication/device health, and produce repeatable test evidence. It is a personal engineering learning system and public portfolio: implementation choices and test results matter as much as final operation.

This does **not** aim to outperform or replace existing standards by default. Use or adapt established protocols when justified. Initial custom UART/LoRa work is deliberately educational and establishes measured behavior before adding abstraction.

## Logical architecture

```text
       PC serial monitor (GUI deferred)
                 |
           USB / UART
                 |
    Ground FIELDLINK transceiver
                 |
           LoRa link (planned)
                 |
    Remote FIELDLINK transceiver / gateway
                 |
  Device-specific UART or other interface
                 |
   Project MCU, sensor, or motor controller
                 |
       Source-specific data
                 v
    [Protocol adapter / decoder]
                 |
   [Normalized record + raw evidence]
                 |
       [Diagnostic services]
       - transport/link faults
       - device health
       - configured application rules
                 |
        [Test records and logs]
```

**Placement note:** A decoder or diagnostic module may execute on the remote node, the ground station, or a computer. The diagram is a logical pipeline, not a finalized physical wiring schematic. Do not confuse a LoRa transport adapter with a Modbus/MAVLink protocol decoder.

## Module contracts

| Module | Input | Output | Responsibility |
| --- | --- | --- | --- |
| Transport | UART/LoRa or another supported interface | Byte stream or framed transport packet | Move bytes; expose link errors/settings where supported |
| Framer/parser | Bytes and interface configuration | Bounded validated message or error | Delimit and validate packets; identify version/type |
| Protocol adapter | Known versioned device-specific messages | Typed normalized record(s) + original evidence reference | Decode meaning/units; reject unsupported definitions |
| Normalized record model | Recognized decoded values | Device ID, type, unit/scale, value, source, timestamps, freshness/quality | Make diagnostic processing protocol-independent |
| Diagnostics | Normalized records and supported link metadata | Fault events with timestamps and evidence | Report observed faults and qualified hypotheses |
| Test and evidence | Hardware/software configuration and observations | Reproducible reports, logs, raw data | Show what was verified, failed, or remains unknown |
| UI (future) | Normalized events and diagnostic data | Operator-facing display / controls | Consume service APIs without changing core logic |

## Diagnostic boundaries

**Level 1: Communications health:** sequence gaps when the source provides sequence information; integrity errors only when observable by the receiver; ACKs/timeouts; link recovery. Some radios drop invalid RF frames internally, so the application may only observe gaps or timeouts.

**Level 2: Device health:** device-reported reset reason, voltage, sensor state, uptime, error counters, as supported.

**Level 3: Application health:** cross-measurement checks using device-specific thresholds and time alignment, e.g. motor commanded to run while speed remains near zero and current is elevated. Such a pattern is a *possible stall*, not proof of a specific mechanical fault.

A device whose entire power supply disappears cannot necessarily send a fault report. Report missing telemetry and last known state instead of inventing a cause.

## Native protocol integration

- **Initial custom serial parser:** small C/C++ PING/PONG and later defined messages; no Python or graphical UI required.
- **LoRa:** bidirectional transport proof using suitable radios, with verified electrical and RF settings.
- **Modbus (future):** adapter uses a documented device register map and function responses; raw registers have no universal meaning without the map. RTU and TCP transports differ.
- **MAVLink (future):** adapter uses an existing compatible message-definition decoder to map selected known messages; preserve system/component/message identity and timestamps where available.
- **Unknown formats:** no speculative conversion; record unsupported protocol/schema and retain safe raw evidence as appropriate.

## Record and packet strategy

A **native transport packet** is distinct from a **normalized diagnostic record**. Do not force Modbus or MAVLink through an additional nested serialization layer without evaluating overhead and compatibility.

Proposed internal record fields: `source_device_id`, `protocol`, `schema_version`, `metric_id`, `value_type`, `value`, `unit_or_scale`, `source_timestamp` (if available), `receive_timestamp`, `quality`, `raw_evidence_ref`. These are conceptual, **not approved wire bytes**.

Use bounded payloads, explicit schema versioning, defined endianness/scaling, CRC/checksum where appropriate, and distinguish measurement age from transmission age.

## Development and educational milestones

| Stage | Target | Learning/evidence |
| --- | --- | --- |
| TST-001 | Wired UART PING/PONG | Embedded C/C++, parser behavior, configuration, repeatable test report |
| TST-002 (planned) | Bidirectional LoRa PING/PONG | RF setup, transport isolation, end-to-end verification |
| Later | Integrity, sequence numbers, timeouts, retries | Fault injection, diagnostic counts, limits and recovery |
| Later | Sensor telemetry into normalized records | Typed values, units/scaling, logs and traceability |
| Later | Second adapter on same diagnostic core | Modularity/regression verification |
| Later | Modbus integration | Industrial registers and protocol interoperability |
| Later | MAVLink integration | Structured message decoding and aerospace-oriented integration |
| Deferred | Graphical UI and custom hardware | User experience, PCB implementation once justified |

Work should progress through **define → design → build → test → analyze → improve**. Firmware and interface decisions should be supported by datasheets, commits, diagrams, test plans, raw evidence, and concise portfolio case studies. No placeholder or planned test counts as verification.

## Design decisions pending

- Exact two-radio topology and any required microcontroller/gateway at each end
- EBYTE module compatibility, serial pin voltage, supplies, antenna, and regional frequency compliance
- Wire framing and error detection for custom messages
- Normalized-record schema and source-specific adapter API
- Measurement timestamp source, freshness windows, and clock synchronization
- Diagnostic severity levels and evidence retention
- Criteria for selecting Modbus/MAVLink adapter demonstrations

## Document links

- [Requirements v0.3 proposed](requirements.md)
- [TST-001 UART test plan](systems/communications/tests/TST-001_uart/test_plan.md)
- [Ground station UI — deferred](ground_station/ui/README.md)
- [Repository engineering guide](../../ENGINEERING_GUIDE.md)
