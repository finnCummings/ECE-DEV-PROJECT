# FIELDLINK — System Requirements

**Project:** FIELDLINK  
**Status:** Proposed Revision — Pending Review  
**Revision:** 0.3 (proposed; v0.2 approved previously)  
**Date:** 2026-10-30  
**Scope:** Communications, protocol adapters, normalized diagnostic model, and test infrastructure; graphical UI deferred

## 1. System Objective

Design, build, and verify a modular **communications, device-integration, and diagnostic test platform**. FIELDLINK shall exchange messages with independent embedded systems, initially over wired UART and bidirectional LoRa, and later interpret supported external protocols through adapters. The purpose is to support fault isolation, meaningful device-health monitoring, repeatable testing, and traceable portfolio evidence.

FIELDLINK is the **complete integration platform**, comprising ground/remote communications components, transport interfaces, protocol adapters, a normalized data model, and diagnostic/test services. A graphical UI remains a deferred FIELDLINK subsystem. External projects such as a miniature TBM and high-altitude-balloon payload remain independent.

## 2. Scope and System Boundaries

**Within FIELDLINK**
- A documented common interface for commands, telemetry, and diagnostics.
- Pluggable, explicitly supported protocol adapters, initially a custom UART parser; MAVLink and Modbus are future integration targets.
- Normalized records retaining source identity, units/scales, timestamps, validity and freshness, while preserving raw or source-specific diagnostic evidence.
- Diagnostic/test services for link health, device-reported faults, and supported application-specific conditions.
- Ground-station graphical UI (later phase, not a prerequisite).
- Ground-side transceiver and host serial connection.
- Reusable message format, validation, exchange and failure-handling behavior.
- Remote transceiver and documented interface to the external project.
- Verification of individual interfaces and end-to-end behavior.

**Outside FIELDLINK**
- The miniature TBM's motor controllers, navigation algorithms, sensors, and application-specific control logic.
- Any other project's internal implementation and safety controller.
- Multi-remote-node operation, until requirements and feasibility are reviewed separately.
- Automatic understanding of unknown or undocumented device data without a protocol definition.
- Claiming that FIELDLINK outperforms existing industry-standard platforms without equivalent measurement evidence.

## 3. Functional Requirements

IDs follow the [Engineering Guide](../../ENGINEERING_GUIDE.md). Each row represents a distinct planned capability. Thresholds marked **TBD** require agreement before being used as pass/fail criteria.

| ID | Requirement | Planned verification |
| --- | --- | --- |
| SYS-001 | The FIELDLINK system shall support bidirectional command and telemetry exchange between the ground station and a remote node over a LoRa link. | End-to-end integration test (TST-002 planned) |
| SYS-002 | FIELDLINK shall expose a documented, reusable interface by which different remote project applications can exchange commands and telemetry without modifying the core communications protocol. | Integration demonstration with two application configurations (test TBD) |
| GND-001 | The ground-station UI shall allow an operator to select and connect to a supported serial communications endpoint. | UI functional test (TBD) |
| GND-002 | The ground-station UI shall send defined operator commands and display their responses or error states. | Command/response UI test (TBD) |
| GND-003 | The ground-station UI shall display received telemetry and available connection-status or diagnostic information. | Simulated and live telemetry test (TBD) |
| GND-004 | The ground-station UI shall record received telemetry with timestamps to an exportable file. | File-output inspection and functional test (TBD) |
| COM-001 | The communications subsystem shall receive and interpret defined UART messages. | Wired UART test (TST-001 planned) |
| COM-002 | The communications subsystem shall transmit defined UART response messages. | Wired UART test (TST-001 planned) |
| COM-003 | The communications protocol shall detect corrupted messages according to a specified integrity check. | Fault injection (TBD) |
| COM-004 | The system shall detect communication loss after a defined timeout and report it to the relevant interface. | Timeout/fault simulation (TBD) |
| RMT-001 | The remote transceiver shall receive valid FIELDLINK commands and make the decoded command available through a documented project interface. | Remote interface integration test (TBD) |
| RMT-002 | The remote transceiver shall accept project-supplied telemetry through the documented interface and transmit it toward the ground station. | Remote telemetry integration test (TBD) |

### Proposed v0.3 requirements — pending approval

These are **additional proposed requirements**, not yet part of the approved v0.2 baseline:

| ID | Requirement | Planned verification |
| --- | --- | --- |
| SYS-003 | FIELDLINK shall normalize measurements from at least two distinct supported device interfaces into a common representation retaining device identity, field meaning, scaling, timestamp, and validity. | Two-adapter integration test (planned) |
| SYS-004 | FIELDLINK shall permit addition of a supported device protocol adapter without changing the core diagnostic processing logic. | Adapter swap/code inspection and regression test (planned) |
| DIA-001 | FIELDLINK shall record communication failures including invalid packets, sequence gaps when supported by the protocol, and communication timeouts, distinguishing observed symptoms from inferred causes. | Controlled fault injection (planned) |
| DIA-002 | FIELDLINK shall evaluate documented device-health or application-specific conditions against configured diagnostic rules, and preserve the supporting observations. | Fault simulation and evidence review (planned) |
| ADP-001 | Each supported adapter shall identify its source protocol/schema version and reject or explicitly label unsupported message definitions. | Compatibility/negative test (planned) |

**Note:** Prefixes `GND` and `RMT` identify the ground-station and remote-node subsystems, respectively. They are local project conventions, not external standards.

## 4. Interfaces and Dependencies

