# Project: Credit Card Fraud Analysis

Credit Card Fraud Analysis leverages exploratory data analysis, visualization, and predictive modeling to uncover fraud patterns and evaluate trade-offs between detecting fraudulent activity and reducing false alerts.

---

## Dataset Content

- **Source:** Synthetic, publicly available on Kaggle: *Credit Card Fraud Dataset*
- **Size:** 1,000,000 transactions (8.7% labeled as fraudulent)
- **Sample Used:** 100,000-row stratified sample (preserves fraud prevalence and feature distributions)
- **Sampling Details:** Row counts, fraud rate, and random seed documented in the ETL notebook; metadata stored in a JSON file.

**Main variables:**
- `distance_from_home`: Distance from customer’s home to transaction location
- `distance_from_last_transaction`: Distance between consecutive transactions
- `ratio_to_median_purchase_price`: Ratio of current transaction to customer’s median purchase size
- `repeat_retailer`: Whether transaction occurred at a previously used retailer
- `used_chip`: Whether a card chip was used
- `used_pin_number`: Whether a PIN was used
- `fraud`: Target variable (1 = fraudulent, 0 = genuine)

---

## Business Rationale

### Problem Statement

Credit card fraud is a global challenge, causing financial loss and stress for victims, and increased costs and reputational risk for financial institutions.

### Business Requirements

Modern fraud prevention relies on machine learning and AI to detect evolving fraud patterns and optimize investigation workflows. The main challenge is balancing recall (catching more fraud) and precision (avoiding false alerts).

- **False negatives:** Direct loss
- **False positives:** Wasted resources, customer dissatisfaction

### Business Goals

- Communicate insights via a dashboard highlighting trade-offs between detecting fraud and minimizing false alerts
- Evaluate model performance using interpretable metrics and threshold tuning
- Demonstrate how analytics inform real-world fraud management strategies

---

## Hypotheses and Tests

| Hypothesis | Test |
|------------|------|
| H1: Fraud increases with greater distance from home | Mann–Whitney U on `distance_from_home` |
| H2: Fraud increases with greater distance from previous transaction | Mann–Whitney U on `distance_from_last_transaction` |
| H3: Fraud increases with higher purchase-price ratio | Mann–Whitney U on `ratio_to_median_purchase_price` (log-transformed) |
| H4: Online orders are more likely to be fraudulent | Chi-Square (`fraud` vs `online_order`) |
| H5: Chip or PIN use reduces fraud likelihood | Chi-Square (`fraud` vs `used_chip` and `used_pin_number`) |
| H6: Fraud likelihood varies by repeat retailer | Chi-Square (`fraud` vs `repeat_retailer`) |
| H7: Threshold tuning shows trade-offs between false positives/negatives | Precision–Recall curve analysis |
| H8: Fraud risk depends on online order and chip use combination | Chi-Square on combined `online_chip_category` |

---

## Project Plan

**Day 1 – Data Understanding and ETL**
- Load, inspect, and clean data in ETL notebook
- Export processed dataset and data dictionary

**Day 2 – Exploratory Data Analysis (EDA)**
- Explore distributions, skew, and correlations
- Use Mann–Whitney U and Chi-Square tests
- Identify features for dashboard storytelling

**Day 3 – Modeling and Evaluation**
- Train Logistic Regression and tree-based models (Decision Tree, Random Forest, Gradient-Boosted Trees)
- Evaluate with Precision, Recall, F1, ROC-AUC, PR-AUC
- Analyze threshold trade-offs

**Day 4 – Dashboard Development (Power BI)**
- Build interactive dashboard with KPIs, filters, and slicers
- Highlight fraud drivers and precision-recall balance

**Day 5 – Review and Documentation**
- Test usability and interpretation
- Finalize README, notebooks, and report

---

## Analysis Techniques

- **EDA:** Descriptive statistics, hypothesis testing, visualization
- **Tests:** Mann–Whitney U (continuous), Chi-Square (categorical), Cliff’s Delta (effect size)

**Key findings:**
- H1: Fraudulent transactions occurred farther from home (p < 0.001, δ = 0.199)
- H2: Greater distance from previous transaction linked to higher fraud risk (p < 0.001, δ = 0.09)
- H3: High purchase-price ratios strongly associated with fraud (p < 0.001, δ = 0.70)
- H4: Online transactions had higher fraud rates (p < 0.001)
- H5: Chip and PIN use reduced fraud frequency (p < 0.001)
- H6: New retailers had marginally higher fraud rate (p < 0.05)
- H7: Lower thresholds increased recall but reduced precision
- H8: Highest fraud rates for online + no chip transactions (p < 0.001)

