# RailSense — Indian Railway Punctuality & Delay Analytics

**Project:** RailSense  
**Author:** Divyanshu Singh  
**Domain:** Data Analytics + AI/ML  
**Platform:** Google Colab / Python


# Dataset Link : https://www.kaggle.com/datasets/naijilaji/indian-railways-passenger-train-delays-dataset/
## 1. Project Overview

RailSense is a data analytics and machine learning project for analyzing historical Indian railway train–station punctuality and delay patterns.

The project uses an aggregated train–station delay dataset and applies:

- Data cleaning and quality auditing
- Exploratory Data Analysis (EDA)
- Statistical summaries
- Station-level punctuality analysis
- Train-level delay analysis
- Correlation analysis
- K-Means clustering
- Isolation Forest anomaly detection
- PCA-based cluster visualization

The goal is to identify delay patterns, characterize different punctuality profiles, and detect unusual train–station observations.

> **Important:** The dataset contains aggregated historical train–station statistics. RailSense does **not** claim to predict the exact delay of a future individual train journey.

---

## 2. Objectives

The main objectives are to:

1. Understand the distribution of train delays.
2. Measure right-time and different delay-severity patterns.
3. Identify stations with high and low punctuality in the available sample.
4. Identify train services with higher average delays.
5. Study the relationship between average delay and punctuality indicators.
6. Group train–station observations into meaningful operational profiles using K-Means.
7. Detect unusual observations using Isolation Forest.
8. Produce interpretable visualizations and findings for railway punctuality analytics.

---

## 3. Dataset

The project uses:

`etrain_delays.csv`

The dataset contains approximately 1,900 raw train–station observations and includes fields such as:

- `train_number`
- `train_name`
- `station_code`
- `station_name`
- `average_delay_minutes`
- `pct_right_time`
- `pct_slight_delay`
- `pct_significant_delay`
- `pct_cancelled_unknown`
- `scraped_at`
- `source_url`

### Dataset Quality

The executed analysis found:

- Raw records: **1,900**
- Raw columns: **11**
- Duplicate rows: **0**
- Missing `average_delay_minutes`: **236**
- Negative delay records: **0**
- Percentage components were checked for approximate consistency with 100%.

After cleaning and preparation, **1,664 observations** were used for the main analytical and ML tasks.

The analysis covered:

- **90 unique train numbers**
- **476 unique stations** in the cleaned analytical data

The `source_url` field is retained in the dataset so that the underlying source can be traced.

---

## 4. Delay Severity Categories

For analytical purposes, RailSense defines the following categories:

| Category | Average Delay |
|---|---:|
| On Time | 0 minutes |
| Minor | >0 to 15 minutes |
| Moderate | >15 to 60 minutes |
| Severe | >60 minutes |

These thresholds are **project-defined analytical categories** and are not presented as official Indian Railways classifications.

---

## 5. Methodology

The notebook follows this workflow:

```text
Raw Dataset
     |
     v
Data Audit
     |
     v
Cleaning & Validation
     |
     v
Feature Engineering
     |
     v
Exploratory Data Analysis
     |
     +----------------------+
     |                      |
     v                      v
Station Analysis       Train Analysis
     |                      |
     +----------+-----------+
                |
                v
       Correlation Analysis
                |
                v
        Standardized Features
                |
        +-------+-------+
        |               |
        v               v
     K-Means       Isolation Forest
        |               |
        v               v
    Clusters         Anomalies
        |
        v
     PCA Visualization
        |
        v
   Findings & Insights
```

---

## 6. Data Cleaning & Feature Engineering

The analysis performs:

- Duplicate detection and removal
- Missing-value inspection
- Negative-delay validation
- Percentage consistency checks
- Removal/exclusion of records without usable average-delay values for delay-based analysis
- Creation of delay severity categories
- Creation of a delay-risk score
- Preparation of standardized ML features

The primary ML feature set is:

- Average delay
- Right-time percentage
- Slight-delay percentage
- Significant-delay percentage
- Cancelled/unknown percentage

Features are standardized before clustering and anomaly detection.

---

## 7. Exploratory Data Analysis

The notebook generates visualizations covering:

