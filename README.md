# AI-based Intrusion Detection System (CIC-IDS2017)


## Overview
This project implements a multi-class intrusion detection model using CIC-IDS2017 dataset, focusing on security-oriented feature engineering and handling severe class imbalance in real-world detection scenarios.
### Research Motivation

Network intrusion detection systems(IDS) must detect highly imbalanced and rare attack types in real-world traffic. However, conventional accuracy metrics can be misleading due to severe class imbalance.

This project focuses on:

- Handling extreme class imbalance in intrusion detection
- Evaluating multiclass ROC-AUC (One-vs-Rest)
- Comparing traditional ML and deep learning approaches
- Understading minority attack detection failure cases


## Dataset
- CIC-IDS2017
- 14 attack classes
- severe class imbalance


## Pipeline
EDA -> preprocessing -> sampling -> sklearn baseline -> PyTorch MLP -> evaluation

## Class Distribution analysis

The dataset exhibited severe class imbalance, with several minority classes cnotaining significantly fewer samples than the majority classes.
When using a standard random train-test split, some minority classes were absent in the test set.
This resulted in undefined ROC-AUC values due to mismatches label dimensions during multi-class evaluation.

To address this issue, **stratified train-test splitting** was applied to preserve class distribution across the training and test sets.
This ensured that all classes were represented in the evaluation phase and enabled stable multi-class ROC-AUC computation.

```python
[513705    403  29088   2333  52268   1202   1294   1855      3      9
  35971   1354    375      5    135]
[128426    101   7272    583  13067    300    323    464      1      2
   8993    338     94      2     34]
```

### class counts
```python
     count  ratio (%)
0   513729  80.270156
1      404   0.063125
2    29149   4.554531
3     2379   0.371719
4    52124   8.144375
5     1183   0.184844
6     1307   0.204219
7     1828   0.285625
8        4   0.000625
9        9   0.001406
10   36049   5.632656
11    1316   0.205625
12     374   0.058438
13       5   0.000781
14     140   0.021875
```

### Bar Plot

<img width="400" height="345" alt="image" src="https://github.com/user-attachments/assets/9663a3da-c76d-4f01-be60-8d31c27e9028" />

<img width="400" height="345" alt="image" src="https://github.com/user-attachments/assets/83a97908-8426-4f98-84f6-c08b5da245ba" />

The dataset shows extreme imbalance.

- The benign class accounts for more than 80% of the dataset.
- Several attack classes contain fewer than 100 samples.
- Some classes contain fewer than 30 samples.

This imbalance severely affects macro-level performance and minority attack detection.

## Methodology

- Multiclasss classification
- severe class imbalance handling
- GPU training
- model saving & loading
- ROC-AUC (OVR)


## Models:

(baseline)
- RandomForest
- LogisticRegression
- XGBClassifier
- LGBMClassifier

(PyTorch)
- MLP


## Evaluation Metrics

             precision    recall  f1-score   support

           0       0.98      0.99      0.98    128402
           1       0.00      0.00      0.00       100
           2       0.99      0.97      0.98      7211
           3       0.94      0.95      0.94       537
           4       0.97      0.89      0.93     13211
           5       0.74      0.73      0.74       319
           6       0.91      0.57      0.70       310
           7       1.00      0.47      0.64       491
           8       0.00      0.00      0.00         0
           9       0.00      0.00      0.00         2
          10       0.90      0.92      0.91      8915
          11       0.98      0.57      0.72       376
          12       0.75      0.06      0.12        95
          13       0.00      0.00      0.00         2
          14       0.00      0.00      0.00        29

    accuracy                           0.97    160000   
    macro avg      0.61      0.48      0.51    160000
    weighted avg   0.97      0.97      0.97    160000
    
    [[127075      0     57     30    292     61      4      0      5      0
     865      2      1      0     10]
     [    99      0      0      0      1      0      0      0      0      0
     ...
       0      0      0      0      0]
       [    29      0      0      0      0      0      0      0      0      0
       0      0      0      0      0]]


## Precision-Recall Analysis

