# FIELDLINK — Ground Station UI Subsystem

**Status:** Planning  
**Subsystem:** Ground station / UI  
**Parent project:** [FIELDLINK](../../README.md)

## Mission

Build a reusable desktop user interface for controlling and monitoring engineering projects through the [FIELDLINK](../../README.md) communications platform. The interface should work across future projects without rewriting the shared transport and diagnostics logic.

## Responsibilities

- Connect to a FIELDLINK communications endpoint (initially a serial/USB interface).
- Display connection state, selected port, configured baud rate, and last received message time.
- Send well-defined commands and show acknowledgments, responses, and errors.
- Display and log telemetry with timestamps and units when provided.
- Expose diagnostic information for troubleshooting.
- Provide a modular way to add project-specific controls, such as a sensor dashboard or a TBM control panel.

The ground station UI **does not** implement LoRa packet transport on its own. It communicates with the FIELDLINK interface and should not depend on project-specific application logic.

## Proposed architecture

```text
Human operator
      |
Ground station UI (desktop application)
      |
Application command / telemetry API
      |
USB serial adapter / PC UART connection
      |
FIELDLINK ground-side transceiver
      |
        LoRa wireless link
      |
FIELDLINK remote transceiver
      |
Remote project (TBM, sensor payload, future systems)
```

This is a conceptual architecture, not verified wiring or a finalized API.

## Initial implementation direction

- **Language:** Python, consistent with the existing serial development workflow.
- **Interface framework:** To be evaluated after requirements are defined (e.g., a simple native Python GUI).
- **Transport:** Keep serial I/O, packet parsing, and user-interface code in separate modules.
- **Data logging:** Prefer timestamped CSV for numerical data and readable text logs for diagnostics.
- **Safety:** Disable unsafe commands if communication is stale or disconnected; remote systems must independently enforce their own safe states.

## Planned development phases

| Phase | Deliverable | Status |
| --- | --- | --- |
| 1 | Requirements and interface specification | Planned |
| 2 | Basic desktop UI with serial connection controls | Planned |
| 3 | PING/PONG command console and response display | Planned |
| 4 | Packet validation, error indicators, and diagnostic log | Planned |
| 5 | Live telemetry display and CSV recording | Planned |
| 6 | Reusable project-specific views | Future |

## Integration contract

The UI sends commands and receives responses/telemetry through a documented FIELDLINK application interface. Message structure, addressing, status codes, timeouts, and version compatibility will be defined by the FIELDLINK system architecture and protocol; do not assume an unverified protocol.

## Documentation and evidence

Use the [Engineering Guide](../../../../ENGINEERING_GUIDE.md) and [shared templates](../../../../templates/) to record design decisions, test plans, tests, and results.

**No implemented UI or validated communications capabilities are claimed yet.**
