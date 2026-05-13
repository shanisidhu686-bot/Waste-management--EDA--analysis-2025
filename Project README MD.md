# 🗑️ Waste Management Data Analysis — EDA Project

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Charts-3F4F75?logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 📌 Overview

This project performs an end-to-end **Exploratory Data Analysis (EDA)** on a one-year trip summary dataset from a waste management company operating in the **UAE**. The dataset covers customer activity, waste types, driver operations, truck utilization, and financial performance.

The goal is to uncover actionable insights to improve **operational efficiency**, **customer retention**, and **revenue growth** — and to make the case for adopting an ERP system.

---

## 📂 Dataset

| Field | Description |
|-------|-------------|
| **Source** | `Trip rep 24.xlsx` (Google Drive) |
| **Format** | Excel → CSV |
| **Period** | Full calendar year (12 months) |
| **Key Columns** | Date, Month, Customer, Location, Waste Type, Driver, Truck No, Activity, Sales Person, Quantity, Price, Amount, VAT 5%, Amount with VAT |

---

## 🎯 Objectives

- Clean and preprocess raw operational data
- Handle missing values, inconsistent naming, and wrong data types
- Perform split analysis on **trip-based** vs **weight-based (KG)** records
- Identify top customers, drivers, and waste types by volume and revenue
- Analyze seasonal and monthly performance trends
- Evaluate driver workload and fleet utilization
- Segment customers by loyalty and revenue tier
- Visualize all findings with interactive and static charts

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, and transformation |
| `numpy` | Numerical operations |
| `matplotlib` | Static bar and line charts |
| `seaborn` | Heatmaps and styled visualizations |
| `plotly.express` | Interactive charts and treemaps |

---

## 🔄 Project Workflow

```
Raw Excel Data
     ↓
Data Loading & Header Fix
     ↓
Missing Value Handling
     ↓
Column Renaming & Data Type Assignment
     ↓
Driver & Customer Name Standardization
     ↓
Quantity Type Split (Trip vs KG)
     ↓
EDA & Visualization
     ↓
Insights & Recommendations
```

---

## 🧹 Data Preprocessing

### Key Steps:
- **Header Fix** — First two rows were empty; actual column headers were in row 2 and were extracted and reassigned
- **Dropped irrelevant columns** — `Tripsheet number`, `Skip No`, `Manifest No`
- **Missing Values:**
  - Numerical columns (`Quantity`, `Price`, `Amount`, etc.) → filled with column **mean**
  - `Driver` column → filled with **mode** (most frequent driver)
  - `Truck No` → filled with `0`
- **Column Standardization** — All column names converted to `lowercase_with_underscores`
- **Waste Type Cleaning** — Removed irrelevant entries like `"rental"` and `"charges"`
- **Data Type Conversion:**
  - `quantity` → `int64`
  - `date` → `datetime`
  - All text columns → `category` dtype for performance
- **Driver Name Standardization:**
  - Regex used to unify spellings (e.g., `md`, `mohd`, `mohamad` → `mohammed`)
  - Manual correction dictionary applied for 15+ naming inconsistencies
  - Final names converted to **Title Case**
- **Customer Name Deduplication** — Variations of the same customer (e.g., `"Nest Waste"`, `"Nest Waste(Noble)"`) merged into one

---

## 📊 Exploratory Data Analysis

### Quantity Type Split
The `quantity` column contained mixed data:
- Value `1` → **Trip-based** collection
- Value `> 1` → **KG-based** (weight) collection

Two separate DataFrames were created:
- `trip_df` — for operational/trip-frequency analysis
- `kg_df` — for waste volume/weight analysis

---

### 📈 Key Analyses & Insights

#### 💰 Top Customers by Revenue
- Revenue is **highly concentrated** among a small group of customers
- Losing even one top client could significantly impact total revenue
- Suggests need for **customer diversification strategy**

#### 📅 Monthly Revenue Trend
- Clear **revenue dip during Ramadan** due to reduced commercial activity in UAE
- Revenue strengthens in the latter half of the year
- Planning and schedule optimization can mitigate seasonal drops

#### 👤 Sales Person Performance
- **Shanir** consistently outperforms across most months and customers
- Heatmap analysis confirms Shanir manages the largest share of high-value accounts
- Incentive-based structures recommended to retain top salespeople

