# Construction PM Risk Analytics

This project evaluates whether task metadata available at creation time can identify elevated overdue risk.

## Run the validated pipeline

```powershell
python -m venv _env
._env\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook
```

Run the notebooks in numerical order: cleaning, feature engineering, risk labeling, model training, then model evaluation. They regenerate the processed data, model, metrics, and predictions without changing the project folder layout.

Its safeguards are deliberate:

- One latest record per `Ref` is retained before splitting, preventing the same task from appearing in training and test data.
- The holdout is chronological: tasks created in the final 20% of the timeline are never used to fit the model.
- Workload features use only records earlier than the task date. Target-derived package-risk features are excluded because this snapshot lacks a valid historical outcome-event table.
- Predicted probabilities are calibrated on a separate later segment of the training period; the decision threshold is selected there, not on the holdout.
- Results report ROC-AUC, average precision, Brier score, precision, recall, and F1. Accuracy is intentionally not a primary claim for this imbalanced outcome.

The model-training and evaluation notebooks use a chronological holdout. Do not use outputs from an earlier random-split run for reporting; regenerate artefacts in `results/` after running the notebooks.

## Scope and interpretation

The outcome is the source system's recorded overdue state. Results measure association and prioritisation quality, not causal effects. The recommended operating threshold must be rechecked whenever the project mix or time period changes.
