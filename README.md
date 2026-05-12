✅ Data Quality Checker
An automated data quality analysis engine that profiles any CSV or Excel dataset — detecting nulls, duplicates, outliers, type mismatches, and validating emails, dates, and phone numbers. With a multi-factor quality score, auto-clean, and downloadable reports.
🟢 Live Demo • 📖 Features • 🚀 Setup • 📊 How It Works

📸 Preview
📋 Dataset Summary     → Rows, columns, nulls, duplicates, numeric cols
🏆 Quality Score       → Multi-factor 0–100 score with penalty breakdown
💡 Fix Suggestions     → Auto-generated recommendations per column
🔴 Missing Values      → Count + % per column with bar chart
🟡 Duplicate Rows      → Normalized detection (strips whitespace + lowercases)
🔵 Data Types          → Smart type inference with mismatch flagging
🟠 Outlier Detection   → IQR-based with bounds per numeric column
📧 Email Validation    → Regex-based invalid email detection
📅 Date Validation     → Multi-format date parsing with invalid examples
📱 Phone Validation    → Format check with invalid count
⚠️ Consistency Check  → Detects India vs IND style inconsistencies
🔗 Correlation Heatmap → Numeric column relationship matrix
📊 Distribution Plots  → Histogram + box plot + skewness stats
🔵 Scatter Plot        → Column vs column with trendline
🧹 Auto Clean          → One-click fix + download cleaned CSV

✨ Features
🧠 Smart Type Inference
Unlike basic dtype checking, this tool uses coercion rate analysis:

Tries converting each column to numeric and datetime
If 60%+ values convert successfully → infers as that type
Phone columns are explicitly excluded from numeric inference
Detects stored-as-text-but-looks-numeric mismatches

🔍 Hidden Null Detection
Catches nulls that pandas misses:
pythonNULL_LIKE = ["", " ", "none", "null", "na", "n/a", "not_available",
             "unknown", "undefined", "missing", "-", "--", "nil", "void"]
All these are normalized to NaN before analysis begins.
🟡 Normalized Duplicate Detection
Standard df.duplicated() misses duplicates with whitespace or casing differences. This tool:

Strips whitespace from all values
Lowercases all strings
Replaces "nan" strings with actual NaN
Ignores ID-like columns (id, index, row_id, sr.no)

🟠 IQR Outlier Detection

Calculates Q1, Q3, IQR per numeric column
Flags values outside Q1 - 1.5×IQR and Q3 + 1.5×IQR
Shows exact bounds, count, min, and max per column

📧 Validation System
TypeMethodExample CaughtEmailRegex ^[\w\.\-]+@[\w\.\-]+\.\w{2,}$riya@gmail, neha@@gmail.comDatepd.to_datetime(errors='coerce')2023-09-31, not_a_datePhoneRegex ^\+?[\d\s\-\(\)]{7,15}$abcd123456, 98765ConsistencyCase-insensitive groupingIndia vs IND
🏆 Multi-Factor Quality Score
Score = 100
- Null Penalty       → up to -30  (based on avg missing %)
- Duplicate Penalty  → up to -20  (based on dup %)
- Outlier Penalty    → up to -20  (based on outlier %)
- Type Mismatch      → up to -10  (per mismatched column)
- Invalid Emails     → up to -10
- Invalid Dates      → up to -8
- Invalid Phones     → up to -5
- Consistency Issues → up to -5
🧹 Auto Clean
One click fixes:

Converts hidden null strings to NaN
Removes normalized duplicates
Drops columns with >50% missing
Fills numeric nulls with median
Fills phone nulls with mode (never median!)
Fills text nulls with most frequent value
Downloads cleaned CSV with before/after score


🛠️ Tech Stack
ComponentTechnologyUIStreamlitData ProcessingPandas, NumPyVisualizationPlotly ExpressValidationPython re (regex)DeploymentStreamlit Cloud

