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

| Class                      | Precision | Recall | F1-Score | Support |
| -------------------------- | --------- | ------ | -------- | ------- |
| DoS Hulk                   | 1.00      | 0.99   | 1.00     | 200     |
| PortScan                   | 0.99      | 0.99   | 0.99     | 200     |
| DDoS                       | 1.00      | 1.00   | 1.00     | 200     |
| DoS GoldenEye              | 0.76      | 1.00   | 0.86     | 200     |
| FTP-Patator                | 1.00      | 0.99   | 1.00     | 200     |
| SSH-Patator                | 1.00      | 1.00   | 1.00     | 200     |
| DoS slowloris              | 1.00      | 1.00   | 1.00     | 200     |
| DoS Slowhttptest           | 1.00      | 0.99   | 1.00     | 200     |
| Bot                        | 1.00      | 0.99   | 1.00     | 200     |
| Web Attack – Brute Force   | 0.94      | 0.15   | 0.26     | 200     |
| Web Attack – XSS           | 0.56      | 0.98   | 0.71     | 200     |
| Infiltration               | 1.00      | 1.00   | 1.00     | 200     |
| Web Attack – SQL Injection | 0.92      | 0.71   | 0.80     | 200     |
| Heartbleed                 | 1.00      | 1.00   | 1.00     | 200     |
|                            |           |        |          |         |
| **Accuracy**               |           |        | 0.92     | 2800    |
| **Macro Avg**              | 0.94      | 0.92   | 0.90     | 2800    |
| **Weighted Avg**           | 0.94      | 0.92   | 0.90     | 2800    |

### 2. Focussing on DOS attacks

Classification Report:

| Class            | Precision | Recall | F1-Score | Support |
| ---------------- | --------- | ------ | -------- | ------- |
| DoS Hulk         | 0.99      | 0.99   | 0.99     | 200     |
| Others           | 0.98      | 0.99   | 0.99     | 200     |
| DDoS             | 1.00      | 0.99   | 1.00     | 200     |
| DoS GoldenEye    | 1.00      | 1.00   | 1.00     | 200     |
| DoS slowloris    | 0.99      | 0.98   | 0.98     | 200     |
| DoS Slowhttptest | 0.99      | 0.99   | 0.99     | 200     |
|                  |           |        |          |         |
| **Accuracy**     |           |        | 0.99     | 1200    |
| **Macro Avg**    | 0.99      | 0.99   | 0.99     | 1200    |
| **Weighted Avg** | 0.99      | 0.99   | 0.99     | 1200    |

### 3. Focussing on WebAttack attacks

Accuracy: 0.7662
F1 Score: 0.7294

Classification Report:

| Class                      | Precision | Recall | F1-Score | Support |
| -------------------------- | --------- | ------ | -------- | ------- |
| Others                     | 1.00      | 0.99   | 0.99     | 200     |
| Web Attack – Brute Force   | 0.64      | 0.18   | 0.28     | 200     |
| Web Attack – XSS           | 0.54      | 0.90   | 0.67     | 200     |
| Web Attack – SQL Injection | 0.94      | 1.00   | 0.97     | 200     |
|                            |           |        |          |         |
| **Accuracy**               |           |        | 0.77     | 800     |
| **Macro Avg**              | 0.78      | 0.77   | 0.73     | 800     |
| **Weighted Avg**           | 0.78      | 0.77   | 0.73     | 800     |

## Findings

1. The model where we train on all attacks performs pretty well. It won't be applicable in an NIDS though, because it's only got a 92% accuracy, and a 90% macro average accuracy. The model is not able to detect attacks with small samples.

2. The model where we focus on DOS attacks performs very good. It has a 99% accuracy, and a 99% macro average accuracy. This model is very good at detecting DOS attacks, and also performs well on detecting "Others".

3. The model where we focus on WebAttack attacks performs the worst. It has a 77% accuracy, and a 73% macro average accuracy. This model is not able to detect WebAttack attacks very well, but it can detect "Others" quite well.

### Focus on DoS

Here is the direct comparison of the evaluation of DoS attacks in either the first model or the model where we focus on DoS attacks.

#### DoS Hulk

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 237, 38)">Equal</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 1.00      | 0.99   | 1.00     | 200     |
| DoS   | 0.99      | 0.99   | 0.99     | 200     |

#### DDos

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 237, 38)">Equal</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 1.00      | 1.00   | 1.00     | 200     |
| DoS   | 1.00      | 0.99   | 1.00     | 200     |

#### DoS GoldenEye

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(38, 255, 38)">Better</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 0.76      | 1.00   | 0.86     | 200     |
| DoS   | 1.00      | 1.00   | 1.00     | 200     |

#### DoS slowloris

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 237, 38)">Equal</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 1.00      | 1.00   | 1.00     | 200     |
| DoS   | 0.99      | 0.98   | 0.98     | 200     |

#### DoS Slowhttptest

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 237, 38)">Equal</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 1.00      | 0.99   | 1.00     | 200     |
| DoS   | 0.99      | 0.99   | 0.99     | 200     |

### Focus on WebAttack

Here is the direct comparison of the evaluation of WebAttack attacks in either the first model or the model where we focus on WebAttack attacks.

#### Web Attack – Brute Force

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 71, 38)">Worse</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 0.94      | 0.15   | 0.26     | 200     |
| Web   | 0.64      | 0.18   | 0.28     | 200     |

#### Web Attack – XSS

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(255, 237, 38)">Equally bad</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 0.56      | 0.98   | 0.71     | 200     |
| Web   | 0.54      | 0.90   | 0.67     | 200     |

#### Web Attack – SQL Injection

<!-- markdownlint-disable MD033 -->
<p style="font-weight: bold;">Performance: <span style="color:rgb(38, 255, 38)">Better</span></p>

| Model | Precision | Recall | F1-Score | Support |
| ----- | --------- | ------ | -------- | ------- |
| All   | 0.92      | 0.71   | 0.80     | 200     |
| Web   | 0.94      | 1.00   | 0.97     | 200     |
