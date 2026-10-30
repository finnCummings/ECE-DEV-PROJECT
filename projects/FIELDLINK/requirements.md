
# FIELDLINK — System Requirements

**Project:** FIELDLINK
**Status:** Draft
**Revision:** 0.1
**Date:** 2026-10-30

## System Objective

Develop a reusable, bidirectional LoRa communications
system capable of exchanging commands, telemetry, and
diagnostic information between a ground station and
different engineering projects.

## Functional Requirements

| ID | Requirement | Verification |
|---|---|---|
| SYS-001 | The system shall support bidirectional communication between a ground station and a remote node. | Demonstration |
| COM-001 | The system shall receive and interpret messages over UART. | Functional test |
| COM-002 | The system shall transmit response messages over UART. | Functional test |
| COM-003 | The protocol shall detect corrupted messages. | Fault-injection test |
| COM-004 | The system shall detect communication loss after a defined timeout. | Timeout test |
| SYS-002 | The communications interface shall support integration with different project applications. | Integration test |

## Design Constraints

- Use LoRa radio communication for the wireless link.
- Begin development with wired UART communication.
- Keep application-specific logic separate from
  communications logic.
- Prefer modular, replaceable hardware components.
- Prioritize reliability, testability, and maintainability.

## Development Phases

1. Wired UART communication
2. Bidirectional LoRa transmission
3. Message framing and error detection
4. Telemetry integration
5. Communication fault handling
6. Integration with other engineering projects

## Open Engineering Decisions

- Message format and framing
- UART baud rate
- Microcontroller-to-radio electrical interface
- Message addressing
- Response timeout
- Data integrity verification method
