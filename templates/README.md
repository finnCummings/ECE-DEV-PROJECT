# Engineering Templates

These templates are **UTF-8 CSV files**, so they can be opened and edited directly in **Visual Studio Code** or a spreadsheet application. No extension is required to edit them as plain text.

## Templates

| File | Use |
| --- | --- |
| [engineering_log.csv](engineering_log.csv) | Record significant engineering sessions, troubleshooting, decisions, and next steps. |
| [test_plan.csv](test_plan.csv) | Define objective, equipment, configuration, variables, procedures, acceptance criteria, and safety before running a structured test. |
| [test_report.csv](test_report.csv) | Capture observed results, raw evidence references, interpretation, acceptance criteria, and follow-up work after a test. |

Each template has three columns: **Section**, **Field**, and **Entry**. Replace prompts and blanks in **Entry**; keep the **Section** and **Field** names so records are comparable.

## Use in VS Code

1. Open this repository in VS Code.
2. Copy a template to the relevant project folder, preserving the `.csv` extension.
3. Edit in the text editor or optionally use a CSV table-view extension for more convenient cell editing.
4. Commit the finished file with the associated code, design, or experimental record.

When manually editing CSV, **quote any cell containing commas, double quotes, or newlines** (double any interior quotation mark). If you edit the files in a spreadsheet application, export or save as CSV UTF-8.

## Naming and example

Use a unique dated filename for log entries, e.g. `2026-11-05_uart_setup.csv`. For one test, place the copied plan and report together in its test directory under stable names:

```text
projects/navcom/systems/communications/
├── logbook/
│   └── 2026-11-05_uart_setup.csv
└── tests/
    └── COM-001_uart/
        ├── test_plan.csv
        ├── test_report.csv
        ├── data/
        │   └── 2026-11-06_run_001.csv
        └── photos/
            └── 2026-11-06_test_setup.jpg
```

The structure above is **illustrative**, not evidence that the test has been run. Create directories and measurement files when they are actually needed.

The templates record narrative notes in CSV to match this workspace preference; more extensive technical narratives, diagrams, and code should remain in formats best suited to them, such as Markdown, KiCad, C, or Python.

See [Engineering Guide](../ENGINEERING_GUIDE.md) for shared conventions.
