# FIELDLINK — Modular LoRa Communications System

**Status:** Planning  
**Project type:** Integrated reusable communications system

## Mission

Design, build, and verify a **reusable, bidirectional LoRa transceiver system** that transfers commands, telemetry, and diagnostic information between a ground station and independently developed engineering projects.

FIELDLINK is intended to be a **communications building block**, not a communications implementation locked to one robot or payload. A miniature tunnel boring machine, remote sensor platform, or future project should be able to use the same underlying message transport through a documented interface.

## Engineering objectives

1. Implement a basic command/response exchange over wired UART.
2. Develop a clear message framing and command/telemetry interface.
3. Integrate bidirectional communication using LoRa UART radio modules.
4. Add message validation, error handling, communication timeout behavior, and test evidence.
5. Demonstrate telemetry from a sensor node and generalize the interface for other projects.
6. Explore addressing and multiple remote nodes as a **future capability**, after reliable point-to-point links are demonstrated.

## Key design principles

- **Project agnostic:** Payload or motor-control logic stays in the application, not the communications layer.
- **Modular:** Hardware, protocol, ground-station software, and project application can evolve separately.
- **Reliable and testable:** Specify measurable behavior and keep raw test evidence.
- **Maintainable:** Clear wiring, straightforward debugging, and replaceable components.
- **Safe failures:** Remote control integrations must account for stale or lost commands.

## Operator interface

FIELDLINK contains the [ground station UI](ground_station/ui/README.md), ground-side transceiver, shared message protocol, and remote transceiver as parts of one integrated system. The UI manages operator commands, telemetry visualization, and diagnostics; the transceivers handle transport. External applications remain independent projects.

The [master system requirements](requirements.md) cover all FIELDLINK subsystems and are currently **Draft — Pending Review**.

## Initial development hardware

Candidate hardware from previous experiments: Arduino Uno R4 WiFi, EBYTE E32-900T20D UART LoRa modules, CP2102 USB-to-UART adapter, and a PC-based Python ground station. Exact voltage levels, pin assignments, operating modes, and configuration will be confirmed against the relevant datasheets before wiring.

## First milestone: D03  Architecture and requirements

Document the logical ground-station-to-node architecture, module interfaces, initial requirements, and a **TST-001 wired UART PING/PONG test plan**.

**No FIELDLINK hardware or firmware testing is claimed by this document.**

## Roadmap

| Phase | Scope | Status |
| --- | --- | --- |
| 1 | Requirements and architecture review; UART commands and responses | Planning |
| 2 | LoRa point-to-point link | Planned |
| 3 | Message integrity and fault handling | Planned |
| 4 | Ground station UI, sensor telemetry, and logging | Planned |
| 5 | Project-agnostic integration | Planned |
| 6 | Optional multi-node support | Future |

Follow the [Engineering Guide](../../ENGINEERING_GUIDE.md) and use the [documentation templates](../../templates/) for records.
