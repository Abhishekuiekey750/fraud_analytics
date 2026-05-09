# Banking Transaction Fraud Analytics

**Data Analytics | Fraud Detection | Exploratory Analysis**

A hands-on analytics project where I work with a public banking-style transaction dataset to understand fraud risk signals, clean and explore the data, build simple risk indicators, and summarize findings in a way a business team could use for follow-up review.

---

## Short project overview

This project follows a practical analytics workflow: load transaction-level data, fix data quality issues, explore patterns that often matter in fraud (amount, channel, location, login behavior), and turn those patterns into clear takeaways. The focus is on **sound analysis and communication**, not on claiming a production-ready fraud engine.

## Business problem statement

Banks and payment teams need to spot **unusual activity** early—before large losses or customer harm. Fraud is often rare and hidden inside normal traffic, so teams rely on **rules, profiles, and reviews** guided by data. The problem here is: *What does “suspicious” look like in this dataset, and which accounts or transactions deserve a closer look?*

## Objective of the project

- Clean and document the transaction data for analysis.  
- Explore relationships between transaction attributes and **anomaly-style flags** (for example, high-value activity, location changes, or concentrated activity on an account).  
- Summarize **KPIs and charts** that support fraud operations or risk discussions.  
- Practice explaining results in **plain language** for recruiters and interview practice.

---

## Dataset information

