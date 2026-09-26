
# ✅ AI Data Quality & Anomaly Detection System

---

> **Upload any CSV or Excel file → Get a full AI-powered data quality report in seconds.**
> No setup. No code. No manual inspection. Just upload and go.

</div>

---

## 📸 What It Looks Like

| Feature | Description |
|---------|-------------|
| 📊 **Data Health Report** | Quality score, readiness bar, critical/warning/passed breakdown |
| 🏥 **Column Health Cards** | Per-column red/orange/green health cards with completeness fill bars |
| 🔬 **Industry Detector** | Auto-detects Sales, HR, Medical, Transport, Finance, E-Commerce |
| 📈 **Before vs After Chart** | Visual comparison of every quality dimension before and after cleaning |
| 🤖 **AI Code Generator** | Writes exact Python cleaning code specific to your dataset |

---

## 🤔 The Problem This Solves

In the real world, **data is always messy.**

Before any data analyst or data scientist can build dashboards, train ML models, or generate reports — someone has to check if the data is actually clean. That means:

- Are there missing values? Which columns? How many?
- Are there duplicate rows inflating counts?
- Are there outliers skewing averages?
- Are emails, phone numbers, and dates formatted correctly?
- Are ID columns safe to auto-fill, or will that create duplicate identities?
- Is the data even the right type?

At most companies this is done **manually** — opening Excel, writing one-off scripts, spending hours on something that should take seconds.

**This tool automates all of it — and knows when NOT to touch your data.**

---

## ✨ Features

### 📊 Data Health Report
A professional dashboard at the top showing your dataset's overall health — quality score out of 100, data readiness progress bar, and a live breakdown of critical issues, warnings, and passed columns.

### 🏥 Column Health Cards
Every column gets its own health card — color coded red (critical), orange (warning), or green (healthy) — with a completeness fill bar showing exactly how much data is present and outlier counts where relevant.

### 🔬 Industry Detector
Automatically detects what kind of dataset you've uploaded — **Sales, HR, Medical, Transport, Finance, or E-Commerce** — and runs domain-specific validation checks unique to that industry:

| Industry | Domain-Specific Checks |
|----------|------------------------|
| 🛒 Sales | Negative revenue, zero quantities, discounts > 100% |
| 👥 HR | Negative salaries, ages outside 18–80, impossible experience years |
| 🏥 Medical | Ages outside 0–120, impossible BMI values, invalid blood pressure |
| 🚢 Transport | Negative fares, duplicate ticket IDs |
| 💰 Finance | Transaction amounts over 1 billion, invalid interest rates |
| 🛍️ E-Commerce | Ratings outside 0–5, negative prices, negative stock values |

### 🏆 Quality Score (0–100)
A weighted scoring system that penalizes your dataset across 8 dimensions:

| Dimension | Max Penalty |
|-----------|------------|
| Missing values | -30 points |
| Duplicate rows | -20 points |
| Outliers (IQR method) | -20 points |
| Type mismatches | -10 points |
| Invalid emails | -10 points |
| Invalid dates | -8 points |
| Invalid phones | -5 points |
| Consistency issues | -5 points |

### 📈 Before vs After Quality Chart
After cleaning, a grouped bar chart shows the improvement across every dimension — missing %, duplicates %, outlier %, type mismatches, and consistency issues — with score cards showing the exact points gained.

### 🧠 Smart Type Inference
Every column is analyzed to determine its **true** type — not just what the file says it is. A column stored as text but containing numbers gets flagged. Phone and postal columns are never misidentified as numeric.

### 🔍 Data Validation Suite
- **📧 Email Validation** — regex-based detection of malformed email addresses
- **📅 Date Validation** — detects unparseable date strings and impossible dates
- **📱 Phone Validation** — checks format, digit count, and character validity
- **⚠️ Consistency Check** — finds case inconsistencies (Male/male/MALE) and whitespace inconsistencies, with suggested fix commands

### 💡 Safe vs Dangerous Fix Classification
Every suggestion is labeled:
- ✅ **Safe to auto-fix** — numeric nulls, categorical nulls in low-cardinality columns
- ⚠️ **Risky** — high-cardinality columns where mode fill could be misleading
- ❌ **Do NOT auto-fill** — ID columns, emails, phones, dates — these require manual review or source correction

