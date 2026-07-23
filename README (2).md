# Data Analyst Jobs — Excel Data Cleaning, Pivot Tables & Dashboard

An end-to-end Excel project analyzing 648 real-world Data Science job postings (scraped from Glassdoor) to uncover salary trends, in-demand skills, and hiring patterns by role, state, and sector.

## 📊 Project Overview

This project takes a raw jobs dataset and turns it into a decision-ready dashboard using only native Excel tools — Find & Replace, formulas, PivotTables, PivotCharts, and Slicers. No external BI tools were used, to demonstrate core spreadsheet-analyst skills.

## 🗂️ Dataset

- **Source:** [Data Scientist Jobs dataset, Kaggle](https://www.kaggle.com/) (Glassdoor job postings)
- **Size:** 660 rows × 27 columns
- **Fields:** job title, salary range, company rating, size, industry, sector, revenue, location, and binary flags for skills mentioned in the posting (Python, Excel, AWS, Tableau, Spark, Hadoop, Big Data)

## 🛠️ Tools Used

- Microsoft Excel (Formulas, Find & Replace, PivotTables, PivotCharts, Slicers)

## 🧹 Data Cleaning

All cleaning was done on a dedicated `Work Sheet` tab, keeping the original `Cleaned_DS_Jobs` tab untouched as a raw-data reference.

| # | Step | Why |
|---|------|-----|
| 1 | Removed duplicate rows | Duplicate postings would inflate counts and skew averages |
| 2 | Converted `Revenue` to a consistent text/category type | Kept revenue bands (e.g. `$100 to $500 million`) uniform for grouping |
| 3 | Converted blank / `-1` / `N/A` entries in `Industry` to `"Unknown"` | Made missing data an explicit, filterable category instead of silent blanks |
| 4 | Converted numeric-looking text fields to true number format | Required for SUM/AVERAGE and PivotTable calculations to work correctly |
| 5 | Standardized `Size` and `Revenue` blanks/`N/A` to `"Unknown"` | One consistent label instead of a mix of blanks and inconsistent "Unknown" spellings |
| 6 | Standardized `job_simp` and `seniority` missing values to true blanks | Previous placeholder text was showing up as a fake category in PivotTables — corrected so blanks are excluded from grouped analysis |
| 7 | Deleted the `Salary Estimate` column | Original text (e.g. `$56K-$97K`) was corrupted during scraping; the dataset already includes clean, derived `min_salary`, `max_salary`, and `avg_salary` columns, making the raw column redundant |
| 8 | Converted `Rating`, `min_salary`, `max_salary`, `avg_salary`, `same_state`, `company_age` to number format | Ensures correct sorting, averaging, and PivotTable aggregation |

**Known limitation:** the State pivot table currently groups on the original `job_state` field rather than the whitespace-trimmed version, so a few states appear with a leading space in the raw pivot data (values are still correct, just formatted inconsistently) — a good next cleanup pass.

## 📈 Pivot Tables

Five PivotTables were built on the cleaned data (`Pivot Table` tab), each isolating a different angle on the job market:

1. **Average salary & posting count by role** (`job_simp`)
2. **Skill demand by role** — % of postings per role requiring Python, Excel, AWS, Tableau, Spark, Hadoop, Big Data
3. **Posting count & average salary by state**
4. **Average company rating by company size**
5. **Posting count & average salary by sector**

## 📊 Dashboard

The `Dashboard` tab brings all five views together into column charts, with **Slicers** for `job_simp`, `job_state`, and `Sector` connected across every chart — so filtering to a single role or sector updates the entire dashboard at once.

## 🔑 Key Insights

**Salary by role** (avg salary in $K, n = postings)

| Role | Avg Salary | Postings |
|---|---|---|
| Manager | $137.9K | 7 |
| Director | $127.0K | 3 |
| Data Scientist | $125.4K | 436 |
| MLE | $118.1K | 34 |
| Analyst | $115.5K | 55 |
| Data Engineer | $114.1K | 45 |
| **Overall average** | **$123.7K** | **648** |

- **Data Scientist roles dominate the market** — 67% of all postings (436 of 648) — so market-wide averages are effectively data-scientist-driven.
- **Python is the single most requested skill**, appearing in 72.5% of all postings, well ahead of Excel (44.8%) and Tableau (18.7%).
- **Skill demand varies sharply by role:** Data Engineer postings lean hardest on Python (82.2%), AWS (55.6%), and Spark (44.4%) — the classic pipeline-and-cloud stack — while Analyst postings favor Excel (54.5%) and Tableau (49.1%) over cloud/big-data tools.
- **Company size and rating have a striking outlier:** companies with an "Unknown" size average a **1.25 rating**, dramatically lower than every known size bracket (which cluster between 3.6–4.0). This likely reflects smaller or less-established employers with fewer, harsher reviews rather than a true size effect — worth flagging as a caveat, not a trend.
- **Geographic concentration:** California accounts for the most postings (154, ~24% of the dataset) but isn't the highest-paying — Washington DC ($139.3K, n=26) and New York ($136.3K, n=52) both out-pay it on average.
- **By sector, Information Technology posts the most jobs** (178) at a moderate average salary ($118.8K), while Business Services posts fewer jobs (120) but pays higher on average ($129.9K).

## 📁 Repository Structure

```
data-analyst-jobs-excel-analysis/
├── data/
│   └── Cleaned_DS_Jobs.csv
├── excel/
│   └── Cleaned_DS_Jobs.xlsx
├── screenshots/
│   └── dashboard.png
└── README.md
```

## 🚀 How to Use

1. Open `Cleaned_DS_Jobs.xlsx`
2. Go to the `Dashboard` tab
3. Use the Slicers at the top to filter by job role, state, or sector — all charts update together
