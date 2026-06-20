# customer-value-retention-sql
SQL + Python + Power BI analysis to decode customer value, segment buyers, and build a data-backed retention strategy for a D2C fashion retailer.

# 🛍️ Decoding Customer Value: A SQL-Driven Retention Strategy

> **IIT Guwahati | Data Analytics Consulting Project**  
> A full-stack data analytics project to identify high-value customers, decode promo dependency, and build a data-backed retention playbook for a D2C fashion retailer.

---

## 📌 Problem Statement

A direct-to-consumer (D2C) fashion brand sells clothing, accessories, footwear, and outerwear across the United States. Despite having 3,900 customers and a structured discount & promotions program, the brand lacks intelligence on:

- Who their most valuable customers actually are
- What behavioral patterns distinguish high-value from low-value customers
- Whether discounts and promo codes are building loyalty — or creating dependency
- Which product categories, regions, and demographics to prioritize for retention

**Core business question:** *Can the brand use transactional and behavioral data to identify its most valuable customers, measure how much of its current revenue depends on promotions, and build a data-backed retention strategy without hurting sales?*

---

## 🎯 Key Questions Addressed

1. Who are the genuinely loyal customers — those who buy even without a discount?
2. What behavioral patterns define high-value customers over time?
3. Which product categories are associated with loyalty vs. discount-driven volume?
4. How should the brand restructure its promotional strategy to protect margins without losing volume?
5. What does the brand's ideal customer profile look like, and how can it acquire more of them?

---

## 🗂️ Project Structure

```
📁 IITG- SQL project/
│
├── 📓 IITG_finaledit.ipynb          # Data cleaning, EDA, feature engineering & value scoring (Python)
├── 📓 sql_analysis.ipynb             # SQL-based business queries using SQLite in-memory DB
├── 📊 IITG.pbix                      # Power BI dashboard (Founder Dashboard)
│
├── 📄 Dataset.csv                    # Raw dataset — 3,900 customers × 18 features
├── 📄 customer_scores_final.csv      # Engineered dataset with Value Score & Segment labels
│
├── 📑 IITG_Customer_Value_Report.pdf # Full analytical report
├── 📑 Retention_Playbook.pdf         # Actionable retention recommendations
│
└── 📈 [Charts — 15 visualizations across 4 analytical blocks]
    ├── 01a–01e  →  Promo & Discount Analysis
    ├── 02a–02e  →  Purchase Behavior & Segmentation
    ├── 03a–03d  →  Spend Drivers (Category, Age, Payment, Geography)
    └── 04a–04c  →  Value Score Analysis
```

---

## 🔬 Scope of Analysis

### 1. Data Preparation & Feature Engineering (Python)
- Cleaned raw dataset: merged duplicate frequency labels (`Fortnightly → Bi-Weekly`, `Every 3 Months → Quarterly`)
- Handled 37 null values in Review Rating (median imputation)
- Engineered an **Age Group** feature (binned: 18–25, 26–35, 36–45, 46–55, 55+)
- Built a **Customer Segment** label using rule-based logic:

| Segment | Rule |
|---|---|
| `Loyal — No Deals` | ≥15 purchases, no promo/discount used |
| `Loyal — Deal User` | ≥15 purchases, but uses promos or discounts |
| `Discount Hunter` | <15 purchases, promo/discount dependent |
| `Low Engagement` | <15 purchases, no promo usage |

- Computed a composite **Value Score** (0–100) using MinMax-normalized components:

```
Value Score = (Spend × 0.25) + (Purchase History × 0.30) + (Frequency × 0.25) + (Rating × 0.10)
            + (Subscription Bonus × 0.10) − (Promo Penalty × 0.10) − (Discount Penalty × 0.05)
```

---

### 2. Customer Segmentation Analysis (SQL)
SQL queries executed via SQLite in-memory database on the engineered dataset:

