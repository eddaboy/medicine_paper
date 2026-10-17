# Repository structure

```text
data/
  external_benchmark_sources/
    medmcqa/
    pubmedqa/
  *.csv
experiments/
  clinical_protocols/
    single_model_baselines/
    delphi_panels/
  fixed_length_controls/
  homogeneous_panels/
  panel_parameter_sweeps/
  protocol_format_controls/
  token_budget_controls/
  external_benchmarks/
    initial_runs/
    medmcqa/
    pubmedqa/
evaluations/
  blind_protocol_selection/
    russian_translation/
    alternative_translation_runs/
  human_and_model_validation/
    expert_ratings/
    expert_agreement/
    healthbench_judge_validation/
  geval_clinical_protocols/
  geval_judges/
analyses/
  clinical_evaluation/
  statistical_inference/
  panel_mechanisms/
  protocol_design/
  round_dynamics/
  clinical_safety/
  evaluation_robustness/
  budget_efficiency/
  benchmark_transfer/
results/
  clinical_evaluation/
    tables/
      supplementary/
    figures/
      supplementary/
  archived_article/
    tables/
    table_images/
    figures/
```

## Data and experiments

`data/` holds the shared clinical corpus, rubrics and benchmark source files. Experiment directories contain generation notebooks and completed responses. Clinical protocols distinguish single-model baselines from Delphi panels; separate control directories vary protocol length, panel homogeneity, parameters, output format and token budgets. External benchmark experiments cover MedMCQA and PubMedQA, including common subsets and expanded panel comparisons.

`evaluations/` contains criterion-level judging, G-Eval scores, blind-sample selection, anonymized expert workbooks and judge validation. Translation prompts are stored as structured JSONL records. Human ratings and saved model responses are empirical observations; analysis notebooks do not recreate them.

## Main execution sequence

1. In `evaluations/human_and_model_validation/expert_agreement/`, run `recalculate_kappa.ipynb`, then `compare_human_protocol_scores.ipynb`.
2. In `experiments/external_benchmarks/medmcqa/benchmark_subsets/`, run `benchmark_condition_comparisons.ipynb`, then `expanded_panel_analysis/expanded_panel_comparisons.ipynb`.
3. Run `experiments/external_benchmarks/medmcqa/internal_source_difficulty_analysis.ipynb`.
4. Run the following notebooks in `analyses/clinical_evaluation/` in order:

| Notebook | Purpose |
| --- | --- |
| `01_clinical_corpus_and_scoring_rubric.ipynb` | Case composition and scoring criteria |
| `02_clinical_panel_and_baseline_comparisons.ipynb` | Main clinical comparisons |
| `03_criterion_recovery_and_synthesis.ipynb` | Content recovery and synthesis mechanisms |
| `04_delphi_rounds_and_consensus.ipynb` | Round effects and agreement |
| `05_panel_composition_and_organizer.ipynb` | Panel membership and organizer effects |
| `06_triage_accuracy_and_safety.ipynb` | Triage performance and safety |
| `07_repeated_runs_length_and_judge_robustness.ipynb` | Repeatability and evaluation robustness |
| `08_medmcqa_benchmark_results.ipynb` | MedMCQA performance |
| `09_token_costs_and_role_configurations.ipynb` | Token costs and role variants |
| `10_main_result_figures.ipynb` | Main study figures |
| `11_supplementary_tables_and_figures.ipynb` | Supplementary tables and figures |

The main sequence writes to `results/clinical_evaluation/`. `results/archived_article/` contains archived empirical tables and visuals; current calculations are written to separate output directories.

## Additional analyses

| Directory under `analyses/` | Topics |
| --- | --- |
| `statistical_inference/` | Clustered uncertainty, variance components, effective sample size, multiplicity and sample-size requirements |
| `panel_mechanisms/` | Criterion recovery, diversity, conformity, independent votes and organizer influence |
| `protocol_design/` | Panel size, temperature, question structure, stopping policies and exploratory panel comparisons |
| `round_dynamics/` | Cohort differences and changes across rounds |
| `clinical_safety/` | Triage accuracy, error costs and net benefit |
| `evaluation_robustness/` | Truncation, protocol length, judge verbosity, rubric ceilings and failure categories |
| `budget_efficiency/` | Generation and aggregation costs under comparable budgets |
| `benchmark_transfer/` | Transfer of mechanisms to MedMCQA and PubMedQA |

These notebooks use completed experiment files and save tables to their topic directories. See [README.md](README.md) for installation, optional model generation and the limits of the available human-rating, USC-draft and HealthBench evidence.
