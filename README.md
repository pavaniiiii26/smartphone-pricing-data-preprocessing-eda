# smartphone-pricing-data-preprocessing-eda
Data preprocessing and EDA on 1800+ smartphone listings to uncover what drives market pricing.

# 📱 Smartphone Features vs Market Pricing
### Data Preprocessing & Exploratory Data Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=flat-square&logo=pandas)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.x-F7931E?style=flat-square&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📌 About The Project

This is a mini-project for the **Data Preprocessing and Exploratory Learning (DPEL)** course. The goal is to take a real-world smartphone market dataset, clean it thoroughly, engineer useful features, and derive meaningful insights through visualization.

We explore how hardware specs like RAM and storage, along with brand identity and contract status, relate to smartphone pricing — a question relevant to both consumers and market analysts.

---

## 🗂️ Project Structure

```
📦 smartphone-pricing-analysis
 ┣ 📓 DPEL_miniproject_improved.ipynb   # Main notebook
 ┣ 📊 smartphones (1).csv               # Dataset
 ┗ 📄 README.md                         # This file
```

---

## 📊 Dataset Overview

The dataset contains **1816 smartphone listings** with the following attributes:

| Column | Description |
|--------|-------------|
| `Smartphone` | Full product name |
| `Brand` | Manufacturer (e.g. Samsung, Apple, Xiaomi) |
| `Model` | Specific model name |
| `RAM` | RAM in GB |
| `Storage` | Internal storage in GB |
| `Color` | Color variant |
| `Free` | Contract-free (Yes / No) |
| `Final Price` | Selling price in € |

---

## 🔧 What We Did

### 1. 🔍 Data Understanding
- Loaded and inspected the dataset shape, datatypes, and basic statistics.
- Identified columns with missing values, wrong types, and unrealistic entries.

### 2. 🧹 Handling Missing Values
- Detected **483 missing RAM** values and **25 missing Storage** values.
- Applied **median imputation first**, then snapped values to the nearest realistic category.
  > ⚠️ *Fixed a silent bug where NaN values were incorrectly mapped to 4 GB due to NumPy's `argmin()` behavior on NaN arrays.*

### 3. 🔁 Removing Duplicates
- Checked for and removed duplicate rows to ensure data integrity.

### 4. 🚫 Fixing Incorrect Values
- Removed entries with unrealistic storage (< 16 GB or > 512 GB).
- Performed **IQR-based outlier detection** on `Final Price` — outliers were flagged but retained as they represent legitimate premium phones.

### 5. 🏷️ Data Type Correction
- Converted `RAM` and `Storage` to integer types after cleaning.

### 6. ⚙️ Feature Engineering
- **`Price_per_GB`**: Price efficiency metric (€ per GB of storage).
- **`Price_Category`**: Categorical bins — `Budget` (< €300), `Mid-range` (€300–700), `Premium` (> €700).

### 7. 🔢 Encoding Categorical Variables
- **`Free`** column: Binary encoded (`Yes → 1`, `No → 0`).
  > ⚠️ *This column was completely skipped in the original — fixed.*
- **`Price_Category`**: Ordinally encoded (`Budget=0`, `Mid-range=1`, `Premium=2`) to preserve meaningful order.
- **`Brand` & `Color`**: One-Hot Encoded with `drop_first=True`.

### 8. 📏 Scaling / Normalization
- Applied `StandardScaler` only to meaningful numeric columns: `RAM`, `Storage`, `Final Price`, `Price_per_GB`.
  > ⚠️ *Fixed: scaling is now applied to a separate `df_scaled` copy — the original notebook scaled in-place, causing all visualizations to plot standardized values while labeling them as "€", making charts unreadable.*

---

## 📈 Visualizations

| # | Chart | Insight |
|---|-------|---------|
| 1 | Histogram + Boxplot — Final Price | Right-skewed distribution; most phones under €500 |
| 2 | Boxplot — RAM vs Final Price | Higher RAM correlates strongly with higher price |
| 3 | Pairplot — by Price Category | Clear separation between Budget, Mid-range, Premium clusters |
| 4 | Bar Chart — Avg Price by Brand | Apple and Samsung lead; Xiaomi and Realme are budget-oriented |
| 5 | Boxplot — Storage vs Final Price | 256 GB+ phones command significant price premiums |
| 6 | Pie Chart — Top 10 Colors | Black, Blue, and White dominate the market |
| 7 | Boxplot — RAM by Brand | Premium brands consistently offer higher RAM |
| 8 | Heatmap — Correlation Matrix | Moderate positive correlation between specs and price |
| 9 | Bar Chart — Price Category Distribution | *(New)* Mid-range is the most common segment |
| 10 | Bar Chart — Price per GB by Brand | *(New)* Budget brands deliver more storage per euro |

---

## 🛠️ Technologies Used

- **Python 3.10**
- **Pandas** — data manipulation and cleaning
- **NumPy** — numerical operations
- **Matplotlib & Seaborn** — data visualization
- **Scikit-learn** — `StandardScaler` for feature scaling

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/smartphone-pricing-analysis.git
   cd smartphone-pricing-analysis
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook DataPreprocessing_project.ipynb
   ```

4. Make sure the dataset file `smartphones (1).csv` is in the same directory as the notebook.

---

## 💡 Key Findings

- **RAM and Storage** are moderate-to-strong predictors of price — higher specs consistently push prices up.
- **Brand** is a significant factor — Apple and Samsung price at a premium even for equivalent specs.
- **Budget segment dominates volume** — the majority of listings fall under €700, reflecting mass-market demand.
- **Black, Blue, and White** account for the majority of color listings, suggesting manufacturers focus production on neutral tones.
- **Price per GB** analysis shows that budget brands (Xiaomi, Realme) deliver significantly more storage per euro compared to Apple and Samsung.

---

## 📝 License

This project is for academic purposes under the DPEL course curriculum.
