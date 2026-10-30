# Engineering Documentation Templates

These are reusable **Markdown (`.md`) templates**, intended to be copied into the appropriate project directory and edited in **Visual Studio Code**. Markdown supports readable headings, tables, checklists, code, and internal links; GitHub also renders it automatically.

## Open a template directly in VS Code for the Web

| Template | Purpose | Open in VS Code |
| --- | --- | --- |
| [Engineering Log](engineering_log.md) | Work sessions, results, troubleshooting, decisions, and next steps | [Open editor](https://github.dev/finnCummings/ECE-DEV-PROJECT/blob/main/templates/engineering_log.md) |
| [Test Plan](test_plan.md) | Objective, setup, method, variables, acceptance criteria, and safety | [Open editor](https://github.dev/finnCummings/ECE-DEV-PROJECT/blob/main/templates/test_plan.md) |
| [Test Report](test_report.md) | Actual measured results, evidence, interpretation, and conclusions | [Open editor](https://github.dev/finnCummings/ECE-DEV-PROJECT/blob/main/templates/test_report.md) |

[Open the full repository in VS Code for the Web](https://github.dev/finnCummings/ECE-DEV-PROJECT)

You can also press **`.`** while viewing the repository on GitHub to open the browser-based VS Code editor.

## Using templates

1. Open the editor and find a template under `templates/`.
2. **Copy** the template into your project directory (do not fill in or overwrite the master).
3. Name dated session logs with `YYYY-MM-DD`, for example `2026-11-05_uart_setup.md`.
4. Keep the test plan and report together in a test-specific directory with stable names.
5. Replace the placeholders with **actual** measurements, configuration information, and evidence; commit your work.

### Example organization — not yet executed

```text
projects/
└── fieldlink/
    └── systems/
        └── communications/
            ├── logbook/
            │   └── 2026-11-05_uart_setup.md
            └── tests/
                └── COM-001_uart/
                    ├── test_plan.md
                    ├── test_report.md
                    ├── data/
                    │   └── 2026-11-06_run_001.csv
                    └── photos/
                        └── 2026-11-06_test_setup.jpg
```

**Use Markdown for engineering records and CSV for raw tabular measurement data**, such as sensor readings, latency measurements, or repeated experiment results.

In desktop VS Code, use **Ctrl+Shift+V** to preview Markdown. The browser editor is suitable for documentation; local VS Code is better for hardware access, firmware development, and test scripts.

See the [Engineering Guide](../ENGINEERING_GUIDE.md) for file naming and configuration conventions.
