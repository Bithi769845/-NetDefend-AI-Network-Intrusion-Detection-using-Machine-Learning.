# 🛡️ NetDefend-AI: Network Intrusion Detection using Machine Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.2%2B-orange.svg)](https://scikit-learn.org/)
[![Imbalanced-Learn](https://img.shields.io/badge/Imbalanced--Learn-0.11%2B-green.svg)](https://imbalanced-learn.org/)
[![License](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)

An advanced Machine Learning pipeline designed for **Network Intrusion Detection System (NIDS)** using the benchmark **NSL-KDD dataset**. This repository demonstrates end-to-end data preprocessing, feature engineering (Correlation, Mutual Information, PCA), handling severe class imbalance with Random Oversampling, and multi-class cyberattack classification.

---

## 📌 Project Overview

Modern computer networks face continuous cyber threats ranging from Denial of Service (DoS) attacks to unauthorized probe scans and root exploits. **NetDefend-AI** evaluates and detects anomalous network behavior by building robust ML models on network connection metrics.

### 🌟 Key Highlights
* **Comprehensive Data Preprocessing**: Automated handling of missing data, duplicate removal, standard scaling of numerical traffic parameters, and label encoding of categorical protocol types (`tcp`, `udp`, `icmp`), network services, and flags.
* **Hybrid Feature Selection**: Combines three feature selection techniques:
  1. **Pearson Correlation Analysis** ($|r| > 0.5$)
  2. **Mutual Information Scoring** (`SelectKBest`)
  3. **Principal Component Analysis (PCA)**
* **Class Imbalance Mitigation**: Utilizes `imbalanced-learn` (`RandomOverSampler`) to balance minority attack classes (`neptune`, `portsweep`, `satan`, etc.) against normal traffic.
* **Multi-Class Attack Classification**: Classifies connection events into normal traffic and specific threat categories.

---

## 📐 Machine Learning Pipeline Architecture

```mermaid
flowchart TD
    A[Raw NSL-KDD Dataset] --> B[Data Preprocessing & Cleaning]
    B --> C[Duplicate Removal & Handling Missing Values]
    C --> D[Standard Scaling & Categorical Label Encoding]
    D --> E[Feature Selection Strategy]
    E --> F1[Correlation Analysis |r| > 0.5]
    E --> F2[Mutual Information SelectKBest]
    E --> F3[Principal Component Analysis PCA]
    F1 --> G[Combined Feature Subset Selection]
    F2 --> G
    F3 --> G
    G --> H[Class Rebalancing via RandomOverSampler]
    H --> I[80/20 Train-Test Dataset Splitting]
    I --> J[Machine Learning Model Training & Evaluation]
```

---

## 📊 Dataset Description: NSL-KDD

The **NSL-KDD dataset** is a refined version of the classic KDD Cup 99 dataset, solving inherent duplication issues to give an unbiased evaluation of intrusion detection algorithms.

* **Total Records Processed**: `132,726` unique network records (after deduplication from 148,517 total records).
* **Total Features**: `41` input attributes + `1` target label column.

### Key Feature Categories:
1. **Basic Traffic Features**: `duration`, `protocol_type`, `service`, `flag`, `src_bytes`, `dst_bytes`, `land`, `wrong_fragment`, `urgent`.
2. **Content Features**: `hot`, `num_failed_logins`, `logged_in`, `num_compromised`, `root_shell`, `su_attempted`, `num_root`, `num_file_creations`, `num_shells`, `num_access_files`, `is_host_login`, `is_guest_login`.
3. **Time-based Network Traffic Features**: `count`, `srv_count`, `serror_rate`, `srv_serror_rate`, `rerror_rate`, `srv_rerror_rate`, `same_srv_rate`, `diff_srv_rate`, `srv_diff_host_rate`.
4. **Host-based Traffic Features**: `dst_host_count`, `dst_host_srv_count`, `dst_host_same_srv_rate`, `dst_host_diff_srv_rate`, etc.
5. **Attack Labels**: `normal`, `neptune`, `portsweep`, `satan`, `ipsweep`, `smurf`, and more.

---

## ⚙️ Installation & Setup

### Prerequisites
* Python 3.8 or higher
* Jupyter Notebook or Google Colab

### Installation Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/NetDefend-AI.git
   cd NetDefend-AI
   ```

2. **Create a Virtual Environment** (Optional but recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Required Packages**:
   ```bash
   pip install pandas numpy scikit-learn imbalanced-learn matplotlib seaborn jupyter
   ```

---

## 🚀 Execution & Usage

1. Open the Jupyter Notebook environment:
   ```bash
   jupyter notebook NSL_KDD.ipynb
   ```
2. Set up dataset file paths inside the notebook (`kdd_train.csv` and `kdd_test.csv`).
3. Run all cells sequentially to view data visualizations, feature selection scores, oversampling pie charts, and model evaluation metrics.

---

## 📂 Project Structure

```text
NetDefend-AI/
├── NSL_KDD.ipynb      # Main Jupyter Notebook containing EDA, preprocessing, ML modeling
├── README.md          # Project Documentation
└── Dataset/           # Directory for NSL-KDD CSV files (kdd_train.csv & kdd_test.csv)
```

---

## 📈 Key Results & Insights

* **Duplicate Removal**: Reduced redundant network records from `148,517` to `132,726` to eliminate training bias.
* **Dimensionality Reduction**: Selected the top 20 most informative features combining correlation, mutual information, and variance ratios.
* **Balanced Target Distribution**: Transformed highly skewed attack distributions into uniform target distributions via `RandomOverSampler` for robust multi-class detection.

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve the models, add new baseline algorithms (e.g., XGBoost, LightGBM, Deep Learning/LSTM), or refine feature engineering:

1. Fork the Project.
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`).
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the Branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

---

