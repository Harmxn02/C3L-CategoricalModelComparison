# C3L - Categorical Model Comparison

This repository contains the code to compare several training techniques for a NIDS. The techniques are:

1. Training a model on only attack data
1. Training a model where we focus on DOS attacks, and combine all other attacks into one class
1. Training a model where we focus on WebAttack attacks, and combine all other attacks into one class

## Data

The data used in this project is the [CICIDS 2017 dataset](https://www.unb.ca/cic/datasets/ids-2017.html).

## Comparison

The models are trained using the following the **Hybrid CNN-GAN model** architecture.

We compare the models using the following metrics:

1. Accuracy (per class)
1. Precision (per class)
1. Recall (per class)
1. F1 Score (per class)

And we do that by creating a classification report for each model.

## Results

### 1. Only attacks

### 2. Only DOS attacks

### 3. Only WebAttack attacks
