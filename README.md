# Job Application Analysis

A data analysis project exploring salary, application volume and job visibility across the **10 most-applied job titles**.

The project combines multiple datasets, handles missing values, converts salaries to hourly rates and presents findings through charts.

## Research Question

How do salary, application volume and job visibility vary across the top 10 most-applied job titles?

## Repository Files

| File or Folder | Description |
| --- | --- |
| [Job application.ipynb](Job%20application.ipynb) | Notebook containing data preparation, analysis and visualisations. |
| [Job application.pptx](Job%20application.pptx) | Presentation summarising the workflow and findings. |
| [Job application Dataset/](Job%20application%20Dataset/) | Dataset folder containing four CSV files and one Excel file. |

The dataset folder is at the **same level** as the notebook and presentation.

### Dataset Files

- `Job application Dataset/postings1.csv`
- `Job application Dataset/postings2.csv`
- `Job application Dataset/postings3.csv`
- `Job application Dataset/postings4.csv`
- `Job application Dataset/postings5.xlsx`

## Project Workflow

1. Load the five dataset files.
2. Inspect missing values, column types and categorical values.
3. Remove unrelated, redundant and highly incomplete columns.
4. Merge the cleaned `postings1`–`postings4` tables using `job_id`.
5. Inspect `postings5`, which is excluded from the merge because it duplicates the role of `postings1`.
6. Handle missing values using field-specific rules.
7. Identify the top 10 job titles by total recorded applications.
8. Convert maximum salaries to hourly equivalents.
9. Compare salaries, views and applications through visualisations.

The selected top-10 subset contains **1,489 job postings**, according to the notebook's saved output.

## Data Preparation

The notebook applies these treatments:

| Field | Treatment |
| --- | --- |
| Company name and company ID | Fill missing values with `Unknown` |
| Experience level | Fill missing values with `Unknown` |
| Views and applications | Fill missing values with `0` |
| Maximum salary | Fill missing values using the mean within each job title |
| Pay period | Apply salary-based rules where values are missing |
| Currency | Fill missing values with `USD` |
| Compensation type | Fill missing values with `BASE_SALARY` |
| Remote status | Treat missing values as `False` |

These treatments are analysis assumptions and may affect the findings.

### Hourly Salary Conversion

Salary values are converted using an assumption of **40 working hours per week**.

| Pay Period | Conversion |
| --- | --- |
| Yearly | Salary ÷ 2,080 |
| Monthly | Salary ÷ 173.33 |
| Weekly | Salary ÷ 40 |
| Biweekly | Salary ÷ 80 |
| Hourly | No conversion |

The salary analysis uses **maximum advertised salary**, including imputed values. It does not measure actual employee earnings.

## Visualisations

The notebook includes:

- Line chart comparing total views and applications by job title
- Bar chart comparing average maximum hourly salary
- Boxplot comparing salary distributions by experience level
- Histogram showing the hourly salary distribution
- Pie chart showing application share
- Scatter plot comparing hourly salary and application volume

The experience-level boxplot applies a group-specific **1.0 × IQR filter**, as implemented in the notebook. The overall salary histogram retains outliers.

## Recorded Salary Results

Average maximum hourly salaries for the selected titles:

| Job Title | Average Maximum Hourly Salary |
| --- | ---: |
| Senior Software Engineer | $92.01 |
| Software Engineer | $78.13 |
| Data Engineer | $55.24 |
| Full Stack Engineer | $55.00 |
| DevOps Engineer | $49.08 |
| Project Manager | $46.11 |
| Business Analyst | $32.00 |
| Recruiter | $28.83 |
| Data Analyst | $28.50 |
| Administrative Assistant | $17.23 |

These values come from the notebook's saved outputs and reflect its cleaning and conversion assumptions.

## Main Findings

- Senior Software Engineer and Software Engineer have the highest average maximum hourly salaries among the selected titles.
- Data Analyst accounts for over 20% of applications within the top-10 subset, according to the notebook's chart interpretation.
- Views and applications provide different measures of engagement.
- The salary-versus-applications chart does not show a clear linear relationship.
- Higher advertised salary alone does not explain application volume.

The findings describe patterns in this dataset. They do not establish that salary or visibility causes changes in applications.

## Tools Used

- Python
- pandas
- NumPy
- Matplotlib
- openpyxl
- Jupyter Notebook

## How to Run

1. Download or clone the repository, including the dataset folder.
2. Install the required packages:

   ```bash
   python -m pip install pandas numpy matplotlib openpyxl notebook
   ```

3. Replace the notebook's absolute Windows paths with these relative paths:

   ```python
   from pathlib import Path
   import pandas as pd

   dataset_dir = Path("Job application Dataset")

   postings1 = pd.read_csv(
       dataset_dir / "postings1.csv",
       low_memory=False
   )
   postings2 = pd.read_csv(dataset_dir / "postings2.csv")
   postings3 = pd.read_csv(dataset_dir / "postings3.csv")
   postings4 = pd.read_csv(dataset_dir / "postings4.csv")
   postings5 = pd.read_excel(dataset_dir / "postings5.xlsx")
   ```

4. Start Jupyter from the repository folder:

   ```bash
   jupyter notebook
   ```

5. Open `Job application.ipynb` and run the cells in order.

## Limitations and Future Improvements

- Salary and application fields have substantial missing data.
- Missing applications are treated as zero, which may undercount activity.
- Salary imputation and pay-period rules may distort comparisons.
- Filling missing currency with USD does not convert existing non-USD salaries.
- Total applications depend partly on the number of postings for each title.
- Future analysis could compare applications per posting, check merge-key uniqueness and separate observed salaries from imputed values.

## Author

**Yan Myoe Naing**  
Applied AI and Analytics, Singapore Polytechnic
