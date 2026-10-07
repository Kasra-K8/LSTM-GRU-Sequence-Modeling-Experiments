# LSTM & GRU Sequence Modeling Experiments

This repository contains a collection of recurrent neural network experiments completed as part of a graduate-level **Deep Learning** course during my M.Sc. studies in Biomedical Engineering at K. N. Toosi University of Technology.

The project explores LSTM and GRU architectures for several sequence-modeling problems, including time-series forecasting, human activity recognition, bidirectional recurrent networks, sequence autoencoding, and ensemble learning.

Several recurrent architectures were implemented manually with **NumPy** to study recurrent state propagation, gating mechanisms, and Backpropagation Through Time (BPTT), rather than relying exclusively on high-level deep-learning APIs.

---

## Project Overview

| Task | Experiment | Application |
|---|---|---|
| Task 2 | LSTM vs GRU | COVID-19 time-series forecasting |
| Task 3 | Stacked LSTM | Human activity recognition |
| Task 4 | Bidirectional LSTM vs GRU | Temperature forecasting |
| Task 5 | LSTM Autoencoder | Signal reconstruction |
| Task 6 | LSTM-GRU Ensemble | ECG signal prediction |

---

## Task 2 — LSTM vs GRU for COVID-19 Time-Series Forecasting

Single-layer **LSTM** and **GRU** models were implemented with NumPy for forecasting daily COVID-19 case data from Iran.

The time series was normalized and converted into 12-step input sequences for predicting a future value three steps ahead.

### Configuration

- Hidden units: 32
- Sequence length: 12
- Prediction horizon: 3 steps
- Optimizer: SGD
- Learning rate: 0.001
- Epochs: 30
- Loss function: Mean Squared Error
- Train/Test split: 80/20

### Submitted Results

| Model | Test MSE |
|---|---:|
| LSTM | 0.028734 |
| GRU | **0.007068** |

The GRU achieved a substantially lower test error in this experiment.

The implementations include recurrent gate calculations and Backpropagation Through Time rather than relying solely on built-in recurrent layers.

---

## Task 3 — Stacked LSTM for Human Activity Recognition

A two-layer **Stacked LSTM** architecture was implemented for human activity recognition using the **HAR70+** dataset.

HAR70+ contains accelerometer recordings from adults over the age of 70 performing several daily activities.

The time-series data was divided into overlapping windows before being passed through two recurrent layers and a final seven-class Softmax classifier.

### Architecture

- LSTM Layer 1: 64 hidden units
- LSTM Layer 2: 32 hidden units
- Time steps: 50
- Step size: 25
- Output classes: 7
- Optimizer: SGD
- Learning rate: 0.005
- Epochs: 5
- Loss function: Cross-Entropy
- Train/Test split: 80/20

This experiment investigates hierarchical temporal feature extraction using stacked recurrent layers.

---

## Task 4 — Bidirectional LSTM and GRU for Temperature Forecasting

Bidirectional LSTM and GRU architectures were investigated for time-series temperature prediction.

Each architecture processes the input sequence in both directions:

- Forward: beginning → end
- Backward: end → beginning

The representations from both directions are concatenated before being used for prediction.

### Configuration

- Hidden units: 32
- Sequence length: 12
- Prediction horizon: 3 steps
- Learning rate: 0.001
- Epochs: 10
- Optimizer: SGD
- Loss function: Mean Squared Error
- Train/Test split: 80/20

### Submitted Results

| Model | Test MSE |
|---|---:|
| Bidirectional LSTM | 0.025726 |
| Bidirectional GRU | **0.015369** |

The Bidirectional GRU produced the lower prediction error in the submitted experiment.

---

## Task 5 — LSTM Autoencoder for Signal Reconstruction

An **LSTM Autoencoder** was developed to investigate representation learning and sequence reconstruction.

A synthetic signal was generated using:

`y(t) = sin(t) + 0.5 cos(2t)`

