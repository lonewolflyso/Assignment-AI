# CSC2042S Assignment 1 - Perceptron Image Classification

Student: Liso Njena  
Student number: NJNLIS001

## Overview

This repository contains a from-scratch NumPy implementation of a one-vs-rest multi-class perceptron for classifying ten Simpsons characters. Separate grayscale and RGB models are trained, tuned, evaluated, and compared using the Simpsons-MNIST dataset.

The notebook covers:

1. JPEG loading, train-validation splitting, flattening, and normalisation.
2. Object-oriented binary and multi-class perceptrons.
3. Epoch-based training with shuffling and stopping-criterion comparison.
4. Learning-rate and normalisation grid searches for grayscale and RGB.
5. Overall and per-class evaluation with confusion matrices.
6. RGB-versus-grayscale analysis.
7. Brightness and rotation augmentation experiments.
8. Reproducibility and environment documentation.

The perceptron is implemented from scratch. Scikit-learn is used only for the stratified split and evaluation metrics.

## Repository contents

- `NJNLIS001.ipynb` - complete documented implementation, experiments, outputs, and analysis.
- `README.md` - setup, execution, and repository documentation.
- `requirements.txt` - required Python packages.
- `.gitignore` - excludes the dataset, assignment PDF, virtual environments, and generated cache files.
- `report.pdf` - final report to be added before submission.

The required dataset is not included.

## Dataset placement

Download or extract the supplied Simpsons-MNIST dataset locally. The notebook accepts either of these layouts:

```text
Assignment-AI/
└── A2-dataset/
    ├── grayscale/
    │   ├── train/
    │   └── test/
    └── rgb/
        ├── train/
        └── test/
```

or:

```text
Assignment-AI/
└── A2-dataset/
    └── dataset/
        ├── grayscale/
        │   ├── train/
        │   └── test/
        └── rgb/
            ├── train/
            └── test/
```

Each train or test directory must contain the ten character folders supplied with the dataset. The notebook expects 8,000 supplied training images and 2,000 test images for each modality.

## Installation

Python 3.10 or newer is recommended.

Create and activate a virtual environment, then install the dependencies:

### Windows PowerShell

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### macOS or Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Start Jupyter:

```bash
jupyter notebook NJNLIS001.ipynb
```

## Running the experiment

In Jupyter, select **Kernel -> Restart Kernel and Run All Cells**.

The complete run includes:

- 24 hyperparameter-tuning models: 12 grayscale and 12 RGB.
- 15 augmentation models: 5 seeds for each of 3 conditions.

Execution therefore takes several minutes. Do not run a later task in a fresh kernel without first running the earlier cells because later sections reuse trained models and result dictionaries.

## Reproducibility

The notebook uses fixed random seeds:

- Main split and controlled experiments: `42`
- Augmentation generation: `2026`
- Augmentation training orders: `11, 22, 33, 44, 55`

RGB and grayscale use the same train-validation indices. Hyperparameter configurations use the same shuffle sequence. Z-score statistics are fitted using training data only.

## Key results

| Experiment | Result |
|---|---:|
| Best grayscale validation accuracy | 0.2619 |
| Grayscale test accuracy | 0.2265 |
| Best RGB validation accuracy | 0.4275 |
| RGB test accuracy | 0.4285 |
| No augmentation | 0.4244 +/- 0.0118 |
| Brightness augmentation | 0.4210 +/- 0.0112 |
| Rotation augmentation | 0.4146 +/- 0.0090 |

Best grayscale settings: z-score normalisation and learning rate 0.0001.  
Best RGB settings: 0-1 scaling and learning rate 0.0001.

## Submission notes

The final archive must retain the complete `.git` directory and commit history. It must not contain `A2-dataset`, the assignment handout, notebook checkpoint files, virtual environments, or Python cache files.

Before submission, extract a copy of the final `.tar.xz` archive and verify that the notebook, README, requirements file, report, and Git history are present and readable.
