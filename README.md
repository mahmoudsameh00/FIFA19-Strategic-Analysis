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

This workbook converts the Python insights into 4 executive-level dashboards, designed to answer specific strategic questions:

### 🔹 Dashboard 1: Valuation & Economics
**Focus:** *Establishing a financial baseline and identifying market anomalies.*
1.  **Correlation Matrix (Heatmap):** Analyzes the drivers of player value by correlating financial metrics (`Value`, `Wage`, `Release Clause`) against key attributes (`Overall`, `Potential`, `Age`, `Reactions`, `Composure`, `Intl. Reputation`).
2.  **Wage Efficiency (Radar Chart):** Maps the relationship between **Wage** and **Market Value**. Deviations highlight "Bargains" (High Value / Low Wage) versus "Overpaid" assets (Low Value / High Wage).
3.  **The Talent Premium Curve:** A scatter plot of **Value vs. Overall Rating**, demonstrating the exponential cost structure of the transfer market (e.g., the massive price jump required to upgrade a player from 85 to 90 Rated).
4.  **The Positional Tax:** A comparative bar chart showing the average Market Value per position, quantifying the "Forward Premium" (clubs paying ~30% more for attackers than defenders).

### 🔹 Dashboard 2: Global Scouting & Talent
**Focus:** *Identifying high-ROI acquisition targets.*
1.  **Global Talent Map (Geospatial):** A density map pinpointing the specific nations producing the highest volume of "Elite Potential" players.
2.  **Gem Finder (Bubble Chart):** A multi-variable filter isolating U21 players with **High Potential (>82)** but **Low Release Clauses (<£5M)**. Bubble size indicates the "Growth Gap."
3.  **ROI Story:** Visualizes "Undervalued Assets" by plotting Market Value against total Stat Points, exposing players who offer elite output for a fraction of the standard price.
4.  **Growth Dumbbells:** Connects a player's *Current Rating* to their *Potential Rating* with a dumbbell plot, clearly visualizing the development runway left for each prospect.

### 🔹 Dashboard 3: Squad Architecture
**Focus:** *Team depth, balance, and succession planning.*
1.  **The Age Curve:** Tracks the average Overall Rating across age groups to mathematically determine the optimal "Buying Window" (Age 21-24) and "Selling Window" (Age 28-30).
2.  **Squad Depth Heatmap:** A grid visualization showing the count of "First Team Ready" players for every position, instantly highlighting depth crises (e.g., "0 Backup Left Backs").
3.  **Player Radar Replacements:** Overlays a potential signing's attributes against a departing star (using the KNN model output) to visually validate them as a statistically suitable successor.

### 🔹 Dashboard 4: Contract Strategy
**Focus:** *Risk management and asset protection.*
1.  **Flight Risk Analysis:** Flags high-value assets (>£20M) with less than 1 year remaining on their contract, warning of potential free transfer losses.
2.  **Contract Strategy Timeline:** Visualizes the squad's contract expiry schedule over the next 5 years to prevent mass exoduses.
3.  **Bosman Targets:** A watchlist of elite players from *other* clubs whose contracts expire in 2019, identifying targets for free acquisition.
4.  **Deadwood Action Plan:** A scatter plot of **Wage vs. Performance**. The "Danger Zone" (Top-Left) identifies players earning star wages while delivering sub-par performance—primary candidates for termination.
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