| Item | Details |
|------|---------|
| **Source** | [Bank Transaction Dataset for Fraud Detection](https://www.kaggle.com/datasets/valakhorasani/bank-transaction-dataset-for-fraud-detection) (Kaggle) |
| **Type of data** | Tabular transaction records (one row per transaction) with customer and channel context |
| **Size (approx.)** | ~2,500 rows in the raw CSV shipped with this repo (small, learning-friendly sample) |
| **Stored files** | `bank_transactions_data_2.csv` (raw), `data_cleaned.csv` (cleaned export used in the R script) |

**Important columns / features (examples)**  
`TransactionID`, `AccountID`, `TransactionAmount`, `TransactionDate`, `TransactionType`, `Location`, `DeviceID`, `IP Address`, `MerchantID`, `Channel`, `CustomerAge`, `CustomerOccupation`, `TransactionDuration`, `LoginAttempts`, `AccountBalance`, `PreviousTransactionDate`

**Engineered fields in the notebook (examples)**  
Ratio of transaction amount to balance, flags for high-value transactions (e.g., above a chosen percentile), and other derived variables used to study unusual behavior.

---

## Technologies used

Tools are grouped by how they show up in this portfolio piece versus what I also use in a typical analyst workflow.

**Used directly in this repository**

- **Python** — data loading, cleaning, feature ideas, and analysis in a notebook  
- **Pandas** — filtering, grouping, missing-value checks, derived columns  
- **Jupyter Notebook** — `fraud-prediction-and-modeling.ipynb`  
- **R** — additional exploration and charts in `data-visualization.R`  
- **ggplot2**, **dplyr**, **lubridate**, **psych** — plotting, data manipulation, dates, simple summaries  

**Common analyst stack I align with (and use in coursework / parallel practice)**

- **NumPy** — numeric operations alongside Python workflows  
- **Matplotlib** / **Seaborn** — standard Python plotting options for EDA  
- **SQL** — how transactional data is usually stored; the same logic appears here as filters and aggregations  
- **Excel** — quick checks on exports and small tables  
- **Power BI / Tableau** — dashboard-style reporting in other settings; this repo emphasizes notebook + R visuals and a short strategy deck PDF  

---

## Project workflow

1. **Data collection** — Download the dataset from Kaggle (API or manual download), keep a clear raw copy (`bank_transactions_data_2.csv`).  
2. **Data cleaning** — Handle missing fields, parse dates, drop or adjust columns that are not needed, and validate basics (for example, non-positive amounts).  
3. **Exploratory Data Analysis (EDA)** — Distributions, counts by channel and location, activity per account, and checks for odd combinations of fields.  
4. **KPI analysis** — Simple operational-style metrics: transactions per account, share of high-value transactions, flags for rapid location change, or repeated login-related patterns (as defined in the code).  
5. **Visualization / dashboard-style outputs** — Charts in R (ggplot2) and the notebook narrative; a PDF deck summarizes strategy-style messaging for stakeholders (`fraud-strategy-and-analytics-deck-AY.pdf`).  
6. **Business insights generation** — Translate patterns into **plain-language** risks and monitoring ideas (what to watch weekly, what to send to review).

---

## Key insights

*(Findings are illustrative of the analysis approach; exact numbers change if you alter thresholds in the code.)*

- **Account concentration** — A small number of accounts can drive a large share of activity; monitoring “busy” profiles is a practical starting point for review queues.  
- **Amount vs. balance** — Very large transactions relative to account balance can be a simple risk signal worth pairing with channel and device context.  
- **Location and timing** — Back-to-back transactions in different locations within a short window can be flagged for manual follow-up (rule-based, easy to explain to non-technical stakeholders).  
- **Channel mix** — Online vs. ATM vs. other channels may show different behavior; splitting metrics by channel keeps alerts more meaningful.  
- **Data limitations** — The sample is modest in size and synthetic-style; results are best framed as **learning outcomes and methods**, not live fraud rates for a real bank.

---

## Dashboard / visualizations

- **Histograms and bar charts** — Login-frequency style views and location-pattern charts (see `data-visualization.R`).  
- **Ranked bar plots** — Highlighting accounts with many short-interval location jumps (a straightforward “anomaly shortlist” idea).  
- **Notebook tables and printed summaries** — Step-by-step EDA and KPI tables inside `fraud-prediction-and-modeling.ipynb`.  
- **Strategy deck (PDF)** — High-level storyline for impact and next steps; useful in interviews to show you can connect analysis to decisions.

---

## Business impact

This type of analysis helps teams **prioritize reviews**, **tune simple rules**, and **explain risk** to partners in operations or compliance. Even without a machine learning model, clear cuts (high value, odd geography, unusual velocity) can reduce wasted investigation time and surface cases that need human judgment.

---

## Folder structure

```text
fraud-analytics/
├── README.md
├── bank_transactions_data_2.csv      # Raw transaction data (Kaggle extract)
├── data_cleaned.csv                  # Cleaned data used by the R visualization script
├── fraud-prediction-and-modeling.ipynb
├── data-visualization.R
└── fraud-strategy-and-analytics-deck-AY.pdf
```

---

## How to run the project

### Prerequisites

- **Python 3.x** with `pip`  
- **Jupyter** (e.g., `pip install notebook` or use VS Code / Cursor Jupyter support)  
- **R + RStudio** (optional, for the `.R` script)  
- **Kaggle account** (if you re-download the data yourself)

### Python / Jupyter

1. Create a virtual environment (recommended).  
2. Install dependencies you need to run the notebook (at minimum: `pandas`; add `numpy`, `matplotlib`, or `seaborn` if you extend the plots).  
3. Open `fraud-prediction-and-modeling.ipynb` and run cells from top to bottom.  
4. If the notebook references Kaggle download steps, add your Kaggle API token as Kaggle’s documentation describes, or place the CSV files in the project folder manually.

### R script

1. Open `data-visualization.R` in RStudio.  
2. Ensure `data_cleaned.csv` sits in the same working directory as the script (or update the path).  
3. Install required packages if prompted: `dplyr`, `ggplot2`, `psych`, `lubridate`, `rstudioapi` (for the default `setwd` line).  
4. Run the script section by section to reproduce plots.

### Note on file paths

The R file uses `rstudioapi` to set the working directory to the script location. If you run R from the command line, set the working directory manually to the folder that contains `data_cleaned.csv`.

---

## Future improvements

- Add **reproducible `requirements.txt`** (and optional `environment.yml`) with pinned versions.  
- Expand **Python visualizations** (Matplotlib/Seaborn) next to the R charts for one consistent toolchain.  
- Try a simple **baseline classifier** with clear metrics (precision/recall at a fixed alert budget) if a stable fraud label exists in a future version of the data.  
- Build a small **SQL appendix** with example queries that mirror the notebook’s group-by logic.  
- Optional **Power BI or Tableau** workbook that reads the cleaned CSV for a click-through demo.

---

## Learning outcomes

- Practiced an end-to-end **analytics workflow** from raw file to insight.  
- Strengthened **Pandas** skills for cleaning, feature ideas, and aggregation.  
- Used **R + ggplot2** for communication-focused charts.  
- Learned to **state limitations** honestly (sample size, synthetic-style data, rule-based flags).  
- Improved **storytelling** by linking charts to operational actions and a short deck.

---

## Conclusion

This project is a **learning and portfolio** exercise in fraud-flavored transaction analytics. It shows how I approach structured data, document assumptions, and explain risk in business terms. I am early in my career and focused on growing depth in SQL, dashboard tools, and modeling—while keeping analysis clear, ethical, and easy for a team to review.

---

**Dataset credit:** [valakhorasani / Bank Transaction Dataset for Fraud Detection on Kaggle](https://www.kaggle.com/datasets/valakhorasani/bank-transaction-dataset-for-fraud-detection)