| Interface | Connected components | Technology / format | Decisions pending |
| --- | --- | --- | --- |
| Protocol adapter to normalization | Supported input protocol ↔ common records | Versioned adapter contract (TBD) | Field maps, units, validation, raw evidence |
| Normalization to diagnostics | Common records ↔ diagnostic engine | Typed events/measurements (TBD) | Fault codes, freshness, clock provenance |
| UI to host communications service | Desktop UI ↔ serial/packet-handling software | Internal application interface (deferred) | Command API, status/error model |
| Host to ground transceiver | PC ↔ USB/UART interface | Serial | Port selection, baud rate, message framing |
| Wireless link | Ground ↔ remote LoRa transceiver | LoRa radio | Module settings, rate, channel/frequency, link behavior |
| Remote to external project | Remote node ↔ target MCU/application | Documented interface (TBD) | Electrical levels, connectors, command/telemetry schema |
| Logging | UI ↔ file system | Timestamped CSV for tabular telemetry (proposed) | Timestamp source, units, metadata, filenames |

Equipment available for evaluation includes the Arduino Uno R4 WiFi, EBYTE E32-900T20D UART radio modules, CP2102 serial adapter, and Python on the computer. These are **candidates**, not a finalized bill of materials. Verify electrical compatibility and operating requirements against datasheets before wiring.

## 5. Nonfunctional Requirements and Constraints

- Separate transport, protocol decoding, normalized data, diagnostic logic, and application behavior; defer GUI implementation.
- Prefer existing protocol parsers for MAVLink or Modbus when those integrations are implemented; avoid wrapping full protocols without a demonstrated need.
- Treat unsupported schemas as unknown, rather than guessing field meanings or inventing diagnoses.
- Provide clear diagnostics suitable for isolating failures at the serial, RF, and application boundaries.
- Define a message timeout and report stale/disconnected status; precise timeout **TBD**.
- Ensure remote equipment independently enforces safety-critical behavior if commands stop arriving; the UI alone is not a safety interlock.
- Define measurable packet-delivery, latency, and data-integrity criteria before corresponding tests; thresholds **TBD**.
- Begin with a wired UART verification before adding wireless integration.
- Keep firmware and software revisions, hardware configuration, and test evidence traceable.

## 6. Requirement Hierarchy

`SYS-001` is an **end-to-end** requirement. UART tests against `COM-001` and `COM-002` provide supporting evidence but cannot by themselves prove wireless operation. `GND` and `RMT` requirements contribute to the end-to-end system as distinct subsystems.

The FIELDLINK ground-station UI is **not a separate project**. Its UI is a deferred subsystem; UI-specific design documentation will be added when UI work becomes active, while this file remains the master requirements document.

## 7. Preliminary Verification Traceability

| Requirement | Test | Status | Evidence |
| --- | --- | --- | --- |
| COM-001 | TST-001 — UART command reception | Not tested | — |
| COM-002 | TST-001 — UART response transmission | Not tested | — |
| SYS-001 | TST-002 — LoRa end-to-end exchange (planned) | Not tested | — |
| GND-001–GND-004 | UI tests (IDs TBD) | Not tested | — |
| RMT-001–RMT-002 | Remote-node integration tests (IDs TBD) | Not tested | — |
| SYS-002, COM-003, COM-004 | Tests TBD | Not tested | — |
| SYS-003, SYS-004, DIA-001, DIA-002, ADP-001 | Adapter/diagnostics verification TBD; proposed v0.3 | Not tested | — |

The test ID `TST-001` is distinct from requirements such as `COM-001`.

## 8. Planned Development Sequence

1. Review and approve system requirements and subsystem boundaries.
2. Define architecture, protocol boundaries, and interface contracts.
3. Implement basic wired UART PING/PONG using a simple ground-station console.
4. Integrate the LoRa radios and remote transceiver for bidirectional communication.
5. Normalize telemetry from at least two supported data sources and develop testable diagnostic rules.
6. Add an established-protocol adapter (Modbus first, MAVLink later) when justified, verifying raw and normalized data.
7. Verify failure handling, test reporting, and reuse with independent projects.
8. Develop the ground-station graphical UI only after the foundations work.

This is a proposed sequence, not a record of completed implementation. UI and firmware modules may be developed in parallel once their interface is agreed.

## 9. Open Engineering Decisions

- [ ] Normalized-record schema, timestamp origin and freshness rules
- [ ] Adapter ABI/API, supported versions, and error reporting
- [ ] Initial communication fault classification and device diagnostic rules
- [ ] Modbus/MAVLink adapter value relative to implementation complexity
- [ ] Ground station UI framework and supported operating systems (deferred)
- [ ] UART port, framing, baud rate, and voltage/interface assumptions
- [ ] RF configuration and operational/environmental constraints
- [ ] Protocol version, addressing, data integrity, retries, and acknowledgment format
- [ ] Remote project interface and power arrangement
- [ ] Meaningful latency, packet-delivery, and communication-loss thresholds
- [ ] Telemetry schema, timestamps, and logging format
- [ ] Which requirements can be demonstrated with simulation before hardware integration

## 10. Change Notes

| Date | Revision | Change | Reason |
| --- | --- | --- | --- |
| 2026-10-30 | 0.1 | Initial FIELDLINK requirements draft | Establish starting system capabilities |
| 2026-10-30 | 0.2 | Consolidate UI, ground transceiver, and remote node under FIELDLINK | Align one system baseline with subsystem boundaries |
| 2026-11-19 | 0.3 proposed | Shift long-term objective to integration, normalized diagnostics, and test evidence | Preserve foundational UART/LoRa learning while leveraging existing standards |

**Review gate:** The owner approved the earlier v0.2 scope in conversation, but the former file was still labeled draft. **The additions in v0.3 are proposed and require explicit review** before treating them as the new technical baseline. Existing TST-001 UART work remains a valid foundational learning experiment; nothing in this proposal represents implemented or verified capabilities.
