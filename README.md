# A Multi-Source Event Correlation Framework for IAM Security Using Machine Learning and Zero Trust Principles

## Authors

**Md. Mushfiqur Rahman**
Department of System Management and Information Security
Samarkand State University, Samarkand, Uzbekistan
Email: [mushfique98@gmail.com](mailto:mushfique98@gmail.com)

**Hasan-Al-Monsur**
ACNABIN Chartered Accountants
Dhaka, Bangladesh
Email: [hasanalmonsur@gmail.com](mailto:hasanalmonsur@gmail.com)

**Nurmamatov Mekhriddin**
Department of System Management and Information Security
Samarkand State University, Samarkand, Uzbekistan
Email: [mehriddinnur@gmail.com](mailto:mehriddinnur@gmail.com)

**Faisal Reza**
Department of ELP
University of North Carolina, USA
Email: [juristsyndicate@gmail.com](mailto:juristsyndicate@gmail.com)

**Mohammad Shafiqul Islam**
Department of International Relations
University of Dhaka, Dhaka, Bangladesh
Email: [adshafiqul@gmail.com](mailto:adshafiqul@gmail.com)

**Sazzad Hossain**
Department of System Management and Information Security
Samarkand State University, Samarkand, Uzbekistan
Email: [sazzad69@gmail.com](mailto:sazzad69@gmail.com)

\---

# Abstract

Identity and Access Management (IAM) systems generate massive volumes of heterogeneous security events originating from authentication services, email communications, file systems, web activities, and endpoint devices. Traditional security monitoring approaches often analyze these event sources independently, making it difficult to detect sophisticated insider threats and coordinated malicious behaviors.

This repository presents a Multi-Source Event Correlation Framework that combines behavioral analytics, machine learning, and Zero Trust security principles for adaptive IAM protection. The framework preprocesses user activity logs, performs user-centric event aggregation, constructs temporal behavioral sessions through sliding-window segmentation, extracts behavioral features, and estimates threat probabilities using an XGBoost-based classifier. The resulting risk scores are subsequently mapped into Zero Trust access-control decisions that dynamically determine whether access should be allowed, challenged through additional authentication, or denied.

The implementation demonstrates how machine learning and continuous trust evaluation can be integrated to improve insider threat detection and risk-aware access control.

\---

# Key Features

Data preprocessing and normalization

User-based event aggregation

Sliding-window behavioral session construction

Multi-source behavioral feature extraction

XGBoost-based threat probability estimation

Zero Trust risk scoring

Dynamic access-control enforcement

Interactive cybersecurity dashboard

Threat visualization and analytics

Reproducible research implementation

\---

# System Architecture

```text
CERT Dataset
      │
      ▼
Data Preprocessing
      │
      ▼
User Event Aggregation
      │
      ▼
Sliding Window Segmentation
      │
      ▼
Feature Extraction
      │
      ▼
XGBoost Threat Assessment
      │
      ▼
Threat Probability P(u,k)
      │
      ▼
Zero Trust Risk Engine
      │
      ▼
Allow / Challenge / Block
```

\---

# Dataset

## Dataset Source

CERT Insider Threat Dataset

The CERT dataset contains enterprise user activity logs collected from organizational environments, including:

* Email activities
* Authentication events
* File access records
* Device usage logs
* Web browsing activities

The current implementation focuses primarily on email-based behavioral analysis while maintaining compatibility with future multi-source extensions.

\---

## Dataset Statistics

|Parameter|Value|
|-|-|
|Total Records|1,048,575|
|Valid Events After Cleaning|18,628|
|Unique Users|998|
|Observation Period|February 2010 – June 2010|
|Event Source|Email Activities|

\---

# Methodology

## Step 1: Data Preprocessing

Raw activity logs are transformed into standardized event representations:

```text
e = (u, t, a, s)
```

where:

* u = user identifier
* t = timestamp
* a = activity type
* s = event source

### Preprocessing Tasks

* Missing value removal
* Invalid record filtering
* Timestamp conversion
* User identifier normalization
* Event standardization

\---

## Step 2: User-Based Event Aggregation

Events are grouped according to individual users and sorted chronologically to construct behavioral histories.

\---

## Step 3: Sliding Window Segmentation

Temporal behavioral sessions are generated using overlapping windows.

### Parameters

