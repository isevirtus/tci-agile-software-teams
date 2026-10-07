# Data and analysis notes

## Original files and derived artifacts

`TCI.xlsx`, `CFA.jasp`, and `Script e syntax.docx` are preserved byte-for-byte as supplied by the study authors. The CSV files and the preparation script were added to make the material easier to inspect and reuse. Selected JASP result tables are extracted from the saved project; extraction is not re-estimation.

The preparation script successfully checked that the workbook and JASP contain the same 148 response rows in the same order. All 38 columns match exactly, all responses are integers in 1–5, and no item value is missing. JASP stores internal category codes, so the script decodes each column through the corresponding label mapping before comparing the values.

## Workbook layout

The single worksheet is named `TCI_148_B`:

- **A1:AL1** contains the Portuguese item headers.
- **A2:AL2** contains short variable names (`tv1` through `ps12`).
- **A3:AL150** contains the 148 × 38 response matrix.
- Columns **AM:AP** contain dimension-score formulas, **AQ** the overall-score formula, **AR** an original-row field (`linha_original`), and **AT** source notes.

The score formulas begin one row above the response matrix. For example, `AM2 = AVERAGE(A3:K3)`, while `AM3 = AVERAGE(A4:K4)`. `AQ2 = AVERAGE(AM2:AP2)` consequently corresponds to the first response row at row 3. The original-row field also starts at row 2. A reader treating all populated columns on a worksheet row as the same participant would misalign them. The clean CSV exports only A3:AL150, and all derived score summaries are recomputed from those item values. No workbook formulas or source-row labels are copied into participant records.

The source note reads:

> Versão B: exclui a linha original 43 e mantém a 112. É igualmente compatível com o banco final pelos escores agregados.

In English: Version B excludes original row 43 and retains row 112, and is equally compatible with the final dataset in terms of aggregate scores. This is a statement in the supplied workbook, not a selection decision made by the preparation script. The original candidate dataset and the record explaining that choice were not supplied. Exact agreement with the embedded JASP data establishes which matrix this project contains; it does not independently establish the historical selection rationale.

## Software and saved options

The project manifest records **JASP 0.98.1**. Its analysis metadata records **jaspFactor 0.95.5**. The `version = "0.95.5"` argument in the DOCX is consistent with the module metadata and does not contradict the application version.

The saved options specify:

- Raw ordinal input, WLSMV estimation, and `standardized = "all"`.
- Four correlated factors with the 11/7/8/12 item allocation documented in the codebook.
- Marker-variable identification, default standard errors, and listwise deletion.
- Additional residual associations `tv7 ~~ tv8` (TCI7–TCI8) and `ps9 ~~ ps10` (TCI35–TCI36).
- No grouping variable, no second-order factor, and no requested AVE or HTMT output in this saved analysis.

The exported call includes `sampleSize = 200`, but also `dataType = "raw"`. The actual embedded dataset contains 148 rows. Do not describe 200 as the observed sample size. The DOCX's `data = NULL` is part of an exported JASP call and does not supply a dataset to a standalone R session. Its printed grouping argument also differs in form from the saved project's empty grouping option. Use the saved project to inspect the original configured analysis.

The model syntax file contains factor definitions and residual associations only. It is not a complete lavaan execution script, and no successful R/lavaan re-estimation is claimed here.

## Checks performed

The basic summaries recomputed from the item matrix are:

| Dimension | Mean | Sample SD | Raw-item alpha |
|---|---:|---:|---:|
| Vision | 4.213759 | 0.589813 | 0.904639 |
| Task Orientation | 4.069498 | 0.689560 | 0.894370 |
| Support for Innovation | 3.965372 | 0.760670 | 0.927238 |
| Participative Safety | 4.198198 | 0.733305 | 0.946397 |

These alpha values agree with the saved JASP table. Alpha over all 38 items is 0.969398. The equal-dimension-weight overall score has mean 4.111707 and sample SD 0.615187. These descriptive computations neither establish unidimensionality nor supply a reliability estimate for that overall score.

Exact five-category counts are available in `results/item_frequencies.csv`. Each item's counts sum to 148. `results/jasp_saved_results.json` provides the saved fit, loading, factor-correlation, residual, and reliability tables together with the saved options.

## Details still requiring original records or further analysis

1. **Total omega:** the saved table gives 1.014389 for the total. This is inadmissible as a reliability estimate. It must be investigated, not rounded down or interpreted as exceptionally high reliability. The four saved dimension omega values are .941962, .912123, .972656, and .975721; they have not been independently re-estimated by this package.
2. **Original additional analyses:** the supplied DOCX contains a CFA export and model syntax. It does not contain the original Python scripts for HTMT, score-distribution tests, Friedman/Wilcoxon comparisons, or figure generation. The preparation script is newly added packaging code and does not replace those original analysis scripts.
3. **Initial factor model:** the saved output's “Baseline model” is the CFA independence/reference model. It must not be presented as the initially specified four-factor model before residual modifications. That earlier four-factor fit is not supplied.
4. **Demographics and clustering:** no age, gender, role, team identifier, or personality columns are present in the released item matrix. The files cannot reproduce demographic tables, confirm membership of the 16 teams, or support a team-dependence analysis by themselves.
5. **Questionnaire and provenance:** the complete questionnaire and response labels are available in [instrument/](../instrument/). The original row-selection record for Version B and exact collection dates remain to be established.

The recorded analysis status is `complete`. That status and the stored result tables do not substitute for a fresh assessment of model admissibility, numerical stability, or sensitivity to the specification.
