# Healthcare Analytics

### Patient profiles, admission patterns, and billing insights

A Python data analytics project that explores healthcare records and translates the analysis into business insights for hospital management. The project combines a Jupyter notebook with an HTML dashboard to examine patient demographics, medical conditions, treatment billing, and insurance coverage.

**Python · Pandas · NumPy · Matplotlib · Jupyter · HTML · CSS · JavaScript · Chart.js**

[Explore the notebook](Healthcare.ipynb) · [Download the dashboard](healthcare_dashboard.html) · [View the dataset](healthcare_dataset.csv)

## Business objective

Use healthcare records to understand patient demand, monitor billing patterns, and identify groups of admissions for further review. The analysis supports questions about emergency department capacity, insurance coverage, and high-billing cases.

## Dataset at a glance

| Attribute | Value |
|---|---|
| Original dataset | 55,500 rows × 15 columns |
| Duplicate rows removed | 534 |
| Records after duplicate removal | 54,966 |
| Admission dates | 8 May 2019 – 7 May 2024 |
| Medical conditions | 6 |
| Insurance providers | 5 |
| Missing values in the input | 0 |
| Derived fields | `Length_of_stay`, `Admission_month` |

Records include age, gender, blood type, medical condition, hospital, doctor, admission type, admission and discharge dates, insurance provider, billing amount, medication, and test results.

## Verified results

These figures were checked against the supplied CSV using the notebook's cleaning rules. Billing values are shown without a currency symbol because the CSV does not specify one.

| Metric | Result |
|---|---:|
| Total recorded billing after cleaning | 1,406,829,297.78 |
| Average billing per record | 25,594.54 |
| Average age | 51.54 years |
| Age range | 13–89 years |
| Average billing for ages 60+ | 25,563.59 |
| Emergency admissions | 18,102 |
| Records above the 90th billing percentile | 5,497 |
| 90th-percentile billing threshold | 45,160.26 |
| Emergency admissions with abnormal test results | 6,038 |

### Findings

- **Medical-condition counts are closely balanced:** Arthritis has the highest count (9,218), followed by Diabetes (9,216); Asthma has the lowest (9,095).
- **Insurance shares are similar:** Cigna leads with 11,139 records, while Aetna has 10,822. The five providers each account for approximately 19.7%–20.3% of records.
- **Senior and overall average billing are close:** The average for ages 60+ is 30.95 lower than the overall mean. This comparison does not establish what drives billing differences.
- **Emergency volume varies by calendar month:** July has the highest pooled count (1,573), and February the lowest (1,452). These totals combine all years rather than representing individual year-months.
- **The review groups are substantial:** 5,497 records exceed the 90th billing percentile, and 6,038 records meet both the emergency-admission and abnormal-test conditions.

## Key analyses

| Business area | Analysis | Management relevance |
|---|---|---|
| Medical conditions | Compare admission counts by medical condition | Understand the distribution of recorded conditions |
| Patient demographics | Examine the age distribution and average age | Describe the population represented in the dataset |
| Billing trends | Track average billing by admission month | Monitor changes in recorded billing amounts |
| Age and billing | Plot age against billing for a reproducible sample; calculate average billing for patients aged 60+ | Explore billing differences across patient ages |
| Insurance coverage | Compare admission counts and shares by insurance provider | Understand the insurance mix |

## Ad-hoc business analyses

- **Emergency demand:** Count emergency admissions by calendar month. This groups the same month across all years to examine seasonal volume.
- **High-billing admissions:** Identify records with billing amounts above the dataset's 90th percentile.
- **Cases for review:** Identify emergency admissions with abnormal test results and count the matching records.

## Data preparation

The notebook inspects the dataset, checks missing values and duplicates, and prepares the fields used in the analysis:

- Remove duplicate rows.
- Standardize patient names by trimming whitespace and applying title case.
- Replace negative billing amounts with the mean billing amount, following the tutorial approach.
- Convert admission and discharge dates to datetime values.
- Calculate length of stay from the difference between discharge and admission dates.
- Create an admission-month field for monthly billing analysis.

## Repository files

| File | Purpose |
|---|---|
| [Healthcare.ipynb](Healthcare.ipynb) | Data inspection, cleaning, analysis, and visualizations |
| [healthcare_dataset.csv](healthcare_dataset.csv) | Input healthcare records |
| [healthcare_dashboard.html](healthcare_dashboard.html) | Browser-based dashboard |
| [.gitignore](.gitignore) | Excludes local environments and temporary files |

## Executive dashboard

The HTML dashboard is titled **Patient Care & Revenue Intelligence** and includes:

- Eight overview KPI cards.
- An executive summary and management takeaways.
- Medical-condition counts and insurance-provider shares.
- Selected monthly average billing points.
- Overall versus senior average billing.
- Emergency admissions by calendar month.
- High-billing and abnormal emergency review groups.
- Hover tooltips, category highlighting, a reset button, and a responsive layout.

**Current interaction scope:** Medical-condition and insurance selectors highlight their corresponding chart categories. They do not filter individual records, apply combined filters, or recalculate KPI cards. Gender and date filters are not implemented.

**Dependencies:** The dashboard loads Chart.js 4.4.4 and Google Fonts from external services. Although delivered as one HTML file, it requires internet access for charts and fonts and is not fully self-contained offline.

## Run locally

### 1. Clone the repository

```bash
git clone https://github.com/RajolKumar2003/Healthcare-Analytics.git
cd Healthcare-Analytics
```

### 2. Set up Python

The project was developed using Python 3.14. In Windows PowerShell, run:

```powershell
py -3.14 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install pandas numpy matplotlib ipykernel
```

### 3. Open the notebook

1. Open the repository folder in VS Code.
2. Install the Microsoft **Python** and **Jupyter** extensions.
3. Open `Healthcare.ipynb`.
4. Select the `.venv` Python environment as the notebook kernel.
5. Run the cells in order, with `healthcare_dataset.csv` in the same folder.

### 4. Open the dashboard

Open `healthcare_dashboard.html` in a web browser with an internet connection. To view it from GitHub, download the HTML file first; GitHub's file viewer displays its source.

## Interpretation and limitations

- Counts represent records or admissions; they do not establish the number of unique patients.
- Billing amounts represent recorded charges, rather than confirmed revenue collected. The analysis does not establish a currency.
- Replacing negative billing amounts with the overall mean is a simplifying assumption that affects billing summaries. A production analysis would investigate those records first.
- The scatter plot uses a sample of 1,000 records with a fixed random seed. Visual patterns alone do not establish causation.
- Abnormal emergency records are an analytical review group, not a clinical triage recommendation.
- Results describe this dataset. Its provenance and representativeness should be verified before applying findings to a real hospital.
- The current dashboard uses dollar symbols, but the CSV does not establish a currency. Its monthly trend contains only the first and last five monthly values from the notebook's truncated output, rather than all 61 months.
- Some dashboard narrative goes beyond the notebook's evidence: the analysis does not establish billing drivers, absence of inflation, or reimbursement risk. Those statements should not be treated as validated findings.

## Future improvements

- Populate the dashboard with all 61 monthly billing values.
- Add record-level filtering with recalculated KPIs and charts.
- Use currency-neutral billing labels unless dataset provenance establishes the currency.
- Add pinned dependencies and make chart assets available locally for offline use.

## Learning context

This project follows ConsoleFlare's **“Build a Data Analytics Project from scratch | Healthcare Case Study”** tutorial. It is presented as a learning and portfolio project with the analysis workflow and business questions documented here.

## Author

**Rajol Kumar**  
M.Sc. in Mathematics and Scientific Computing, NIT Warangal  
[GitHub profile](https://github.com/RajolKumar2003)