|Parameter|Value|
|-|-|
|Window Length (Tw)|24 Hours|
|Step Size (Δ)|12 Hours|

Window definition:

```text
W(u,k) = {eᵢ | tᵢ ∈ \[kΔ, kΔ + Tw]}
```

\---

## Step 4: Behavioral Feature Extraction

For each behavioral window, a feature vector is constructed:

```text
X(u,k) = \[Fauth, Ffile, Femail, Fweb, Fcorr]
```

### Feature Groups

|Feature|Description|
|-|-|
|Fauth|Authentication behavior features|
|Ffile|File access behavior features|
|Femail|Email communication features|
|Fweb|Web activity features|
|Fcorr|Cross-source correlation features|

### Email Features Used

* Email count
* Off-hour email ratio
* Email activity rate
* Temporal activity patterns

\---

## Step 5: Machine Learning-Based Threat Assessment

An XGBoost classifier estimates the threat probability associated with each behavioral session.

Output:

```text
P(u,k) ∈ \[0,1]
```

where:

* 0 = benign behavior
* 1 = highly suspicious behavior

\---

## Step 6: Zero Trust Risk Scoring

The threat probability is mapped to dynamic trust levels using predefined thresholds.

### Risk Thresholds

```text
τm = Medium-Risk Threshold

τh = High-Risk Threshold
```

### Decision Rules

```text
P(u,k) < τm
        ↓
    Allow Access

τm ≤ P(u,k) < τh
        ↓
Step-Up Authentication

P(u,k) ≥ τh
        ↓
   Block Access
```

\---

# Interactive Dashboard

The repository includes an interactive Gradio-based dashboard for real-time behavioral simulation and Zero Trust decision visualization.

## Dashboard Inputs

* Email Count
* Off-Hour Email Ratio
* Failed Login Count
* File Access Count
* USB Usage Count
* Web Access Count
* Medium-Risk Threshold (τm)
* High-Risk Threshold (τh)

## Dashboard Outputs

* Threat Probability P(u,k)
* Risk Level
* Enforcement Action
* Behavioral Feature Summary
* Risk Gauge Visualization

\---

# Project Structure

```text
IAM-ZeroTrust-Framework/
│
├── README.md
├── requirements.txt
├── LICENSE
│
├── notebooks/
│   └── md\_(1).ipynb
│
├── dataset/
│   └── email.csv
│
├── models/
│   └── MODEL.pkl
│
├── dashboard/
│   └── dashboard.py
│
├── outputs/
│   ├── confusion\_matrix.png
│   ├── threat\_distribution.png
│   └── risk\_analysis.png
│
└── images/
    └── dashboard\_preview.png
```

\---

# Installation

Clone the repository:

```bash
git clone https://github.com/mushfique98/A-Multi-Source-Event-Correlation-Framework-for-IAM-Security.git
```

Move into the project folder:

```bash
cd YOUR\_REPOSITORY
```

Install dependencies:

```bash
pip install -r requirements.txt
```

\---

# Required Libraries

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
xgboost
gradio
pickle
```

\---

# Running the Project

## Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
md\_1.ipynb
```

and execute all cells sequentially.



# Experimental Outputs

The framework generates:

* Threat probability distributions
* Behavioral analytics
* Risk-level distributions
* Zero Trust access decisions
* Confusion matrices
* Security monitoring visualizations

\---

# Reproducibility

All preprocessing scripts, feature extraction procedures, threat scoring methods, Zero Trust decision mechanisms, and dashboard components are included in this repository to facilitate reproducible research and future extensions.

\---

# Future Work

Future enhancements include:

* Full multi-source event integration
* Advanced graph-based correlation analysis
* Deep learning threat detection models
* Federated Zero Trust architectures
* Real-time SIEM integration
* Explainable AI (XAI) support

\---

# Citation

If you use this repository in your research, please cite:

```text
Rahman, M. M., Hasan-Al-Monsur, Mekhriddin, N.,
Reza, F., Islam, M. S., \& Hossain, S.

A Multi-Source Event Correlation Framework for IAM Security
Using Machine Learning and Zero Trust Principles.

2026.
```

\---

# License

This project is released for academic, educational, and research purposes.

\---

# Acknowledgements

The authors acknowledge the CERT Insider Threat Program for providing the dataset used in this research and thank the research community working on Identity and Access Management (IAM), Zero Trust Security, and Insider Threat Detection.

