# Disaster Tweet Classification Benchmark

A reproducible comparison of disaster-related tweet classification methods across CrisisLexT6, CrisisLexT26, and the Kaggle NLP Getting Started dataset.

The notebook compares keyword filtering, fuzzy keyword matching, Bag of Words, TF-IDF with linear models, an active-learning experiment, and RoBERTa fine-tuning.

## Results summary

The saved full-run results identify RoBERTa as the strongest method on all three balanced evaluation splits:

| Dataset | Accuracy |
|---|---:|
| CrisisLexT6 | 94.26% |
| CrisisLexT26 | 83.86% |
| Kaggle disaster tweets | 80.52% |

These results are measured on deliberately balanced splits. They should not be interpreted as performance on each dataset's original class distribution.

## Repository structure

```text
.
├── Disaster_Tweet_Classification_Data_Mining_Project.ipynb
├── data/
│   ├── raw/                 # Three source dataset archives
│   └── SHA256SUMS.txt       # Dataset integrity hashes
└── outputs/notebook_roberta_runs/
    └── */results.json       # Saved full RoBERTa metrics
```

## Setup

Python 3.10 or newer is recommended.

```bash
python -m venv .venv
python -m pip install -r requirements.txt
jupyter lab
```

Open `Disaster_Tweet_Classification_Data_Mining_Project.ipynb` and run it from the repository root.

By default, the notebook loads the supplied RoBERTa metrics rather than repeating several hours of CPU training. Set `RUN_FULL_ROBERTA = True` in the configuration cell to retrain the transformer models.

## Reproducibility notes

- Dataset archives are accessed through relative paths and can be verified with `data/SHA256SUMS.txt`.
- Every dataset uses its own train/test split and model run.
- Saved transformer results record the checkpoint, row counts, hyperparameters, device, runtime, and class-level metrics.
- The stored notebook output now uses portable relative paths.

## Evaluation scope

Balancing makes false positives and false negatives easier to compare, but it changes real-world class prevalence—especially for CrisisLexT26. In addition, random tweet-level splits may share event-specific language between training and testing. Event-grouped evaluation would be required to claim generalization to unseen disasters.

This repository is a structured reproduction and extension of the comparison study discussed in the notebook, not an exact rerun of every experiment in that study.
