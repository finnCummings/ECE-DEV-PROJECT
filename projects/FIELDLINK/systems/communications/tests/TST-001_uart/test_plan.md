# TST-001 — Wired UART PING/PONG Test Plan

**Project:** FIELDLINK  
**Status:** Draft — Not Executed  
**Date:** 2026-10-30  
**Related requirements:** COM-001, COM-002  
**Purpose:** Establish a repeatable UART command/response baseline before using LoRa hardware.

## Objective

Demonstrate that an embedded node receives defined serial commands and returns the correct response using a wired USB serial connection. This test isolates UART and command parsing from radio configuration and RF link failures.

## Initial hardware / software

- Arduino Uno R4 WiFi (candidate microcontroller)
- USB data cable and computer
- Arduino-compatible C/C++ development environment
- Serial Monitor or equivalent terminal

**No LoRa transceiver required for TST-001. No Python UI required.**

## Configuration to record before testing

| Configuration item | As-tested value |
| --- | --- |
| Board and serial port | TBD |
| Firmware Git commit | TBD |
| Baud rate | 9600 baud (proposed; confirm in firmware and terminal) |
| UART framing | 8 data bits, no parity, 1 stop bit (proposed) |
| Command termination | Newline (proposed) |
| Response termination | Newline (proposed) |
| USB cable / host | TBD |
| Test date | TBD |

## Proposed message behavior

- After receiving an exact newline-terminated `PING`, respond with `PONG` followed by a newline.
- For an unknown command, do not respond with `PONG`; an explicit `ERR` response is acceptable if documented.
- The parser must not treat a partial command as complete before the newline.
- No claim is made yet about bytes on the air, RF packet delivery, or remote telemetry.

## Test steps

1. Identify the correct serial port and record the hardware and firmware configuration.
2. Program firmware to accept the defined serial input and output a response.
3. Open a serial terminal configured to the firmware's baud rate and newline setting.
4. Send one valid `PING`, record the exact response and confirm framing.
5. Send an invalid command (e.g., `PANG`), verify it does not return `PONG`.
6. Send a partial command before newline; verify it is not processed prematurely.
7. Repeat the valid exchange **100 times** using a reproducible procedure (a serial terminal is sufficient initially; automation is optional).
8. Restart or reconnect and verify the exchange again.
9. Record observations, configuration, deviations, and any failures in a copied `test_report.md` when the experiment actually occurs.

## Proposed acceptance criteria — review during implementation

| Criterion | Acceptance threshold | Method |
| --- | --- | --- |
| Correct command/response | 100 correct `PONG` responses to 100 complete `PING` commands | Count responses |
| Response time | Within 1 second after each complete command | Timing method TBD |
| Invalid command handling | Invalid command does not yield `PONG` | Send invalid command |
| Partial message handling | No response until full delimiter received | Send fragmented command |
| Restart recovery | Valid `PING` succeeds after reset/reconnect | Manual demonstration |

A serial terminal alone may not support trustworthy per-exchange latency measurement. **Do not claim the one-second timing criterion was verified without an adequate measurement method.** If timing cannot be measured, record that criterion as **inconclusive**.

## Safety and troubleshooting

- Use USB serial first; do not connect LoRa modules during this test.
- Avoid connecting unverified voltage levels between hardware devices.
- Record any port errors, unintended resets, lost messages, or mismatched settings.
- Stop and troubleshoot unexpected electrical behavior before continuing.

## Results and evidence

**Not tested.** Later evidence should include:
- firmware source and Git commit;
- terminal transcript or measurements;
- actual configuration;
- completed test report;
- pass/fail/inconclusive status for each criterion.

## Next experiment

After TST-001 passes, create a **separate test plan** for bidirectional LoRa PING/PONG, including radio configuration, power and logic-level verification, antenna requirements, and message integrity checks.
