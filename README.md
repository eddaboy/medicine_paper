# Clinical multi-model Delphi experiments

This repository contains the data, completed language-model runs, Jupyter notebooks, statistical results and figures for a study of clinical protocol generation by multi-model Delphi panels. The analyses compare panel synthesis with individual models and budget controls, examine agreement and criterion recovery across discussion rounds, and evaluate clinical safety and transfer to MedMCQA and PubMedQA.

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

## Reproduce the results

Use Python 3.13, the version used for the original verification, or a compatible Python version supported by `pyproject.toml`. From the repository root:

```bash
python -m venv .venv
```

Activate the environment using `.venv\Scripts\Activate.ps1` in Windows PowerShell or `source .venv/bin/activate` on Linux/macOS, then install the analysis environment:

```bash
python -m pip install .
python -m jupyter lab
```

Run each notebook from top to bottom. Paths resolve within the repository. The recommended sequence is:

1. Recalculate expert agreement and protocol scores with `recalculate_kappa.ipynb`, followed by `compare_human_protocol_scores.ipynb`, in `evaluations/human_and_model_validation/expert_agreement/`.
2. Run `benchmark_condition_comparisons.ipynb` in `experiments/external_benchmarks/medmcqa/benchmark_subsets/`, followed by `expanded_panel_analysis/expanded_panel_comparisons.ipynb` and `experiments/external_benchmarks/medmcqa/internal_source_difficulty_analysis.ipynb`.
3. Run notebooks `01`–`09` in `analyses/clinical_evaluation/` in numerical order, then `10_main_result_figures.ipynb` and `11_supplementary_tables_and_figures.ipynb`.
4. Run the additional topic analyses in `analyses/` as needed. They use the included completed experiment data; their outputs remain within the corresponding thematic directories.

The main outputs are written to `results/clinical_evaluation/tables/` and `results/clinical_evaluation/figures/`. The `supplementary/` subdirectories hold additional tables and figures. `results/archived_article/` preserves the empirical tables and visuals associated with the article, allowing comparison with the current calculations.

The data-preparation notebook in `experiments/external_benchmarks/initial_runs/` regenerates prepared external-benchmark CSVs from the included source datasets. Blind-sample construction notebooks preserve the recorded case identifiers and protocol assignments. Expert ratings are primary observations and are supplied as anonymized workbooks.

## Collect new model responses

Install the optional generation dependencies:

```bash
python -m pip install ".[generation]"
```

Configure the empty `API_KEY`, `FOLDER_ID` or equivalent variables in the relevant experiment or judge notebook before running it. New responses depend on model availability and sampling and constitute new experiments. The archived responses are the inputs used to reproduce the recorded results.


