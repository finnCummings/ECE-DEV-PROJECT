# FIELDLINK — System Requirements

**Project:** FIELDLINK  
**Status:** Draft — Pending Review  
**Revision:** 0.2  
**Date:** 2026-10-30  
**Scope:** Ground station UI, ground transceiver, shared protocol, and remote transceiver

## 1. System Objective

Design, build, and verify a reusable, bidirectional LoRa communications system for exchanging operator commands, telemetry, and diagnostic information between a ground station and remote engineering projects.

FIELDLINK is the **complete system**: its computer-based user interface, ground-side communications device, wireless link, and remote transceiver. External applications (e.g., a miniature TBM or sensor payload) remain independent projects that integrate through a documented interface.

## 2. Scope and System Boundaries

**Within FIELDLINK**
- Ground-station UI for commands, telemetry viewing, connection status, and diagnostics.
- Ground-side transceiver and host serial connection.
- Reusable message format, validation, exchange and failure-handling behavior.
- Remote transceiver and documented interface to the external project.
- Verification of individual interfaces and end-to-end behavior.

**Outside FIELDLINK**
- The miniature TBM's motor controllers, navigation algorithms, sensors, and application-specific control logic.
- Any other project's internal implementation and safety controller.
- Multi-remote-node operation, until requirements and feasibility are reviewed separately.

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

**Note:** Prefixes `GND` and `RMT` identify the ground-station and remote-node subsystems, respectively. They are local project conventions, not external standards.

## 4. Interfaces and Dependencies

| Interface | Connected components | Technology / format | Decisions pending |
| --- | --- | --- | --- |
| UI to host communications service | Desktop UI ↔ serial/packet-handling software | Internal application interface (TBD) | Command API, status/error model |
| Host to ground transceiver | PC ↔ USB/UART interface | Serial | Port selection, baud rate, message framing |
| Wireless link | Ground ↔ remote LoRa transceiver | LoRa radio | Module settings, rate, channel/frequency, link behavior |
| Remote to external project | Remote node ↔ target MCU/application | Documented interface (TBD) | Electrical levels, connectors, command/telemetry schema |
| Logging | UI ↔ file system | Timestamped CSV for tabular telemetry (proposed) | Timestamp source, units, metadata, filenames |

Equipment available for evaluation includes the Arduino Uno R4 WiFi, EBYTE E32-900T20D UART radio modules, CP2102 serial adapter, and Python on the computer. These are **candidates**, not a finalized bill of materials. Verify electrical compatibility and operating requirements against datasheets before wiring.

## 5. Nonfunctional Requirements and Constraints

- Separate the UI, communications transport, protocol handling, and external application behavior.
- Provide clear diagnostics suitable for isolating failures at the serial, RF, and application boundaries.
- Define a message timeout and report stale/disconnected status; precise timeout **TBD**.
- Ensure remote equipment independently enforces safety-critical behavior if commands stop arriving; the UI alone is not a safety interlock.
- Define measurable packet-delivery, latency, and data-integrity criteria before corresponding tests; thresholds **TBD**.
- Begin with a wired UART verification before adding wireless integration.
- Keep firmware and software revisions, hardware configuration, and test evidence traceable.

## 6. Requirement Hierarchy

`SYS-001` is an **end-to-end** requirement. UART tests against `COM-001` and `COM-002` provide supporting evidence but cannot by themselves prove wireless operation. `GND` and `RMT` requirements contribute to the end-to-end system as distinct subsystems.

The FIELDLINK ground-station UI is **not a separate project**. Its [subsystem README](ground_station/ui/README.md) documents UI-specific development while this document remains the master requirements baseline.

## 7. Preliminary Verification Traceability

| Requirement | Test | Status | Evidence |
| --- | --- | --- | --- |
| COM-001 | TST-001 — UART command reception | Not tested | — |
| COM-002 | TST-001 — UART response transmission | Not tested | — |
| SYS-001 | TST-002 — LoRa end-to-end exchange (planned) | Not tested | — |
| GND-001–GND-004 | UI tests (IDs TBD) | Not tested | — |
| RMT-001–RMT-002 | Remote-node integration tests (IDs TBD) | Not tested | — |
| SYS-002, COM-003, COM-004 | Tests TBD | Not tested | — |

The test ID `TST-001` is distinct from requirements such as `COM-001`.

## 8. Planned Development Sequence

1. Review and approve system requirements and subsystem boundaries.
2. Define architecture, protocol boundaries, and interface contracts.
3. Implement basic wired UART PING/PONG using a simple ground-station console.
4. Integrate the LoRa radios and remote transceiver for bidirectional communication.
5. Develop the ground-station UI for commands, diagnostics, and telemetry.
6. Verify telemetry logging, fault handling, and reuse with an independent project.

This is a proposed sequence, not a record of completed implementation. UI and firmware modules may be developed in parallel once their interface is agreed.

## 9. Open Engineering Decisions

- [ ] Ground station UI framework and supported operating systems
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

**Review gate:** This updated document is a **draft for owner review**. It is not an approved or verified technical baseline. Do not start implementation based on unreviewed requirements.
