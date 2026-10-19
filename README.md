# Formula 1 Podium Prediction Companion

ACL Milestone 1: data cleaning, three analytical questions, leakage-safe features,
model comparisons, experiments, explainability and pre-race inference.

## Run the notebook

Notebook0.ipynb is the main submission notebook. Use the project Python
environment, select its kernel in VS Code or Jupyter, restart and choose Run All.

The verified environment uses Python 3.13.7. Install requirements-tested.txt
for the tested package versions, or requirements.txt for compatible dependencies.
JupyterLab is an optional interface; VS Code can use the existing Python kernel.

Put all 14 supplied CSVs in F1 Data, set F1_DATA_DIR, or attach the supplied
dataset on Kaggle. The dataset is the 2024 snapshot referenced by the milestone:
[Formula 1 World Championship / Ergast](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020).
Raw CSVs are immutable. Run All recreates cleaned DataFrames and saves local
tables, figures and fitted models under reports, or F1_OUTPUT_DIR.

## Notebook order

1. Inspect and clean every table, with before/after EDA and integrity checks.
2. Answer the three questions with joins, rates, visualizations and sensitivity checks.
3. Engineer prior-race features and fit preprocessing using training data only.
4. Compare the original models and five additional configurations.
5. Compare feature groups, two preprocessing orders and five planned feature sets.
6. Freeze selections, evaluate the held-out period and demonstrate saved-model inference.
7. Explain the selected model with permutation importance, SHAP and LIME.

Final test evaluation follows the experiments so all settings are fixed first.
The notebook itself retains the milestone's six stage headings.

## Decisions and verified result

Historical repeated driver-race entries use one complete source row: smallest
finishing order, then smallest positive grid, then smallest resultId. Grid,
constructor and finish remain attached to that entry. Detailed rows are preserved.

Training is 2003-2018; validation 2019-2021; test 2022-2024. All eight model settings
are compared across the five planned feature versions. The added constructor-form
and Q1-pace features remain documented trials: validation still selects the
original reduced neural network, with 32/16 hidden units, nine numeric inputs,
eight missing indicators, median filling then scaling, and threshold 0.43.
Validation PR-AUC is 0.7638; test PR-AUC is 0.7078 and test F1 is 0.6730.

The test period was evaluated in the earlier notebook. No test score selects
features, preprocessing, checkpoints, model settings or thresholds in this revision.

Flagged lap/timing values remain unchanged and excluded from predictors; their
accuracy is unresolved. Mechanical-failure rates depend on status assumptions.
LIME's local fit is weak, and both the lab setup and locality trials are disclosed.
XAI describes model reliance, not causation.

## Inference and reproduction

The fitted pipeline, feature schema and threshold are saved together in
reports/models/podium_companion.joblib. The notebook checks reloaded predictions,
complete/partial records, missing markers, zero-grid handling and outcome rejection.
The interface accepts already-engineered pre-race features in original units; it
does not retrieve live data or compute a driver's history from an ID.

The fresh-kernel execution record, analytical PDF, all displayed figures and
result exports are saved locally. Source CSV hashes are checked before and after.
Original notebook and report files were backed up outside the project folder.

## Submission and repository scope

This repository contains the finalized notebook and its environment instructions.
Stage 5 shows both preprocessing orders and each planned feature trial separately;
Question 1 displays common-circuit rank changes with rates and starting counts.

The Kaggle link in the notebook points to an earlier published version. Upload the
current executed notebook to Kaggle, verify its accessible link, and submit the
current analytical PDF with the required links. Publishing code to GitHub does not
update Kaggle or submit the project form.

Notebook0.ipynb remains the only submission notebook. Raw data, the environment,
backups and reports stay excluded from this repository. The partner notebook
and report are preserved.
