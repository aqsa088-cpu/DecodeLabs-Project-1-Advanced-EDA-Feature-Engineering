# Student Performance — Advanced EDA & Feature Engineering

## Project Overview

This project performs **Advanced Exploratory Data Analysis (EDA) and Feature Engineering** on the Students Performance dataset. The goal is to transform raw data into a mathematically clean dataset ready for machine learning algorithms by handling missing data, detecting and neutralizing outliers, and engineering new predictive features.

---

## Dataset

**File:** `StudentsPerformance.csv`  
**Source:** Packaged as `Student Performance.zip`  
**Size:** 1000 rows × 8 columns  

### Features

| Column | Type | Description |
|--------|------|-------------|
| `gender` | Categorical | Student's gender (female / male) |
| `race/ethnicity` | Categorical | Ethnic group (group A–E) |
| `parental level of education` | Categorical | Highest parental education level |
| `lunch` | Categorical | Lunch type — socioeconomic indicator (standard / free/reduced) |
| `test preparation course` | Categorical | Whether prep course was completed (none / completed) |
| `math score` | Numerical (int) | Math test score (0–100) |
| `reading score` | Numerical (int) | Reading test score (0–100) |
| `writing score` | Numerical (int) | Writing test score (0–100) |

---

## Notebook Structure

### 1. Data Loading & Initial Exploration
- Extracts the dataset from the ZIP archive
- Loads data into a pandas DataFrame
- Displays first 5 rows, dataset info, and descriptive statistics
- Counts unique values for all categorical columns

### 2. Data Cleaning & Preprocessing
- Renames all column names to `snake_case` (e.g., `math score` → `math_score`)
- Strips special characters from column names for compatibility

### 3. Missing Value Handling
- Checks all columns for null values
- **Result:** No missing values found — dataset is complete (1000/1000 non-null per column)
- Imputation (Mean / Median / KNN) is correctly skipped with a printed explanation

### 4. Outlier Detection & Neutralization
Uses **Z-Score method** (threshold = 3) to identify and cap outliers via Winsorization:

| Column | Outliers Found | Action |
|--------|---------------|--------|
| `math_score` | 4 (scores: 0, 8, 18, 19) | Capped to non-outlier range |
| `reading_score` | 4 (scores: 17, 23, 24, 24) | Capped to non-outlier range |
| `writing_score` | 4 (scores: 10, 15, 19, 22) | Capped to non-outlier range |

### 5. Feature Engineering
Five new predictive features engineered from existing columns:

| New Feature | Description |
|-------------|-------------|
| `average_score` | Mean of math, reading, and writing scores |
| `total_score` | Sum of all three scores |
| `has_test_prep` | Binary flag — 1 if prep course completed, else 0 |
| `performance_category` | Categorical label: `high` (≥80), `medium` (≥60), `low` (<60) |
| `parental_education_numeric` | Ordinal encoding of parental education (0=some high school → 5=master's) |

---

## Key Skills & Libraries Used

- **Python** — core language
- **Pandas** — data loading, cleaning, manipulation
- **NumPy** — numerical operations, outlier capping
- **SciPy** (`scipy.stats.zscore`) — Z-score outlier detection
- **re** — regular expressions for column name cleaning
- **zipfile / os** — file extraction and path management

---

## How to Run

1. Upload `Student Performance.zip` to `/content/` in Google Colab
2. Open `Student_Performance.ipynb` in Google Colab
3. Run all cells from top to bottom (`Runtime → Run all`)

> **Note:** The notebook includes a fallback data-loading block in the cleaning cell to handle kernel restarts gracefully.

---

## Output

After running all cells, the final DataFrame contains **13 columns** (8 original + 5 engineered) with all outliers neutralized and column names standardized, ready for downstream machine learning tasks.

---

## Project Requirements Checklist

- [x] Handle missing data via statistical imputation (Mean/Median/KNN)
- [x] Identify and neutralize outliers using Z-Scores or IQR
- [x] Engineer at least 3 new predictive features from existing columns
