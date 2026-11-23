# OsdagBridge Testing & Issue Reporting - Short-Span Steel Girder Module

Test harness, plan, log and report template for the OsdagBridge testing task.

> **Honesty note:** this scaffold contains the *plan* and tooling only. No test results, bugs, screenshots or video exist until you run the software. Do not submit placeholders as findings.

## Layout
| Path | Purpose |
|---|---|
| `docs/TEST_PLAN.md` | 42 planned cases (A basic, B additional, C custom materials, D multi-run, E outputs, F negative) + procedure + pass/fail rules |
| `test_log.xlsx` | Test-case log with status dropdowns, Summary (formulas), Multi-Run, Dict Comparison, Issues sheets |
| `scripts/compare_dicts.py` | `ui-vs-input`, `output-vs-report`, `run-diff` comparisons (tolerance-aware, CSV export) |
| `scripts/build_test_matrix.py` | Regenerates plan + log; edit the `TC` table, then re-run |
| `scripts/make_zip.py` | Builds the submission ZIP |
| `report/main.tex` | LaTeX report skeleton (Overleaf-ready); search for `TODO` |
| `issues/` | GitHub issue template and duplicate-check log |
| `video/STORYBOARD.md` | Screencast shot list |
| `test_cases_osi/`, `evidence/` | Put your `.osi` files, screenshots, tracebacks, dictionaries here |

## Workflow
1. Do the setup from the task brief (fork, clone, `conda env create`, launch).
2. **Adapt parameter names/ranges** in `scripts/build_test_matrix.py` to the real UI, re-run it.
3. For each case: enter inputs -> save `.osi` -> dump input dict -> design -> dump output dict -> screenshots.
4. Compare: 
   ```bash
   python scripts/compare_dicts.py ui-vs-input ui_values.json evidence/dictionaries/TC-A01_in.json --csv evidence/logs/TC-A01_in.csv
   python scripts/compare_dicts.py output-vs-report TC-A01_out.json report_values.json
   python scripts/compare_dicts.py run-diff run1_out.json run2_out.json
   ```
   `ui_values.json` = flat `{"Label": value}` you type by hand from the UI. If key names differ, pass `--map mapping.json`. `.osi` files are read via PyYAML when installed.
5. Log results in `test_log.xlsx`; for failures, search existing GitHub issues, then file using `issues/ISSUE_TEMPLATE.md` (or comment on the existing issue).
6. Fill `report/main.tex`, compile on Overleaf, record the video, tick `docs/SUBMISSION_CHECKLIST.md`, run `python scripts/make_zip.py`.