**Summary:**  
Distance, purchase-price ratio, and online activity are strong fraud predictors. Authentication features (chip, PIN) reduce risk; online transactions without chip use are highest risk.

---

## Dashboard Design

**Power BI dashboard:** Two interactive pages

### 1. Fraud Overview (Decision-Maker View)
- KPI cards: total transactions, incorrect/correct fraud alerts, % false alerts
- Pie chart: % transactions identified as fraud
- Bar charts: fraud rate by purchase type, chip use, purchase-price ratio
- Heat map: distance from home × purchase-price ratio vs fraud rate
- Slicers: purchase type, chip/PIN use, retailer type

### 2. Threshold Analysis (Analyst View)
- Threshold slider: updates precision, recall, false-alert rate, missed-fraud count
- KPI cards: totals for transactions and frauds
- Bar charts: fraud rate by PIN use, online/in-person, chip use, distance, purchase-price ratio
- Shared slicers for filtering

**Design considerations:**  
Focus on interpretability and interactivity. Dataset is synthetic (no cost/time variables), so cost-impact or time-series visuals are not included. Wireframes are in the wireframes folder.

---

## Modeling and Evaluation

- **Models:** Logistic Regression (baseline), Decision Tree (class-weighted), Random Forest, Gradient-Boosted Trees
- **Metrics:** Precision, Recall, F1, ROC-AUC, PR-AUC
- **Threshold tuning:** Central to analysis; lower thresholds increase recall but cause more false alerts

**Workflow:**  
Reproducible ETL, statistical EDA, and model evaluation produce actionable insights for the dashboard.

---

## Main Data Analysis Libraries

| Library / Module                       | Purpose / Use in Project                                                                                      |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------|
| `sklearn.model_selection`              | Splitting data (train/test/validation), parameter tuning (`train_test_split`, `GridSearchCV`)                 |
| `sklearn.metrics`                      | Calculating evaluation metrics (precision, recall, F1, ROC-AUC, PR-AUC), confusion matrix visualization       |
| `sklearn.linear_model.LogisticRegression` | Baseline interpretable classifier for comparison                                                            |
| `sklearn.tree.DecisionTreeClassifier`  | Simple, transparent model to explore decision boundaries and feature splits                                   |
| `sklearn.ensemble.RandomForestClassifier` | Ensemble model for non-linear relationships and predictive stability                                        |
| `sklearn.ensemble.GradientBoostingClassifier` | Gradient boosting ensemble for accuracy and bias-variance control                                      |
| `xgboost.XGBClassifier`                | High-performance gradient boosting for advanced modeling                                                      |
| `imblearn.over_sampling.SMOTE`         | Synthetic Minority Oversampling Technique for handling class imbalance                                        |
| `matplotlib.pyplot`                    | Plotting evaluation curves (Precision–Recall, ROC, threshold visualizations)                                  |

---

## Dataset Selection and Limitations

**Rationale:**  
The European Credit Card Fraud dataset (2013) was rejected due to low fraud rate (0.17%) and PCA-transformed features. The Kaggle synthetic dataset was chosen for its:
- Manageable 8.7% fraud rate
- Interpretable features
- No need for GitHub LFS or large-file handling

**Limitations:**
- Models perform unrealistically well due to data simplicity
- No transaction amounts, timestamps, or cost data
- No monetary/time context for loss or fraud timing
- Limited cost–benefit or time-trend analysis

---
# Project File Structure

CREDIT-CARD-FRAUD-ANALYSIS/
│
├── .venv/                              # Virtual environment (excluded from Git)
│
├── Dashboard/                          # Final Power BI dashboard
│   └── Credit-Card-Analysis-Dashboard.pbix
│
├── data/                               # Datasets used for ETL, EDA, and modelling
│   ├── processed/                      # Cleaned and transformed dataset
│   │   └── card_transdata_processed.csv
│   └── raw/                            # Original dataset and metadata
│       ├── card_transdata_sample_100k.csv
│       └── sample_log.json
│
├── jupyter_notebooks/                  # Project notebooks for each stage
│   ├── 01_ETL.ipynb                    # Data extraction, cleaning, and transformation
│   ├── 02_EDA.ipynb                    # Exploratory data analysis and hypothesis testing
│   └── 03_Modelling.ipynb              # Model training, evaluation, and threshold tuning
│
├── reports/                            # Model output and comparison CSVs
│   ├── balance_model_comparison.csv
│   ├── balance_model_detailed_comparison_t70.csv
│   ├── balance_threshold_comparison.csv
│   ├── logit_test_thresholds.csv
│   ├── logit_test_thresholds_detailed.csv
│   ├── logit_thresholds_test_detailed.csv
│   ├── test_model_compare.csv
│   └── tree_test_thresholds.csv
│
├── Wireframe/                          # Dashboard layout drafts created in Balsamiq
│   ├── Balsamiq_Dashbboard_Report_Page_1.jpg
│   └── Balasmic_Dashboard_Report_Page_2.jpg
│
├── requirements.txt                    # Python library dependencies
├── setup.sh                            # Deployment setup script
├── Procfile                            # Heroku deployment configuration
├── .gitignore                          # Files excluded from version control
├── .python-version                     # Python version information
├── .slugignore                         # Files excluded from deployment build
└── README.md                           # Project documentation



