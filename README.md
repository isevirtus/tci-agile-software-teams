# Team Climate Inventory in agile software teams

Supplementary material for **What Do Team Climate Scores Tell Us? A Psychometric Study of Agile Software Teams**, by Mirko Perkusich, Icaro Costa, Ramon Santos, Emilia Mendes, Danyllo Albuquerque, and Angelo Perkusich.

The study examines the internal structure, internal consistency, and dimensional separation of a Brazilian Portuguese Team Climate Inventory (TCI) among 148 professionals from 16 agile software teams. The analyses concern individual perceptions. The shared item matrix contains 38 five-category responses per person; it does not include team identifiers or demographic variables.

## Files

| File | Contents |
|---|---|
| [data/TCI.xlsx](data/TCI.xlsx) | Original supplied workbook, preserved unchanged. Read the layout notes before using its score columns. |
| [data/tci_items.csv](data/tci_items.csv) | Analysis-ready 148 × 38 item matrix, verified against the data embedded in the JASP project. |
| [data/codebook.csv](data/codebook.csv) | Variable names, manuscript item identifiers, dimensions, and Portuguese item headers from the workbook. |
| [analysis/CFA.jasp](analysis/CFA.jasp) | Original supplied JASP project with embedded data, options, and saved CFA output. |
| [analysis/Script e syntax.docx](analysis/Script%20e%20syntax.docx) | Original supplied analysis-script and syntax document. |
| [analysis/jasp_export.R](analysis/jasp_export.R) | JASP function call extracted from the DOCX. This requires JASP's module environment and is not a standalone R script. |
| [analysis/cfa_model.lav](analysis/cfa_model.lav) | Extracted factor-model syntax with line breaks normalized. |
| [scripts/prepare_data.py](scripts/prepare_data.py) | Recreates the clean CSV, codebook, frequencies, basic score summaries, and selected saved-output exports. |
| [results/](results/) | Derived item frequencies, basic score summaries, saved JASP tables, and validation metadata. |
| [docs/DATA_NOTES.md](docs/DATA_NOTES.md) | Source layout, dataset provenance, analysis settings, and unresolved details. |

## Use the data

For analyses outside JASP, use `data/tci_items.csv`. Its column order follows the administered questionnaire:

| Dimension | CSV variables | Manuscript items | Score |
|---|---|---|---|
| Vision | `tv1`–`tv11` | TCI1–TCI11 | Mean of 11 items |
| Task Orientation | `to1`–`to7` | TCI12–TCI18 | Mean of 7 items |
| Support for Innovation | `si1`–`si8` | TCI19–TCI26 | Mean of 8 items |
| Participative Safety | `ps1`–`ps12` | TCI27–TCI38 | Mean of 12 items |

Responses are integers from 1 to 5, with larger values indicating a more favorable perception. No item is reverse-scored. The descriptive overall score is the mean of the **four dimension means**, giving equal weight to each dimension. It is not the mean of all 38 items.

The provided matrix has no missing item responses. Item wording in the codebook reproduces the workbook headers; the files do not establish the exact verbal response anchors used on the original survey form.

## Recreate the derived files

From the repository root, using Python 3.10 or later:

```sh
python -m venv .venv
# Activate .venv using the command appropriate to your operating system.
python -m pip install -r requirements.txt
python scripts/prepare_data.py
```

The script reads the originals without modifying them. It checks all 5,624 item values against the decoded JASP data, exports exact counts for all five response categories, and recomputes dimension means, sample standard deviations, medians, endpoints, and raw-item alpha. It also extracts selected **previously saved** JASP results into JSON. It does not refit the CFA, estimate omega, calculate HTMT, or recreate the original Friedman/Wilcoxon analyses.

The original files' SHA-256 checksums and the executed checks are in [results/validation.json](results/validation.json). Dependency pinning in `requirements.txt` describes the preparation script, not the original study's full software environment.

## Inspect the CFA

Open `analysis/CFA.jasp` in **JASP 0.98.1**, the application version recorded in the project. Its `jaspFactor` module version is **0.95.5**, also shown in the exported function call. These are different version identifiers.

The saved analysis uses ordinal items, WLSMV, four correlated factors, marker-variable identification, listwise missing-data handling, and the additional residual associations `tv7 ~~ tv8` and `ps9 ~~ ps10`. All 148 records in the project are included. Saved fit indices are CFI = .943, TLI = .939, RMSEA = .086, and SRMR = .089. The initial model without those two residual associations is not included.

The saved reliability table contains **total omega = 1.014**, outside its admissible range. It is retained in the archived output for transparency and must not be used as valid reliability evidence. See the [data notes](docs/DATA_NOTES.md) for this and the workbook's Version B provenance note. A full re-estimation of the original analyses remains necessary before claiming complete computational reproduction.

## Relationship to the earlier study

These are the same participants and TCI responses used in Guimarães et al. (2024), *Investigating the relationship between personalities and agile team climate: A replicated study*, [Information and Software Technology, 169, 107407](https://doi.org/10.1016/j.infsof.2024.107407). That article investigated personality–climate relationships. The present manuscript addresses distinct psychometric research questions and analysis procedures. Personality variables are not part of this package.

## Citation and reuse

The accompanying manuscript is a draft; no accepted publication or DOI is asserted. [CITATION.cff](CITATION.cff) identifies the supplementary dataset and authors. Cite the relevant repository commit when using this material. No reuse license has been specified in this repository.