- **Q1 — High vs. Low Value Customer Profile:** Compared spend, purchase history, promo rate, and subscription rate across value tiers
- **Q2 — Promo Dependency by Segment:** Identified which segments show the strongest repeat purchase behavior, and which are discount-driven
- **Q3 — Geographic Intelligence:** Classified states as `Organic High Value`, `High Spend but Promo Driven`, `Developing Market`, or `Low Priority` using conditional SQL logic
- **Q4 — Category Entry vs. Retention:** Identified which categories attract new customers vs. which retain loyal ones
- **Q5 — Ideal Customer Profile (ICP):** Profiled the top 15 customer archetypes within the `Loyal — No Deals` segment using multi-dimensional grouping

---

### 3. Founder Dashboard (Power BI)
Interactive `.pbix` dashboard built for non-technical business stakeholders. Covers:
- Promo dependency map by region and segment
- Customer value distribution by tier
- Category-level spend and loyalty analysis
- Subscription vs. non-subscriber performance comparison

---

### 4. Retention Playbook (Business Recommendations)
Findings translated into two outputs: **what the brand should stop doing** and **what it should do instead**. Every recommendation states the target segment, the proposed action, and the expected margin impact — structured for a marketing team to act on immediately.

---

## 📊 Dataset Overview

| Property | Detail |
|---|---|
| Source | Synthetic retail dataset (D2C fashion, US market) |
| Rows | 3,900 customers |
| Features | 18 raw columns |
| Engineered Features | Age Group, Segment, Value Score |

**Key columns:**

`Customer ID` · `Age` · `Gender` · `Category` · `Purchase Amount (USD)` · `Location` · `Season` · `Review Rating` · `Subscription Status` · `Discount Applied` · `Promo Code Used` · `Previous Purchases` · `Payment Method` · `Frequency of Purchases`

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python (pandas, numpy) | Data cleaning & feature engineering |
| Matplotlib / Seaborn | Exploratory data visualization |
| scikit-learn (MinMaxScaler) | Value score normalization |
| SQLite (via `sqlite3`) | In-memory SQL business queries |
| Power BI | Interactive founder dashboard |
| Jupyter Notebook | End-to-end analysis environment |

---

## 🚀 How to Run

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Step 1 — Feature Engineering & EDA
Open and run `IITG_finaledit.ipynb` in Jupyter.  
This reads `Dataset.csv`, cleans the data, generates all 15 charts, and exports `customer_scores_final.csv`.

### Step 2 — SQL Analysis
Open and run `sql_analysis.ipynb`.  
This loads `customer_scores_final.csv` into an in-memory SQLite database and runs the 5 business queries.

### Step 3 — Power BI Dashboard
Open `IITG.pbix` in Power BI Desktop to explore the interactive dashboard.

> ⚠️ **Note:** File paths in the notebooks are set to local Windows paths. Update the `file_path` variable in each notebook to match your local directory before running.

---

## 📈 Key Findings (Highlights)

- **~43% of all transactions involve a promo code or discount** — the brand is heavily promotion-dependent
- The `Loyal — No Deals` segment, while smaller in size, drives disproportionately higher value scores
- **Subscribers consistently outperform non-subscribers** across spend, purchase history, and review ratings
- Certain categories (e.g., Outerwear) show stronger loyalty signals, while others primarily attract discount hunters
- A handful of states show high spend with low promo dependency — the brand's organic growth targets

---

## 📁 Outputs

| File | Description |
|---|---|
| `customer_scores_final.csv` | Scored & segmented customer dataset ready for CRM/marketing use |
| `IITG_Customer_Value_Report.pdf` | Full analytical findings report |
| `Retention_Playbook.pdf` | Actionable retention strategy document |
| `IITG.pbix` | Power BI dashboard for business stakeholders |
| `01a–04c *.png` | 15 publication-ready visualizations |

---

## 👥 Authors

**Juee Mahajan & Devesh Langer**  
IIT Guwahati | Data Analytics & Consulting Program

---

## 📄 License

This project was completed as part of an academic program. The dataset is synthetic and used for educational purposes only.