### 🧹 Smart Auto Clean
One click to automatically fix all **safe** issues:
- Drops columns with >50% missing data
- Fills numeric nulls with column median
- Fills safe categorical nulls with column mode
- Removes duplicate rows (normalized comparison)
- **Skips dangerous columns** (ID, email, phone, date) with a clear warning instead of creating invalid data

### 🤖 AI Cleaning Code Generator
The most unique feature — generates **ready-to-run Python code** specific to your dataset. Not generic templates. Real code with your actual column names, real median values, real IQR bounds, and warnings on dangerous columns:

```python
import pandas as pd

# DROP 'cabin' — 77.1% missing, too much to salvage
df.drop(columns=['cabin'], inplace=True)

# FILL 'age' nulls with median (28.0) — 19.87% missing
df['age'] = pd.to_numeric(df['age'], errors='coerce')
df['age'].fillna(28.0, inplace=True)

# WARNING: 'customer_id' has 12% missing — DO NOT auto-fill
# This is an ID column — flag these rows for manual review
# df['customer_id_missing_flag'] = df['customer_id'].isna().astype(int)

# CAP 'fare' outliers at IQR bounds [0, 65.63]
df['fare'] = df['fare'].clip(lower=0, upper=65.63)
```

### 🔗 Correlation Heatmap
Interactive heatmap showing relationships between all meaningful numeric columns. Phone, postal, and constant columns are excluded to prevent noise. Strong correlations (≥ 0.5) are automatically highlighted and explained, with valid pair counts shown.

### 📊 Distribution Plots
Histogram + box plot for every numeric column with mean, median, standard deviation, and skewness stats — lets you visually spot skewed distributions instantly.

### 🔵 Scatter Plot
Pick any two numeric columns and visualize their relationship with an OLS trend line.

### 📥 Downloadable Outputs
- **Cleaned dataset** as CSV after auto-cleaning
- **AI-generated cleaning script** as a `.py` file ready to run
- **Quality report** as CSV with scores per column

---

## 🆚 How This Compares

| Feature | This Tool | Pandas df.info() | Great Expectations | AWS DataBrew |
|---------|-----------|-----------------|-------------------|--------------|
| Zero setup needed | ✅ | ❌ | ❌ | ❌ |
| Quality score | ✅ | ❌ | ✅ | ✅ |
| Industry detection | ✅ | ❌ | ❌ | ❌ |
| Safe vs dangerous fix | ✅ | ❌ | ❌ | ⚠️ |
| AI code generator | ✅ | ❌ | ❌ | ❌ |
| Before vs after chart | ✅ | ❌ | ❌ | ✅ |
| Free & open source | ✅ | ✅ | ✅ | ❌ |

---

## 🛠️ Tech Stack

| Technology | Purpose |
|-----------|---------|
| **Python 3.10+** | Core language |
| **Pandas** | Data loading, manipulation, profiling |
| **NumPy** | Numerical operations, IQR calculations |
| **Streamlit** | Web UI and deployment |
| **Plotly** | Interactive charts (bar, heatmap, histogram, scatter) |
| **Statsmodels** | OLS trendline for scatter plots |
| **OpenPyXL** | Excel file (.xlsx, .xls) support |
| **Regex** | Email and phone validation |

---

## 🚀 Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/Samarthsj1013/AI-Data-Quality-Anomaly-Detection-System.git
cd AI-Data-Quality-Anomaly-Detection-System

# 2. Install dependencies
pip install streamlit pandas numpy plotly openpyxl statsmodels

# 3. Run the app
streamlit run app.py
```

Open your browser at `http://localhost:8501`

---

## 📁 Project Structure

```
AI-Data-Quality-Anomaly-Detection-System/
│
├── app.py              ← Streamlit UI — all sections, layout, visualizations
├── checker.py          ← Core logic — all checks, scoring, cleaning functions
├── requirements.txt    ← Python dependencies
└── README.md           ← You are here
```

---

## 🧠 How It Works — Under The Hood