1. Average-delay distribution
2. Delay-severity distribution
3. Top delayed stations
4. Top right-time stations
5. Top delayed train services
6. Correlation matrix
7. Average delay vs. right-time percentage
8. K-Means silhouette scores
9. PCA cluster visualization
10. Isolation Forest anomaly visualization

These plots are included in the project report.

---

## 8. Key Results

### Overall Delay Profile

For the cleaned analytical dataset:

- Mean average delay: **40.70 minutes**
- Median average delay: **24.00 minutes**
- Maximum observed average delay: **586 minutes**
- Mean right-time percentage: **49.78%**

### Delay Severity

| Severity | Observations | Percentage |
|---|---:|---:|
| On Time | 18 | 1.08% |
| Minor | 491 | 29.51% |
| Moderate | 841 | 50.54% |
| Severe | 314 | 18.87% |

Moderate-delay observations form the largest severity group in the analyzed sample.

---

## 9. Station-Level Findings

Station rankings were calculated using stations with at least **3 observations** to reduce the influence of extremely small samples.

There were **193 stations** meeting this minimum-observation criterion.

Examples of stations appearing among the highest average-delay observations include:

- SLO SAMALKOT JN
- NDD NIDADAVOLU JN
- RJY RAJAMUNDRY
- ANV ANNAVARAM
- TUNI
- AKP ANAKAPALLE
- IPM ICHCHPURAM
- CAP CHATRAPUR
- TEL TENALI JN
- BPP BAPATLA

Examples of stations with high right-time percentages in the analyzed sample include:

- MS CHENNAI EGMORE
- MBM MAMBALAM
- SDAH SEALDAH
- NAD NAGDA JN
- DNR DANAPUR
- TEN TIRUNELVELI JN
- MMCT MUMBAI CENTRAL
- DHN DHANBAD JN
- CBE COIMBATORE JN
- ST SURAT

These rankings describe the available dataset sample and should not be interpreted as nationwide or permanent operational rankings.

---

## 10. Train-Level Findings

Examples of services with high average delays in the analyzed sample include:

| Train | Average Delay |
|---|---:|
| 12261 Howrah Duronto | 370.50 min |
| 12262 Howrah Duronto | 316.83 min |
| 12236 Duronto Express | 148.00 min |
| 12509 Guwahati Sbc Express | 143.19 min |
| 12839 Howrah Mail | 109.37 min |
| 12626 Kerala Express | 101.05 min |
| 12840 Howrah Mail | 100.81 min |
| 12510 Sbc Guwahati Express | 87.97 min |
| 12245 Duronto Express | 78.20 min |
| 12842 Coromandel Express | 65.53 min |

These figures represent the observations available in the dataset rather than a complete operational history of each train.

---

## 11. K-Means Clustering

K-Means was used to discover groups of train–station observations with similar punctuality and delay profiles.

The analysis evaluated cluster counts from **k = 2 to k = 8** using silhouette scores.

| k | Silhouette Score |
|---:|---:|
| 2 | 0.451210 |
| 3 | 0.492545 |
| 4 | **0.516364** |
| 5 | 0.437583 |
| 6 | 0.452481 |
| 7 | 0.449144 |
| 8 | 0.403684 |

The project selected **k = 4** based on the highest silhouette score among the tested values.

The resulting profiles included groups characterized by combinations such as:

- Relatively high punctuality and low delay
- Moderate delay with lower right-time percentage
- High average delay and significant-delay percentage
- Unusual profiles dominated by cancelled/unknown percentages

PCA was used to visualize the resulting clusters in two dimensions.

---

## 12. Isolation Forest Anomaly Detection

Isolation Forest was applied to the same standardized operational features.

Configuration used in the notebook:

- `n_estimators = 300`
- `contamination = "auto"`
- `random_state = 42`

Results:

- Total analytical observations: **1,664**
- Detected anomalies: **239**

In RailSense, an anomaly means that an observation has an unusual combination of delay/punctuality characteristics relative to the analyzed dataset.

An anomaly does **not** automatically mean:

- a data error,
- a railway operational failure, or
- a service disruption.

It should be treated as a candidate for further investigation.

