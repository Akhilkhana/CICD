# Iris ML Model Training CI/CD

A CI/CD pipeline for training and evaluating machine learning models on the classic Iris dataset, using GitHub Actions, CML (Continuous Machine Learning), and scikit-learn.

## What It Does

Every time code is pushed to `main` or a pull request is opened, the pipeline automatically:

1. Sets up a clean Python environment
2. Installs all dependencies
3. Trains a **Logistic Regression** and a **Random Forest Classifier** on the Iris dataset
4. Evaluates both models (accuracy, F1, precision, recall)
5. Generates a **Confusion Matrix** and **Feature Importance** plot
6. Posts a CML report with scores and plots as a pull request comment
7. Uploads plots and scores as workflow artifacts

## Models

| Model | Notes |
|---|---|
| Logistic Regression | C=0.0001, lbfgs solver, multinomial |
| Random Forest Classifier | 100 estimators, random_state=44 |

Both models are trained on 6 features: the 4 original Iris measurements plus two engineered ratio features (sepal and petal length/width ratios).

## Tech Stack

| Layer | Tool |
|---|---|
| Language | Python 3.10 |
| ML | scikit-learn |
| Data | pandas, numpy |
| Visualisation | matplotlib, seaborn |
| CI/CD | GitHub Actions |
| ML Reporting | CML (Continuous Machine Learning) |

## Project Structure

```
CICD/
├── .github/
│   └── workflows/
│       └── run.yaml       # GitHub Actions CI/CD pipeline
├── iris.csv               # Iris dataset
├── train_model.py         # Model training, evaluation, and plot generation
├── requirements.txt       # Python dependencies
└── README.md
```

## CI/CD Pipeline Overview

```
push / pull_request → main
        │
        ▼
  Checkout repo
        │
        ▼
  Set up Python 3.10
        │
        ▼
  pip install -r requirements.txt
        │
        ▼
  python train_model.py
  ├── trains LogReg + RandomForest
  ├── saves scores.txt
  ├── saves ConfusionMatrix.png
  └── saves FeatureImportance.png
        │
        ▼
  CML posts report as PR comment
        │
        ▼
  Upload artifacts (scores, plots)
```

## Running Locally

1. **Clone the repository**

```bash
git clone https://github.com/Akhilkhana/CICD.git
cd CICD
```

2. **Install dependencies**

```bash
pip install -r requirements.txt
```

3. **Train the models**

```bash
python train_model.py
```

Outputs: `scores.txt`, `ConfusionMatrix.png`, `FeatureImportance.png`

## Output Files

| File | Description |
|---|---|
| `scores.txt` | Train/test accuracy, F1, recall, precision for both models |
| `ConfusionMatrix.png` | Normalized confusion matrix for Logistic Regression |
| `FeatureImportance.png` | Feature importance bar chart from Random Forest |

## License

This project is open source. See [LICENSE](LICENSE) for details.