**Notes:**
- The Dasboard folder contains the final .pbix Power BI report file.
- The Wireframe folder stores exported Balsamiq images showing early dashboard design drafts.
- The reports folder holds all model and threshold comparison outputs used in Power BI and documentation.

## Future Directions

- Dashboard supports future cost-based analysis
- With real data, users could estimate costs per false positive/missed fraud
- Industry reports highlight high false positive workload, reinforcing need for balanced detection

---

## Ethical Considerations

- **Privacy:** Dataset is synthetic; no personal data. Real data would require GDPR compliance.
- **Fairness & Accountability:** Automated detection balanced with human review for fairness.
- **Transparency:** Models are decision-support tools; thresholds and metrics are documented and visualized.

---

## Deployment

- Delivered as a Power BI dashboard (`Capstone_FraudDashboard.pbix`), and in Jupyter Notebooks (pleasee file structure secytion)
- All visuals link to processed dataset.

## Challenges and Limitations

### Technical Challenges

- **Environment setup:**  
    Initial issues with VS Code not activating the virtual environment led to import errors (e.g., `No module named numpy`). This was resolved by reinstalling dependencies directly into the active Jupyter kernel using `%pip install -r requirements.txt`, with guidance from my project tutor.

- **Seaborn compatibility:**  
    The latest Seaborn version deprecated using color palettes without a defined `hue`. This caused repeated `FutureWarning` messages. The issue was fixed by specifying `hue=` and `legend=False` in plot functions, based on troubleshooting with Copilot.

- **Dashboard integration:**  
    Limitation creating visuals without time and cost reakationships to fraud.

### Dataset and Modeling Limitations

- The synthetic dataset’s clear class separation led to inflated model performance compared to real-world scenarios.
- Absence of cost and time-based features limited the ability to analyze business impacts, such as comparing fraud-loss costs with false-alert investigation costs.
- Simplified feature design reduced the complexity of relationships, making the data less representative of real fraud detection challenges.

Despite these constraints, the dataset enabled a full demonstration of the fraud analytics workflow (from ETL and EDA through modeling and dashboard delivery)while highlighting practical challenges encountered in real-world fraud detection projects.

## Project Summary

This project investigates how to detect credit card fraud while balancing operational risks, false alerts, and investigation costs. By tuning model thresholds and evaluating precision–recall trade-offs, it demonstrates how machine learning can support more effective, cost-aware fraud management. While the synthetic dataset limits analysis of real-world financial and time-based patterns, it enables a practical demonstration of analytics workflows and dashboard design for fraud detection in a capstone context.

## Credits

**Fraud Research and Business Context**
- FICO (2023). Credit Card Fraud Detection: 2025 Trends and Interventions
- Soto-Valero, C. (2023). Evaluation Metrics for Real-Time Financial Fraud Detection ML Models
- Alon, T. (2023). Ultimate Guide to PR-AUC: Calculations, Uses, and Limitations (Coralogix Blog)
- Sahoo et al. (2023). Data Leakage and Deceptive Performance in Credit Card Fraud Detection (arXiv preprint)
- NICE Actimize (2024). Reducing False Positives in Transaction Monitoring
- J.P. Morgan (n.d.). False Positives & Fraud Prevention Tools

**Acknowledgements**
- Tutor: Vasi Pavaloi (coding and project guidance)
- ChatGPT and GitHub Copilot (debugging, code refinement, documentation)
- Code Institute LMS documentation (structure and best practices)

- The text for the Home page was taken from Wikipedia Article A
- Instructions on how to implement form validation on the Sign-Up page was taken from [Specific YouTube Tutorial](https://www.youtube.com/)
- The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)
