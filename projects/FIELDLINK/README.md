# FIELDLINK — Modular Communications and Diagnostics Platform

**Status:** Planning  
**Project type:** Reusable embedded communications, interoperability, diagnostics, and test platform

## Mission

Design, build, and verify a **modular communications and diagnostic test platform** that connects independent embedded systems, translates supported protocol data through adapters, normalizes telemetry, diagnoses faults, and preserves test evidence. **UART and bidirectional LoRa are the first learning and verification stages**, not the entire long-term purpose.

FIELDLINK is designed to be **project agnostic**: a TBM, sensor payload, or future engineering system can expose information through a documented adapter without rewriting the central diagnostic logic. MAVLink and Modbus are candidate *future protocol adapters*, not standards we intend to replace.

## Engineering objectives

1. Implement a basic command/response exchange over wired UART.
2. Develop a clear message framing and command/telemetry interface.
3. Integrate bidirectional communication using LoRa UART radio modules.
4. Add message validation, error handling, communication timeout behavior, and test evidence.
5. Demonstrate sensor telemetry, then normalize typed measurements with identity, units, timing, and validity metadata.
6. Build diagnostics for link faults, device-reported health, and rule-based application symptoms; verify them through fault injection.
7. Demonstrate reuse by adding a second protocol/device adapter without changing the core diagnostic engine.
8. Evaluate Modbus and MAVLink adapters after the baseline is verified. Consider multiple remote nodes and a graphical UI only when they serve a justified need.

## Key design principles

- **Project agnostic:** Payload or motor-control logic stays in the application, not the communications layer.
- **Protocol interoperability:** Decoding adapters translate known formats; the shared diagnostic model is independent of any specific protocol.
- **Evidence first:** Preserve native message context and raw test records; never claim to know the cause of a fault from insufficient evidence.
- **Modular:** Hardware, protocol, ground-station software, and project application can evolve separately.
- **Reliable and testable:** Specify measurable behavior and keep raw test evidence.
- **Maintainable:** Clear wiring, straightforward debugging, and replaceable components.
- **Safe failures:** Remote control integrations must account for stale or lost commands.

## Operator interface

FIELDLINK encompasses ground and remote transport, protocol adapters, normalized records, and diagnostic/test services. A graphical operator UI is a **deferred subsystem**, not required to begin embedded development. External applications remain independent projects.

The [requirements](requirements.md) contain proposed **v0.3 additions** for interoperability and diagnostics, pending owner review. The earlier v0.2 scope was approved in conversation; new technical requirements are not yet baselined. See [architecture.md](architecture.md) for the conceptual integration design.

## Initial development hardware

Candidate hardware from previous experiments: Arduino Uno R4 WiFi, EBYTE E32-900T20D UART LoRa modules, and CP2102 USB-to-UART adapter. Initial ground-side operation uses a PC serial monitor; a Python interface is optional and deferred. Exact voltage levels, pin assignments, operating modes, and configuration will be confirmed against the relevant datasheets before wiring.

## Current development priority

**Approved focus (2026-10-30):** Establish wired UART and bidirectional LoRa communications first. The graphical user interface remains in scope, but implementation is **deferred** until the communications baseline is functioning and tested. Use a serial monitor for early command-response experiments; no Python GUI is required.

## First milestone: D03 — Architecture and requirements review

Document the logical ground-station-to-node architecture, module interfaces, initial requirements, and a **TST-001 wired UART PING/PONG test plan**.

**No FIELDLINK hardware or firmware testing is claimed by this document.**

## Roadmap

| Phase | Scope | Status |
| --- | --- | --- |
| 1 | Wired UART PING/PONG; test plan, firmware and evidence | Next implementation milestone |
| 2 | Two-way LoRa PING/PONG over ground/remote transceivers | Planned |
| 3 | Message integrity, ACKs, timeouts, reliability diagnostics and fault injection | Planned |
| 4 | Sensor telemetry, normalization, timestamps/units, and logging | Planned |
| 5 | Second project-specific adapter and common diagnostic engine | Planned |
| 6 | Modbus integration, then MAVLink, using established decoders | Future |
| 7 | Graphical UI, custom PCBs, and optional multi-node support where justified | Deferred |

Follow the [Engineering Guide](../../ENGINEERING_GUIDE.md) and use the [documentation templates](../../templates/) for records.
