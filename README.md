# ML-RankAttack: Machine Learning-Based Detection of Rank Attacks in RPL-Based IoT Networks

This project implements a machine learning pipeline for detecting **Rank Attacks** in **RPL-based IoT networks**, where malicious nodes manipulate rank values to disrupt routing.

## Project Overview

In **RPL (Routing Protocol for Low-Power and Lossy Networks)**, a Rank Attack is a severe threat that misguides the routing process. This project explores **supervised and unsupervised** machine learning techniques to detect such attacks using network traffic features.

## Author

**Haiqa Javed**
* Student ID: i211578
* Course: CS4111 - Applied Machine Learning for Cyber Security
* Submission Date: May 3, 2025

## Dataset

* File: `Rank.csv`
* Features extracted from simulated RPL network traffic.
* Label: `PCKT_LABEL`

  * `0`: Normal packet
  * `1`: Malicious (Rank Attack)

## Data Preprocessing

* Dropped 38 irrelevant columns (IDs, IPs, timestamps).
* Removed duplicates and handled missing values:

  * Critical labels were dropped if missing.
  * Filled categorical nulls with `'UNKNOWN'`.
  * Numerical nulls (e.g., `RPL_VERSION`) filled with `-1`.
* Categorical features encoded using `pandas.factorize()`.

## Exploratory Data Analysis

* Notable **class imbalance** observed:

  * Majority: Normal traffic
  * Minority: Rank attack

## Supervised Learning Models

### Baseline: Random Forest (Original Data)

* High accuracy, but overfit to normal class.

### Random Forest (Shuffled)

* Improved generalization, but minority class still underrepresented.

### Random Forest + SMOTE

* Used **Synthetic Minority Oversampling Technique**.
* Achieved perfect recall and F1-score for attack class.

## Unsupervised Learning Approaches

### One-Class SVM

* Trained only on normal data.
* Achieved perfect **recall** but low **precision** (good for anomaly detection).

### KMeans Clustering

* Automatically grouped data.
* Demonstrated good separation between normal and attack classes.

## Results Summary

| Method                   | Accuracy | Precision | Recall | F1-Score | Notes                       |
| ------------------------ | -------- | --------- | ------ | -------- | --------------------------- |
| Random Forest (Original) | 1.00     | 1.00      | 1.00   | 1.00     | Overfit on majority class   |
| Random Forest (Shuffled) | 0.24     | 0.30      | 0.23   | 0.26     | Poor recall for attacks     |
| RF + SMOTE               | 1.00     | 1.00      | 1.00   | 1.00     | Balanced performance        |
| One-Class SVM            | 0.94     | 0.17      | 1.00   | 0.30     | Best recall, weak precision |
| KMeans Clustering        | 0.90     | 0.85      | 0.90   | 0.88     | Strong unsupervised results |


## Conclusion

This project presents a **robust ML pipeline** for Rank Attack detection in RPL-based IoT environments. While **supervised learning** with SMOTE achieved the best overall results, **unsupervised methods** like One-Class SVM and KMeans are promising for real-world scenarios with unlabeled data.
