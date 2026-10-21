# ML Network Intrusion Detector

## Project Overview

This project uses machine learning to identify malicious network traffic from normal traffic. It uses the **UNSW-NB15** cybersecurity dataset and compares a Logistic Regression baseline with a Random Forest classifier.

The project is designed as an academic cybersecurity/ML project and demonstrates:

- Network-flow data preprocessing
- Exploratory data analysis
- Binary classification
- Handling categorical and numerical features
- Target-leakage prevention
- Model comparison
- Precision, recall, F1-score and ROC-AUC evaluation
- Confusion-matrix analysis
- Feature-importance analysis
- Saving a reusable ML pipeline

## Dataset

**Official dataset page:**  
https://research.unsw.edu.au/projects/unsw-nb15-dataset

The official UNSW page provides the predefined training and testing partitions:

- `UNSW_NB15_training-set.csv`
- `UNSW_NB15_testing-set.csv`

The official dataset page reports 175,341 records in the training partition and 82,332 in the testing partition.

### Dataset setup

Create this folder structure:

```text
MLNetworkIntrusionDetector/
├── Niveedita_MLNetworkIntrusionDetector.ipynb
├── requirements.txt
├── README.md
├── Niveedita_ProjectReport.docx
└── data/
    ├── UNSW_NB15_training-set.csv
    └── UNSW_NB15_testing-set.csv
```

Download the two CSV files from the official UNSW dataset page and place them in `data/`.

## Technologies Used

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Joblib

## Machine Learning Approach

### Target

`label`

- `0` = Normal traffic
- `1` = Attack traffic

### Excluded fields

The following fields are not used as predictive features:

- `label` — target
- `attack_cat` — directly describes the attack category and would cause target leakage
- `id` — record identifier
- `srcip`, `dstip` — high-cardinality endpoint identifiers
- `stime`, `ltime` — timestamps that can introduce dataset-specific temporal effects

### Models

1. **Logistic Regression**
   - Used as an interpretable baseline
   - Uses balanced class weights

2. **Random Forest**
   - Captures nonlinear relationships and feature interactions
   - Uses balanced subsampling
   - Produces feature-importance estimates

## Evaluation Metrics

The project reports:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix
- ROC curve

F1-score is emphasized because intrusion detection must balance false positives and false negatives.

## Installation

Open a terminal in the project folder:

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Running the Project

Start Jupyter:

```bash
jupyter notebook
```

Open:

```text
Niveedita_MLNetworkIntrusionDetector.ipynb
```

Run the notebook from top to bottom.

The trained model and model comparison results are saved automatically in:

```text
artifacts/
├── best_intrusion_detector.joblib
└── model_results.csv
```

## Expected Output

After execution, the notebook produces:

- Dataset shape and validation information
- Class-distribution analysis
- Model comparison table
- Classification report
- Confusion matrix
- ROC curve
- Random Forest feature-importance chart
- Saved ML pipeline
- Example prediction for a test record

## Reproducibility

A fixed `random_state=42` is used for the machine-learning models. The preprocessing and model are stored together in a single scikit-learn pipeline to ensure consistent inference.

## Limitations

The UNSW-NB15 dataset is a benchmark rather than a complete representation of current enterprise traffic. Performance on this dataset should not be interpreted as guaranteed production IDS performance. A production implementation would require live-traffic validation, concept-drift monitoring, threshold tuning, continuous retraining and additional security controls.

## Academic Reference

Moustafa, N. and Slay, J. (2015). *UNSW-NB15: A Comprehensive Data Set for Network Intrusion Detection Systems (UNSW-NB15 Network Data Set).* Military Communications and Information Systems Conference (MilCIS).

Dataset information and citation guidance are available on the official UNSW dataset page.
