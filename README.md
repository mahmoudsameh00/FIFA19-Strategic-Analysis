# ⚽ FIFA 19 Strategic Analysis & Valuation System

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg?style=for-the-badge&logo=python&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-Desktop-orange.svg?style=for-the-badge&logo=tableau&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success.svg?style=for-the-badge)

## 📌 Executive Summary
This project acts as a **Football Consultancy Suite**, utilizing machine learning and data visualization to solve key operational challenges in club management. By processing the FIFA 19 dataset through a rigorous Data Engineering pipeline, we built a **Decision Support System** that optimizes:

1.  **Player Valuation:** Removing market inefficiencies using correlation analysis.
2.  **Scouting:** Identifying high-potential talent ("Hidden Gems") using "Moneyball" metrics.
3.  **Squad Planning:** Visualizing depth and structural weaknesses using Radar Charts.
4.  **Financial Strategy:** Managing contract risks and capitalizing on Bosman transfers.

---

## 🏗️ Project Architecture

The project is divided into two distinct technical pipelines:

### 1️⃣ Data Engineering Pipeline (`notebooks/01_...`)
**Goal:** Transform raw, messy data into a "Golden Record" for analysis.
* **Advanced Imputation:** Trained a **Random Forest Regressor** to predict missing `Release Clause` values ($R^2 \approx 0.94$) instead of using standard mean filling, preserving the financial distribution.
* **Domain Logic Application:**
    * **Goalkeepers:** Imputed missing outfield stats with `0` based on position logic.
    * **Contracts:** Calculated `Contract_Years_Remaining` and imputed missing expiration dates using a distribution-based 3-year offset.
* **Feature Engineering:** Mapped 160+ nationalities to broad **Regional Markets** (e.g., "South America", "DACH Region") for macro-scouting.

### 2️⃣ Strategic Intelligence Analysis (`notebooks/02_...`)
**Goal:** Generate actionable intelligence and specific transfer targets.
* **Growth Modeling:** Calculated `Growth_Potential = Potential - Overall` to find players entering their prime.
* **Squad Architecture:** Aggregated specific positions (e.g., LWB, LB, CB) into functional roles (**Defender, Midfielder, Attacker**) to build Squad Depth Heatmaps.
* **Risk Assessment:** Flagged "Flight Risks" (High Value + <1 Year Contract) and "Deadwood" (Low Performance + High Wage).

---

## 📊 Tableau Dashboard Suite
*(Click the link below to download the interactive workbook)*
📂 **[Download FIFA19_Strategic_Analysis_Dashboard.twbx](./dashboard/FIFA19_Strategic_Analysis_Dashboard.twbx)**

The analysis culminates in 4 interactive dashboards:

### 🔹 Dashboard 1: Valuation & Economics
**Business Question:** *Are we overpaying for talent?*
* Analyzes the **"Positional Tax"** (the premium paid for Strikers vs. Defenders).
* Visualizes **Wage Efficiency** (Cost per Attribute Point) to identify overpaid stars.
![Valuation](./dashboard/images/01_valuation_economics.png)

### 🔹 Dashboard 2: Talent Growth & ROI
**Business Question:** *Where are the future stars?*
* **The Age Curve:** Visualizes the peak performance window (Age 24-29) for optimal recruitment.
* **Gem Finder:** Isolates U21 players with Potential >82 and Market Value <£10M.
![Talent](./dashboard/images/02_talent_growth.png)

### 🔹 Dashboard 3: Squad Architecture
**Business Question:** *Do we have enough depth?*
* **Depth Map:** A heatmap of "First Team Ready" players per position.
* **Radar Charts:** Compares specific transfer targets against the "Ideal Player" profile for their role.
![Squad](./dashboard/images/03_squad_depth.png)

### 🔹 Dashboard 4: Contract Risk Management
**Business Question:** *Who is leaving for free?*
* **Bosman Targets:** A watchlist of elite players approaching free agency.
* **Deadwood Action Plan:** A prioritized list of players to sell or terminate based on wage burden.
![Contracts](./dashboard/images/04_contract_strategy.png)

---

## 📂 Repository Structure
```text
FIFA19-Strategic-Analysis/
│
├── 📁 Rawdata/
│   ├── fifa19.csv                    # Original Kaggle Dataset
│   └── fifa19_eda_ready.csv              # The "Golden Record" (Cleaned CSV)
│
├── 📁 Tableau_Datasets/        # Processed CSVs specifically for Tableau
│   ├── Tableau_Age_Curve.csv
│   ├── Tableau_Gem_Finder.csv
│   ├── Tableau_Squad_Depth.csv
│   └── ... (Other Dashboard Inputs)
│
├── 📁 notebooks/
│   ├── 01_Data_Engineering_Pipeline.ipynb   # Cleaning, ML Imputation, Encoding
│   └── 02_Strategic_Intelligence_Analysis.ipynb  # Business Logic & Prep for Tableau
│
├── 📁 models/
│   ├── release_clause_rf_model.joblib  # Trained Random Forest Model (Release Clause Imputation)
│   └── Positional_Backup_Model.joblib  # KNN Model for Player Similarity
│   
├── 📁 dashboard/
│   ├── FIFA19_Strategic_Analysis_Dashboard.twbx  # Tableau Workbook
│   └── images/                                   # Screenshots for README
│
├── 📁 plots/  # 15 Static High-Res Python Visualizations 
│             
├── requirements.txt            # Python Dependencies
└── README.md                   # Project Documentation
