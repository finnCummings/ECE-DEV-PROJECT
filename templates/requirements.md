# [Project Name] — System Requirements

**Project:** [PROJECT]  
**Document status:** Draft  
**Revision:** 0.1  
**Date:** YYYY-MM-DD  
**Author:** [Name]  
**Related architecture:** [architecture.md](architecture.md)

> Copy this template into the project folder as `requirements.md`. Keep requirement IDs stable and link tests to evidence. See [Engineering Guide](../ENGINEERING_GUIDE.md) when working from the template directory.

## 1. System Objective

Describe what the system is intended to accomplish, who or what uses it, and the boundaries of its responsibility.

## 2. Scope

**In scope:**  
- [Capability included in this project]

**Out of scope:**  
- [Capability owned by another project or deferred to future development]

## 3. Functional Requirements

Use **one verifiable statement per row**. Give each requirement a permanent ID following the Engineering Guide conventions. Do not number a test with a requirement ID.

| Requirement ID | Requirement (shall statement) | Verification method | Priority |
| --- | --- | --- | --- |
| SYS-001 | The system shall [observable end-to-end capability]. | System test | Must |
| COM-001 | The communications subsystem shall [observable communication behavior]. | TST-001 (planned) | Must |
| COM-002 | The communications subsystem shall [another independently verifiable behavior]. | TST-001 (planned) | Must |

## 4. Nonfunctional Requirements and Constraints

Include only constraints with a genuine technical basis. Replace vague words like *fast* or *reliable* with measurable targets once known.

| Requirement ID | Constraint or performance requirement | Acceptance criteria | Verification |
| --- | --- | --- | --- |
| [ID] | [E.g., timeout, range, electrical limits, maintenance requirement] | [Threshold, units, conditions] | [Inspection / analysis / test] |

## 5. Interfaces and Dependencies

| Interface / dependency | Connected system | Type / protocol | Notes |
| --- | --- | --- | --- |
| [Interface] | [External system] | [UART / USB / API / power / other] | [Voltage, baud rate, framing, assumptions, or TBD] |

Identify which project owns each side of the interface.

## 6. Requirement Decomposition

Describe important parent-child relationships. A subsystem test may support a system requirement, but **does not automatically verify end-to-end system behavior**.

| Parent requirement | Supporting requirement(s) | Rationale |
| --- | --- | --- |
| SYS-001 | COM-001, COM-002 | [Why these capabilities support the system goal] |

## 7. Verification and Traceability

Keep **requirement IDs** (e.g., `COM-001`) separate from **test IDs** (e.g., `TST-001`). A test may verify multiple requirements; one requirement may require multiple tests.

| Requirement ID | Test / verification ID | Status | Evidence link |
| --- | --- | --- | --- |
| SYS-001 | TST-002 (planned) | Not tested | — |
| COM-001 | TST-001 (planned) | Not tested | — |
| COM-002 | TST-001 (planned) | Not tested | — |

Valid status examples: **Not tested**, **In progress**, **Passed**, **Failed**, **Inconclusive**. Only mark **Passed** when supported by actual recorded evidence.

## 8. Open Engineering Decisions

- [ ] [Unresolved interface, performance target, safety condition, or design choice]

## 9. Change Notes

| Date | Revision | Change | Reason |
| --- | --- | --- | --- |
| YYYY-MM-DD | 0.1 | Initial draft | Establish requirements baseline |

Git preserves the authoritative change history; this table should summarize meaningful requirements decisions, not every edit.

## 10. References

- [Engineering Guide](../../ENGINEERING_GUIDE.md) — update the relative path when copying to a different project directory.
- [Relevant datasheets or standards]
- [Related issues, designs, tests, and experiment records]