#### 🔁 Customer Loyalty Segmentation
| Tier | Active Months | Share |
|------|--------------|-------|
| One-time | 1–3 | ~54.9% |
| Occasional | 4–6 | — |
| Regular | 7–9 | — |
| Loyal | 10–12 | ~27.8% combined (Regular + Loyal) |

> ⚠️ Over half of customers never returned — retention strategy urgently needed.

#### 🏷️ Customer Revenue Tiers
Customers classified as: `Small`, `Medium`, `Large`, `Premium` based on total revenue.

#### 🚛 Driver Performance
- A few top drivers (Noor, Harjinder, Gurpreet) handle the majority of trips
- **145 total drivers** — many underutilized
- Higher trip count ≠ higher revenue (route value varies)

#### 🚌 Fleet Utilization
- Drivers are mostly assigned to **fixed trucks** rather than a shared pool
- Truck `75194` dominated by Noor; Truck `64258` used primarily by Harjinder & Gurpreet
- Suggests need for **fleet rotation** and balanced workload distribution

#### 🗑️ Waste Type Analysis (Trip-based)
- **Concrete Waste** peaks sharply in June (construction demand)
- **General Waste** shows consistent year-round growth
- **Wood Waste** peaks in UAE's cooler construction season (Oct–Dec)

#### ⚖️ Waste Type Analysis (KG-based)
- **Hazardous Waste** is the largest by weight, peaking in Nov–Dec
- KG-based collection is **project-driven**, not consistent month-to-month

#### 📊 KG vs Trip Revenue Split
- Trip-based operations: **~70.6%** of total revenue
- KG-based operations: **~29.7%** of total revenue

---

## 📉 Visualizations

| Chart | Type |
|-------|------|
| Top 10 Customers by Revenue (Trip & KG) | Horizontal Bar (Plotly) |
| Monthly Revenue Trend | Bar Chart (Matplotlib) |
| Sales Person Monthly Trend | Line Chart (Matplotlib) |
| Sales Person vs Customer Heatmap | Heatmap (Seaborn) |
| Customer Revenue Segmentation | Pie Chart |
| KG vs Trip Revenue Distribution | Donut Chart |
| Monthly Revenue + Trip Count | Dual-Axis Line Chart |
| Customer Loyalty Distribution | Pie Chart |
| Driver Trips vs Revenue (Top 10) | Dual-Axis Bar+Line Chart |
| Driver Performance Classification | Pie Chart |
| Driver–Truck Utilization Heatmap | Interactive Heatmap (Plotly) |
| Top 5 KG Waste Types — Monthly Trend | Line Chart (Plotly) |
| Top 5 Trip Waste Types — Monthly Trend | Line Chart (Plotly) |
| Top 15 Waste Types by KG (Treemap) | Treemap (Plotly) |
| Top 15 Waste Types by Trip Count (Treemap) | Treemap (Plotly) |

---

## 🏁 Conclusion

This analysis identified critical patterns in a UAE-based waste management company's one-year operations:

- **Revenue is concentrated** in a small set of customers and drivers
- **Customer retention is low** — majority are one-time users
- **Seasonal demand** (Ramadan, construction season) drives predictable fluctuations
- **Fleet and driver allocation** is rigid and imbalanced
- **Hazardous and Concrete waste** require targeted planning due to volatility

### ✅ Recommendation
Implement an **ERP system** tailored for waste management to automate:
- Driver allocation and route optimization
- Fleet maintenance scheduling
- Customer follow-up and retention tracking
- Real-time financial and operational reporting

---

## 🚀 How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/waste-management-eda.git
   cd waste-management-eda
   ```

2. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn plotly openpyxl
   ```

3. **Open the notebook:**
   ```bash
   jupyter notebook Main_Project_EDA_Of_Waste_Management.ipynb
   ```

4. **Run all cells** — the dataset is loaded directly from Google Drive via the embedded link.

---

## 📁 Repository Structure

```
waste-management-eda/
│
├── Main_Project_EDA_Of_Waste_Management.ipynb   # Main analysis notebook
├── README.md                                     # Project documentation
└── data.csv                                      # Auto-generated CSV from Excel (after first run)
```

---



**Sidhrathul Munthaha**
- GitHub: [@your-username](https://github.com/shanisidhu686-bot)
- LinkedIn: [your-linkedin](https://www.linkedin.com/in/sidhrathul-munthaha)

---



This project is for educational and analytical purposes. The dataset belongs to the respective waste management company and has been used solely for academic analysis.