<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/1f3f013e-e58b-4da6-a9cd-b4feb0acaf7f" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/02d5938f-b05b-47e5-8f29-f7f3f3a115c5" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/786638dd-ae1e-4616-9bbc-e4c3c0e4c3ca" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/cb89ccee-2648-4b7c-adf3-bf5e3d95090d" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/fdf7b218-bd9e-4fe2-8025-20169743fbc7" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/03dcd62b-f0cf-4424-afbc-1137dfd2b739" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/c556ef04-3083-4a97-adee-f717fd02088e" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/cded829d-c77d-4b66-97a5-208a0ab57824" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/b5b47468-ff05-40e8-9f36-2d316a2a04f8" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/60bca1c3-9bcf-4cb7-bfe8-7471fb1eac8f" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/54a0e673-bd9e-44dc-bb2f-01e0586443f1" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/0a745254-f73b-4b40-9508-8e12588cd116" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/a864ea70-8149-4d82-8610-874e6fd99a7b" />
<img width="250" height="453" alt="image" src="https://github.com/user-attachments/assets/86a10ceb-2675-46d9-94f5-78f66cca7e3f" />

<img width="691" height="545" alt="image" src="https://github.com/user-attachments/assets/cec4f35f-d38d-4bc1-be4a-2fb132843f4f" />

Due to severe class imbalace, ROC-AUC can provide overly optimistic performance estimates. In intrusion detection systems, PR curves are more informative than ROC curves due to extreme calss imbalance.
Therefore, Precision-Recall(PR) curves were evaluate using a one-vs-rest strategy.
PR curves better reflect minority attack detection perfomance.

Result shows:
- Majority classes achieve high AP scores.
- Rare attack classes show near-zero precision-recall performance.
- The model struggles with minority attack detection.



## ROC-AUC Analysis

<img width="691" height="545" alt="image" src="https://github.com/user-attachments/assets/6976c748-173a-4e34-bf3e-336865f749cb" />

To evaluate class separability under severe imbalance, we computed the One-vs-Rest (OVR) ROC-AUC score.

Since the dataset contains 14 attack classes, binary ROC evaluation is not applicable.
Therefore, nulticlass ROC-AUC was conputed using **macro averaging**.

- Multi-class strategy: One-vs-Rest (OVR)
- Averaging method: Macro
- Probability output: Softmax

Macro ROC-AUC score: 

The ROC curves indicate that majority classes show high separability, while minority attack classes exhibit weaker discrimination performance due to severe imbalance.


## Results

### Class Imbalance Analysis

```python
macro avg f1 = 0.51
weighted avg f1 = 0.97
```
The dataset exhibits severe class imbalance.

- Majority class (Benign) dominates the dataset.
- Several attack classes contain fewer than 100 samples.
- Some classes in the test set contain only 2-29 samples.

This leads to:

- High overall  accuracy (97%)
- Poor macro-average performance (macro avg f1 = 0.51)
- Failure to detect rare attack types

### Error Analysis

- The model fails to detect extremely rare attack classes (e.g., class 1, 12, 14).
- Minority classes are frequently misclassified as benign.
- Indicates need for:
  - Class wighting
  - Focal loss
  - Data resampling
  - Cost-sensitive learning
       

## Security Perspective

In practical IDS deployment, failure to detect rare but critical attacks can cause severe damage.
This project highlights the gap between high overall accuracy and real-world security effectiveness.
Macro-f1 and multiclass ROC-AUC were emphasized over simple accuracy metrics.


## Future Work
- Apply class-weighted CrossEntropyLoss
- Implement Focal Loss for rare attack detection
- Exlplore SMOTE / undersampling strategies
- Test Transformer-based architectures
- Evaluate real-time deployment feasibility


## Reproductibility
Environment:

- Python 3.12.10
- Pytorch 2.10.0
- sklearn 1.7.2

Install dependencies:

```bash
pip install -r requirements.txt
```

## commit history
- Initial commit: Add data preprocessing pipeline
- Add sklearn baseline (RandomForest)
- Implement multiclass evaluation metrics
- Fix label-column mismatch error
- Add Pytorch MLP with GPU support
- Implement ROC-AUC (One-vs-Rest)
- Add model saving adn loading

