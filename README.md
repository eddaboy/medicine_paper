# Delphi Framework for AI-assisted Medical Diagnostics

This repository contains the data, completed language-model runs, Jupyter notebooks, statistical results and figures for a study of clinical protocol generation by multi-model Delphi panels. The analyses compare panel synthesis with individual models and budget controls, examine agreement and criterion recovery across discussion rounds, and evaluate clinical safety and transfer to MedMCQA.

The notebooks contain their analytical logic inline. Saved model responses and anonymized expert ratings provide the empirical inputs for reproducing the results.

## Contents

| Directory | Contents |
| --- | --- |
| `data/` | Clinical cases, scoring rubrics and source benchmark datasets |
| `experiments/` | Generation notebooks, completed responses, parameter sweeps and control experiments |
| `evaluations/` | Protocol judging, blind-sample selection, expert ratings and judge validation |
| `analyses/` | Main clinical analyses and additional analyses grouped by research topic |
| `results/` | Generated tables and figures, plus archived article tables and visuals |

See [STRUCTURE.md](STRUCTURE.md) for the directory map and the main notebook sequence.

The main outputs are written to `results/clinical_evaluation/tables/` and `results/clinical_evaluation/figures/`. The `supplementary/` subdirectories hold additional tables and figures. `results/archived_article/` preserves the empirical tables and visuals associated with the article, allowing comparison with the current calculations.

The data-preparation notebook in `experiments/external_benchmarks/initial_runs/` regenerates prepared external-benchmark CSVs from the included source datasets. Blind-sample construction notebooks preserve the recorded case identifiers and protocol assignments. Expert ratings are primary observations and are supplied as anonymized workbooks.

Configure the empty `API_KEY`, `FOLDER_ID` or equivalent variables in the relevant experiment or judge notebook before running it. New responses depend on model availability and sampling and constitute new experiments. The archived responses are the inputs used to reproduce the recorded results.