🚀 Getting Started
1. Clone the Repository
bashgit clone https://github.com/Samarthsj1013/Data-Quality-Checker.git
cd Data-Quality-Checker
2. Install Dependencies
bashpip install -r requirements.txt
3. Run the App
bashstreamlit run app.py
App opens at http://localhost:8501 🎉
4. Upload a Dataset
Upload any .csv, .xlsx, or .xls file and instantly get a full quality report.

📦 Requirements
txtstreamlit
pandas
numpy
plotly
openpyxl

📊 How It Works
Upload CSV/Excel
      ↓
normalize_nulls()     ← Replace hidden null-like strings with NaN
      ↓
infer_column_types()  ← Smart type detection via coercion rate
      ↓
┌─────────────────────────────────┐
│  check_nulls()                  │
│  check_duplicates()             │
│  check_data_types()             │
│  detect_outliers()              │
│  validate_emails()              │
│  validate_dates()               │
│  validate_phones()              │
│  check_consistency()            │
└─────────────────────────────────┘
      ↓
quality_score()       ← Multi-factor weighted penalty system
      ↓
generate_suggestions() ← Column-level fix recommendations
      ↓
Display Report + Charts + Auto Clean Option

📁 Project Structure
Data-Quality-Checker/
├── app.py           # Streamlit UI — all sections and charts
├── checker.py       # Core logic — all check functions
└── requirements.txt # Dependencies
app.py — UI Layer

File upload and data preview
5-column summary card (rows, cols, nulls, dups, numeric)
Quality score display with color coding
Score breakdown expander
3-column layout for missing/duplicates/outliers
4-column validation section
Correlation heatmap with strong correlation callouts
Distribution plots with stats (mean, median, std, skewness)
Scatter plot with trendline
Auto-clean with before/after score comparison

checker.py — Logic Layer

normalize_nulls(df) — Hidden null replacement
load_data(file) — CSV/Excel loader with normalization
infer_column_types(df) — Smart type inference
check_nulls(df) — Missing value analysis
check_duplicates(df) — Normalized duplicate detection
check_data_types(df, type_info) — Type mismatch table
detect_outliers(df, type_info) — IQR outlier detection
validate_emails(df) — Regex email validation
validate_dates(df, type_info) — Date parsing validation
validate_phones(df) — Phone format validation
check_consistency(df) — Value inconsistency detection
quality_score(...) — Multi-factor scoring
generate_suggestions(...) — Auto fix recommendations
auto_clean(df, type_info) — One-click cleaning
correlation_heatmap(df, type_info) — Correlation matrix
distribution_plots(df, type_info) — Numeric column list


🧪 Test Dataset
Use this messy CSV to test all features:
csvid,name,age,email,phone,signup_date,country,salary
1,Samarth,21,samarth@gmail.com,9876543210,2023-01-12,India,50000
2,Riya,twenty-two,riya@gmail,9876543211,12/02/2023,India,52000
3,Aman,23,aman123@gmail.com,,2023-03-05,India,not_available
4,Neha, ,neha@@gmail.com,9876543213,2023/04/01,IND,48000
5,John,29,john.doe@gmail.com,9876543214,2023-05-15,USA,70000
6,Samarth,21,samarth@gmail.com,9876543210,2023-01-12,India,50000
7,Kavya,-5,kavya@gmail.com,abcd123456,2023-07-21,India,45000
8,Rohit,200,rohit@gmail.com,9876543216,2023-08-10,India,9999999
What it catches:

✅ Duplicate row (rows 1 & 6 — same data, different ID)
✅ Hidden nulls (not_available, empty strings)
✅ Type mismatches ("twenty-two" in age)
✅ Outliers (age -5, 200; salary 9999999)
✅ Invalid emails (riya@gmail, neha@@gmail.com)
✅ Invalid dates (2023-09-31, not_a_date)
✅ Invalid phones (abcd123456, 98765)
✅ Consistency issues (India vs IND)


🌐 Live Demo
https://data-quality-checker13.streamlit.app
Deployed on Streamlit Cloud — free, no login required.

📄 License
MIT License — free to use, modify, and distribute.