---

## 13. Technologies Used

### Programming

- Python

### Data Analysis

- Pandas
- NumPy

### Visualization

- Matplotlib
- Seaborn

### Machine Learning

- Scikit-learn
  - StandardScaler
  - KMeans
  - silhouette_score
  - PCA
  - IsolationForest

### Development Environment

- Google Colab
- Jupyter Notebook

---

## 14. Project Structure

```text
RailSense/
│
├── DivyanshuSingh_RailSense.ipynb
├── requirements.txt
├── Project Document.docx
├── README.md
└── data/
    └── etrain_delays.csv
```

> The dataset may need to be downloaded separately depending on the submission/repository setup. The notebook expects the dataset file to be available at the path used in the notebook.

---

## 15. How to Run

### Option 1 — Google Colab

1. Open `DivyanshuSingh_RailSense.ipynb` in Google Colab.
2. Upload `etrain_delays.csv` when prompted or place it in the expected working directory.
3. Run the notebook cells from top to bottom.
4. The notebook performs the complete analysis and generates the visualizations and ML results.

### Option 2 — Local Jupyter Environment

Install the required dependencies:

```bash
pip install -r requirements.txt
```

Then launch Jupyter:

```bash
jupyter notebook
```

Open:

```text
DivyanshuSingh_RailSense.ipynb
```

and execute the cells sequentially.

---

## 16. Reproducibility

The notebook uses fixed random states where applicable, including:

```python
random_state = 42
```

This is used for the machine-learning components so that results can be reproduced under the same software/data conditions.

Because the dataset is an external historical dataset, results may differ if the underlying source data is updated or replaced.

---

## 17. Important Limitations

The current dataset does not provide complete operational context such as:

- Weather conditions
- Track congestion
- Signaling conditions
- Maintenance events
- Crew-related factors
- Route-level congestion
- Detailed timetable adherence
- Real-time train movement data
- Holiday/festival effects

Therefore, the project identifies **patterns and profiles**, but does not establish causal explanations for why a train or station experienced a delay.

The dataset is also an aggregated train–station dataset rather than individual journey-level records. Therefore, this project intentionally avoids claiming exact future delay prediction.

---

## 18. Future Scope

RailSense can be extended by integrating:

1. Official Indian Railways timetable data
2. Historical train-level running data
3. Weather and monsoon/fog indicators
4. Route distance and route characteristics
5. Station congestion indicators
6. Holiday and festival calendars
7. Maintenance and operational-event data
8. Real-time train running information
9. Journey-level historical records
10. Supervised delay prediction when suitable journey-level data is available

With richer journey-level data, future versions could evaluate models such as XGBoost, Random Forest, LightGBM, or temporal deep-learning models for delay prediction.

---

## 19. Conclusion

RailSense demonstrates an end-to-end data analytics and AI/ML workflow for Indian railway punctuality analysis.

The project combines data-quality validation, exploratory analysis, visualization, clustering, and anomaly detection to transform historical train–station delay statistics into interpretable operational profiles.

The analysis found substantial variation in delay and punctuality across the available observations. K-Means identified four distinct profiles based on the tested feature set, while Isolation Forest identified observations with unusual combinations of operational characteristics.

The results provide a foundation for a future railway analytics system that incorporates richer operational, environmental, and journey-level data.

---

## 20. Dataset & Source Note

The dataset used in this project is the `etrain_delays.csv` file used by the executed notebook. The dataset contains a `source_url` field that preserves source references associated with the records.

Before publishing the project publicly, the exact dataset page/URL and applicable license or usage terms should be added here and in the project report if required by the internship submission guidelines.

---

## 21. Internship Submission Contents

The RailSense submission package is intended to contain:

```text
DivyanshuSingh_RailSense.ipynb
requirements.txt
Project Document.docx
README.md
```

The notebook contains the executable project workflow, the report documents the methodology and results, `requirements.txt` lists Python dependencies, and this README provides project documentation and execution instructions.

---

## Author

**Divyanshu Singh**  
M.Tech — Software Engineering  
VIT Chennai

**Project:** RailSense — Indian Railway Punctuality & Delay Analytics