### 1. Data Loading (`load_data`)
Loads CSV or Excel files with `dtype=str` to preserve raw values exactly as stored, then runs `normalize_nulls` to convert 20+ hidden null-like values ("none", "N/A", "-", "unknown", "nil" etc.) into proper `NaN` before any analysis.

### 2. Smart Type Inference (`infer_column_types`)
For each column, attempts to coerce values to numeric and datetime. If ≥60% of values coerce successfully → that's the inferred type. Phone and postal columns are explicitly excluded from numeric inference to prevent misidentification.

### 3. Quality Score (`quality_score`)
Weighted penalty system across 8 dimensions. Each penalty is capped to prevent any single issue from dominating the total. Final score = `max(0, 100 - sum_of_all_penalties)`.

### 4. Outlier Detection (`detect_outliers`)
Uses the **IQR method**:
- Q1 = 25th percentile, Q3 = 75th percentile
- IQR = Q3 − Q1
- Outlier if value < Q1 − 1.5×IQR **or** value > Q3 + 1.5×IQR

### 5. Safe vs Dangerous Classification (`generate_suggestions`)
Every null-fix suggestion is categorized based on column name patterns:
- ID/key/uuid columns → ❌ flag for manual review
- Email/phone columns → ❌ must be collected from source
- Date/time columns → ❌ needs business context
- High cardinality (>80% unique) → ⚠️ risky
- Low-cardinality categorical → ✅ safe to fill with mode

### 6. Industry Detection (`detect_industry`)
Keyword scoring across 6 industries — each industry has 8 signal keywords checked against column names. The industry with the highest match count wins. Confidence = number of keywords matched.

### 7. Correlation Heatmap (`correlation_heatmap`)
Force-coerces all non-phone, non-postal columns to numeric before calculating correlations. Excludes columns with <50% valid values or zero variance to prevent noise. Returns valid pair counts per correlation for scientific transparency.

### 8. Code Generation (`generate_cleaning_code`)
Programmatically builds Python code strings based on detected issues — using real median values, real IQR bounds, real column names, and real warnings on dangerous columns. Zero hardcoding, 100% dataset-specific output every time.

---

## 🧪 Test Datasets

| Dataset | What it tests |
|---------|--------------|
| [Titanic (Kaggle)](https://www.kaggle.com/datasets/heptapod/titanic) | Missing values, outliers, type mismatches, transport detection |
| Any HR CSV with salary/employee columns | HR industry detection, salary range checks |
| Any sales CSV with revenue/product columns | Sales industry detection, negative revenue check |
| Any medical CSV with age/BMI columns | Medical industry detection, impossible value checks |
| Any messy CSV with 50k+ rows | Full stress test of all features |

---

## 💼 Real-World Applications

This tool replicates what enterprise tools like **AWS Glue DataBrew**, **Great Expectations**, and **Talend Data Quality** do — built from scratch as a lightweight, open-source alternative that anyone can use without any setup.

Use cases:
- **Data Engineers** — profile raw datasets before building pipelines
- **Data Analysts** — validate data before building dashboards or reports
- **ML Engineers** — check dataset quality before training models
- **Students** — understand what's wrong with their assignment or project datasets

---

## 🗺️ Roadmap

- [ ] Cross-column validation (quantity × unit_price ≈ total_amount)
- [ ] Null heatmap — visual grid of exactly which cells are missing
- [ ] PDF report export
- [ ] Multi-file comparison (compare 2 datasets side by side)
- [ ] ML-based anomaly detection beyond IQR
- [ ] Support for JSON and Parquet files
- [ ] API endpoint for programmatic access

---

## 👨‍💻 Author

**Samarth Jayant**
B.E. Information Science & Engineering | Global Academy of Technology, Bangalore

[![GitHub](https://img.shields.io/badge/GitHub-Samarthsj1013-181717?style=flat&logo=github)](https://github.com/Samarthsj1013/AI-Data-Quality-Anomaly-Detection-System)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/samarthsj1013)
[![Live App](https://img.shields.io/badge/Live_App-data--quality--checker13.streamlit.app-FF4B4B?style=flat)](https://data-quality-checker13.streamlit.app)

---

<div align="center">

**If this project helped you, give it a ⭐ on GitHub!**

*Built with Python, Streamlit, and way too much caffeine ☕*

</div>