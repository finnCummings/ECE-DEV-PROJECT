# ECE Development Project

**Electrical Engineering · Applied Learning · Living Technical Portfolio**

## Mission

I am developing practical, transferable engineering skills alongside my Electrical Engineering studies at North Carolina State University. My aim is to turn classroom knowledge into **working, tested systems** and demonstrate my understanding of the engineering process through reproducible evidence.

This repository is both my engineering workspace and a public portfolio of what I define, design, build, test, troubleshoot, improve, and learn.

## Engineering Philosophy

> **Design it simply. Build it correctly. Test it rigorously. Expect it to break. Make it easy to fix.**

My experience maintaining F-15 aircraft in the U.S. Air Force taught me to value reliability, maintainability, fault isolation, and the technician who has to troubleshoot equipment when it fails.

The engineering cycle here is **define → design → build → test → analyze → improve**. A failure is useful when it is documented, investigated, and translated into a better design.

## Skills I Am Building

- **Embedded development:** C/C++, microcontrollers, UART, peripheral integration, interrupt-driven design, and eventually custom KiCad PCBs.
- **Communications:** bidirectional links, framing, reliability, diagnostics, and integration with established protocols.
- **Controls and automation:** sensors, motor control, feedback, PID, and autonomous behaviors in future prototypes.
- **Test engineering:** requirements, repeatable experiments, fault injection, instrumentation, data analysis, and verification reports.
- **Engineering judgment:** modular design, trade studies, safe failure states, serviceability, and configuration management.

## Projects

| Project | Objective | Status |
| --- | --- | --- |
| **[FIELDLINK](projects/FIELDLINK/)** | Develop a reusable **communications, integration, and diagnostic test platform** that connects diverse embedded devices through protocol adapters, normalizes telemetry, and produces traceable evidence. Begin with wired UART and bidirectional LoRa; evaluate Modbus and MAVLink adapters later. | Requirements update proposed; communications baseline planned |
| **Miniature TBM** | Explore motor control, navigation, autonomy, fault handling, and maintainability on a small robotic testbed; a potential future integration target for FIELDLINK. | Concept |

The [portfolio](portfolio/) will present compact, evidence-backed case studies linked to actual engineering work—not just project descriptions.

## FIELDLINK: Why Build It?

Existing protocols such as **MAVLink** and **Modbus** are useful standards, not competitors that FIELDLINK must replace. The long-term goal is to connect supported protocols through **adapters**, preserve source-specific information, and expose a common device-health and diagnostic model for experiments across different projects.

The differentiator to test is **reusability, troubleshooting, and verification**. Comparative superiority, packet delivery rate, and reliability must be demonstrated rather than assumed.

A graphical ground-station UI is **deferred** until the communications and diagnostics foundations work. Early experiments use embedded C/C++, a serial monitor, and existing hardware; Python is not a prerequisite.

## Current Focus

1. **D03:** Confirm FIELDLINK architecture and review proposed v0.3 requirements; maintain the previously approved v0.2 requirements baseline until reviewed.
2. **TST-001:** Implement and execute wired UART PING/PONG; record a test report and evidence.
3. **TST-002 (planned):** Demonstrate bidirectional LoRa communication with verified hardware settings.
4. Add packet integrity, timeouts, structured records, and a second adapter only after validating the fundamentals.

See the [FIELDLINK architecture](projects/FIELDLINK/architecture.md), [Engineering Guide](ENGINEERING_GUIDE.md), and [documentation templates](templates/).

**Project status is evidence-based. No planned FIELDLINK feature is represented as tested or verified without supporting records.**
