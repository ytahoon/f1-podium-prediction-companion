# Formula 1 Podium Prediction Companion

ACL Milestone 1: relational data auditing, three analytical questions, leakage-safe
pre-race features, model comparisons, experiments, explainability and inference.

## Main files

- [Notebook0.ipynb](Notebook0.ipynb): complete executed notebook, in milestone order.
- [Analytical PDF report](reports/ACL_Milestone_1_Report.pdf): eight summary pages
  and an appendix containing all 32 static notebook figures.
- [Final model comparison](reports/complete_modeling_report.csv): training,
  validation and unseen-test results for all three final models.
- [Modeling table](reports/modeling_table.csv): one row per driver-race with
  unfilled original-unit features; `podium` is the target.
- [Final model inputs](reports/final_model_inputs.csv): the prepared 17 inputs,
  with identifiers/split/target retained separately for traceability.
- [Reproducibility record](reports/reproducibility_report.json), including data hashes.

## Run locally

Use Python 3.11 or newer. The verified environment used Python 3.13.7; exact
tested library versions are in `requirements-tested.txt`.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m ipykernel install --user --name acl-f1 --display-name "ACL F1"
python -m jupyterlab
```

Put the 14 supplied CSVs in `F1 Data` beside the notebook, select the project
kernel, restart it and choose Run All. Alternatively set `F1_DATA_DIR` to the
folder containing the CSVs. Data remain immutable; cleaning uses copies.

The source dataset referenced by the milestone is
[Formula 1 World Championship / Ergast on Kaggle](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020).
This work uses the supplied 2024 snapshot, not an automatically refreshed dataset.
The exact CSV hashes are recorded for reproducibility. The original raw data and
private working backups are not committed to this repository.

## Kaggle

Import `Notebook0.ipynb`, attach the supplied CSV snapshot and enable Internet
if dependency installation is needed. The setup cell discovers the attached CSV
folder under `/kaggle/input`. No GPU is required. Save an executed version and
verify that the evaluator can access the notebook and its data sources.

Kaggle submission is separate from this GitHub repository. Import the main
`Notebook0.ipynb`, attach the supplied data snapshot and save an executed version.

## What the notebook does

1. Clean and audit all 14 tables, with before/after EDA.
2. Answer circuit conversion, home-country advantage and mechanical-retirement questions.
3. Create prior-race form and standings features, and split chronologically.
4. Compare logistic regression, random forest and a shallow neural network.
5. Compare six feature-group removals and two preprocessing orders; freeze choices.
6. Complete unseen-test evaluation and complete/partial inference demonstrations.
7. Explain the selected model with permutation importance, SHAP and LIME.

Final test evaluation intentionally follows the experiments: features, models
and thresholds must be fixed first. XAI follows the frozen-model evaluation.

## Final setup and limitations

Train: 2003-2018. Validation: 2019-2021. Test: 2022-2024. The selected neural
network has 32/16 hidden units, nine numeric inputs and eight missing flags,
with training-median filling followed by scaling. Its fixed threshold is 0.43.
Validation PR-AUC is 0.7638; test PR-AUC is 0.7078 and test F1 is 0.6730.
The model remains selected using validation, not the test ranking.

Historical constructor conflicts and flagged timing/lap records remain pending
TA guidance. Their original values are retained; the disputed fields are not
final model inputs. Mechanical rates are status-based estimates. The selected
LIME explanation has weak local fidelity (R² 0.293). XAI is not causal evidence.

The inference function accepts precomputed pre-race feature values in original
units. It does not retrieve live results or reconstruct history from a driver ID.

## Repository scope

`Notebook0.ipynb` is the only submission notebook. Older notebooks, backups,
duplicate upload bundles and intermediate report exports are archived outside
the project folder. The repository retains the analytical PDF, final comparison
table, modeling tables and reproducibility records.
