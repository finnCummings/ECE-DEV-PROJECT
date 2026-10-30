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