The model consists of an encoder that compresses the input sequence into a latent representation and a decoder that reconstructs the original signal.

### Architecture

The overall pipeline is:

`Input Sequence → LSTM Encoder → Latent Representation → RepeatVector → LSTM Decoder → TimeDistributed Output`

The encoder learns a compressed representation of the input signal, while the decoder reconstructs the sequence from this representation.

After training, the reconstructed signal closely followed the original synthetic time series.

This experiment demonstrates the use of recurrent neural networks for:

- Sequence compression
- Latent representation learning
- Signal reconstruction
- Autoencoder-based temporal modeling

---

## Task 6 — LSTM-GRU Ensemble for ECG Prediction

An ensemble architecture combining **LSTM** and **GRU** representations was investigated for ECG time-series prediction.

The two recurrent branches process the same input sequence independently. Their predictions are then combined using learnable weighting coefficients.

The ensemble output is formulated as:

`ŷ = α × Output_LSTM + β × Output_GRU`

where `α` and `β` control the relative contribution of each recurrent model.

### Configuration

- LSTM/GRU hidden units: 32
- Time steps: 10
- Prediction horizon: 2 steps
- Learning rate: 0.01
- Epochs: 50
- Optimizer: SGD
- Loss function: Mean Squared Error
- Train/Test split: 80/20

This experiment explores whether complementary temporal representations from different recurrent architectures can be combined for time-series prediction.

---

## Key Concepts Explored

This project covers several important concepts in recurrent deep learning:

- Recurrent Neural Networks
- Long Short-Term Memory Networks
- Gated Recurrent Units
- Backpropagation Through Time
- Stacked Recurrent Networks
- Bidirectional Recurrent Networks
- Time-Series Forecasting
- Sequence Classification
- Human Activity Recognition
- Sequence Autoencoders
- Latent Representation Learning
- Signal Reconstruction
- Ensemble Learning
- ECG Signal Modeling

---

## Repository Structure

```text
.
├── LSTM_GRU_Sequence_Modeling_Experiments.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── report/
    └── Deep_Learning_HW2_Report_FA.pdf
```

---

## Requirements

The main Python packages used in this project are:

```text
numpy
pandas
matplotlib
scikit-learn
tensorflow
openpyxl
```

Install the dependencies using:

```bash
pip install -r requirements.txt
```

---

## Technologies

- Python
- NumPy
- Pandas
- TensorFlow / Keras
- Scikit-learn
- Matplotlib
- LSTM
- GRU
- Bidirectional RNNs
- Stacked RNNs
- Autoencoders
- Backpropagation Through Time
- Time-Series Forecasting
- Ensemble Learning

---

## Academic Context

**Course:** Deep Learning  
**Project Type:** Graduate Course Assignment  
**Program:** M.Sc. Biomedical Engineering  
**University:** K. N. Toosi University of Technology  
**Author:** Kasra Attar Kashani

The complete Persian-language assignment report is available in the `report/` directory.

---

## Data

The datasets used in the original experiments are not included in this repository.

The experiments use data for:

- COVID-19 time-series forecasting
- HAR70+ human activity recognition
- Temperature time-series forecasting
- Synthetic signal reconstruction
- ECG time-series prediction

Dataset paths should be configured locally before running the corresponding notebook sections.

A local directory such as the following can be used:

```text
data/
├── covid_iran.xlsx
├── Temperature Dataset.xlsx
├── ECG Datasets.xlsx
└── har70plus/
```

The `data/` directory is excluded from version control through `.gitignore`.

---

## Notes

This repository was created to document and showcase experimental work completed during a graduate Deep Learning course.

The focus of the assignment was not only model performance, but also understanding the internal operation of recurrent architectures, including gating mechanisms, hidden-state propagation, sequence processing, and gradient-based learning.

The included notebook contains the implementation, experiments, visualizations, and outputs, while the complete Persian-language technical report provides additional mathematical explanations and discussion.
