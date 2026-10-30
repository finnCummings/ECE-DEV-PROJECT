# Engineering Guide

**Established:** 2026-10-30  
**Applies to:** ECE Development Project

## Purpose
Keep engineering work easy to understand, locate, reproduce, review, and maintain. Add only procedures that solve real problems.

## Where files belong
- `README.md`: portfolio landing page and project status.
- `portfolio/`: brief, evidence-backed case studies linking to engineering records.
- `projects/`: individual engineering projects, each with an overview, designs, code, component records, and tests.
- `ENGINEERING_GUIDE.md`: shared file organization and engineering practices.

Within a project, group work by system or subsystem where practical. Keep manufacturer datasheets distinct from original designs. A test involving several components belongs with the system or experiment, not inside an unrelated component folder. Link to authoritative files rather than duplicating them. Create new folders only when needed.

## File names and dates
Use descriptive lowercase `snake_case` for original files, except established tool filenames such as `README.md`. Use `YYYY-MM-DD` in dated records such as logs, test data, photographs, and exported reports. **Never use dates as folder names.**

Keep names of source code and actively edited CAD files stable; use Git history for changes. For manufacturer datasheets, preserve their part number and revision, and note acquisition dates in the component record. Avoid names such as `final_v3_revised`.

## Configuration and testing
- Use meaningful Git commits to record work; use branches and pull requests for collaboration or changes needing review.
- Record which hardware revision or physical configuration, software commit, and test conditions produced each important result.
- Never overwrite raw measurements. Give each test run its own dated name or unique run identifier.
- Store raw data separately from processed results. State units, measurement methods, and significant uncertainty.
- Keep editable design sources (KiCad, CAD, C, Python) alongside relevant exports.
- Mark capabilities accurately: planned, in development, or verified.
- Protect credentials and personal, controlled, and proprietary materials; do not publish sensitive records.

## New project initiation and requirements review

**Every new engineering project starts with a draft `requirements.md` for the project owner's review, before architecture design, implementation, or testing begins.**

1. Create the project directory and copy [`templates/requirements.md`](templates/requirements.md) into it as `requirements.md`.
2. Draft the objectives, scope, functional and nonfunctional requirements, interfaces, constraints, and planned verification methods. Give requirements stable unique IDs following the conventions below; label unknowns explicitly as **TBD**.
3. Commit the draft to GitHub and provide a direct link for review. Mark its status **Draft — Pending Review**.
4. **Wait for the project owner's feedback and approval before advancing to architecture, code, hardware design, or tests.** Revise the draft as requested and retain the review history through Git commits.
5. After approval, mark the document **Reviewed — Initial Baseline** and continue with the architecture and implementation plan. Any later requirement changes should be reviewed before they materially change scope.

Creating the initial project overview and requirements draft is permitted before review; do not treat a draft as an approved technical baseline. Keep this gate lightweight—one clear review, not excessive administration.

## Requirements identification and traceability

Assign each formal requirement a **stable, unique ID** so designs, tests, and evidence can refer to it without ambiguity. Use the format `PREFIX-NNN`, where the prefix identifies the requirement level or subsystem and the three-digit number is a sequential identifier within that category. These prefixes are **FIELDLINK project conventions**, not universal industry standards.

| Prefix | Scope | Example |
| --- | --- | --- |
| `SYS` | Complete system behavior | `SYS-001` — bidirectional ground-station-to-node communication |
| `COM` | Communication interfaces and protocol | `COM-001` — UART message reception |
| `PWR` | Power subsystem | `PWR-001` — power input requirements |
| `HWR` | Hardware and electrical interfaces | `HWR-001` — compatible logic voltage |
| `SWR` | Firmware/software behavior | `SWR-001` — packet validation behavior |

Introduce a prefix only when it helps distinguish actual requirements; avoid inventing unused categories. Assign new IDs in sequence, **do not reuse retired IDs**, and keep an ID stable when wording is revised. A requirement should state an observable or measurable outcome and have an identified verification method. Avoid treating a general aspiration like "reliable" as a verified requirement until it has measurable acceptance criteria.

### System-level versus subsystem requirements

System requirements describe the capability FIELDLINK must provide end to end. Subsystem requirements describe specific capabilities needed to accomplish it. For example:

- `SYS-001`: communicate bidirectionally between a ground station and a remote node.
- `COM-001`: receive and interpret a UART message.
- `COM-002`: send a UART response.

The two UART requirements contribute to `SYS-001`, but passing UART tests **does not establish that the LoRa end-to-end link meets `SYS-001`**. That requires separate system-level verification.

### Keep test IDs separate

Use `TST-NNN` for **test procedures or test cases**, never for requirements. For example, `COM-001` is a requirement, while `TST-001` can be the UART PING/PONG test that checks `COM-001` and `COM-002`. The same test may verify more than one requirement. Conversely, one requirement may need multiple tests.

A small traceability table in the project's requirements document is sufficient initially:

| Requirement ID | Verification test ID | Result | Evidence |
| --- | --- | --- | --- |
| `COM-001` | `TST-001` | Not tested | — |
| `COM-002` | `TST-001` | Not tested | — |
| `SYS-001` | `TST-002` (planned) | Not tested | — |

Update results **only after executing tests** and linking actual reports, raw data, or other evidence. Keep engineering logbooks identified by date and descriptive filename; a separate `LOG-NNN` series is unnecessary unless a genuine traceability need emerges. Existing examples labeled `COM-001_uart` should be renamed to `TST-001_uart` when the corresponding test directory is created.

## Practical workflow
1. Define the problem and what success means.
2. Design a simple solution, noting meaningful tradeoffs.
3. Build and test safely.
4. Record results, failures, and necessary configuration information.
5. Analyze, improve, and commit the work.

Use GitHub Issues for actionable tasks. Avoid unnecessary approval gates, redundant records, and process for process's sake.

## Engineering philosophy
> **Design it simply. Build it correctly. Test it rigorously. Expect it to break. Make it easy to fix.**

Ask of every rule or feature: *What problem does it solve? What happens without it? Is there a simpler way?*
