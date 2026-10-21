# U.S. High School Educational Inequality Analysis

---

## Project Overview

This project investigates whether socioeconomic conditions are associated with academic performance across U.S. high schools. School performance is measured using average ACT scores or SAT-equivalent scores from EdGap. Socioeconomic characteristics such as unemployment, college attainment, household income, and free/reduced-price lunch participation are examined as potential predictors of school performance.

In addition to the socioeconomic variables provided by EdGap, school enrollment from the National Center for Education Statistics (NCES) is added as an additional predictor. The goal is to determine how well socioeconomic characteristics and school size can predict differences in average ACT performance.

- **Objective:** Determine whether socioeconomic factors and school enrollment can predict ACT/SAT performance in U.S. high schools.
- **Domain:** Education / Educational Inequality
- **Key Techniques:** Data cleaning, dataset merging, missing-value imputation, exploratory data analysis, visualization, log transformation, OLS regression, polynomial regression, residual analysis, and model comparison.

---

## Project Structure

```text
├── data/                                      # Raw and processed data
│   ├── raw/
│   │   ├── EdGap_data.xlsx                    # School performance and socioeconomic data
│   │   ├── ccd_sch_029_1617_w_1a_11212017.csv # NCES school information data
│   │   └── enrollment_dataset.csv             # NCES school enrollment data
│   └── clean_data/
│       └── education_clean.csv                # Final cleaned dataset
├── code/                                      # Jupyter notebooks and Python scripts
│   └── Education.ipynb                       # Main notebook
├── reports/                                   # Generated reports and visualizations
├── requirements.txt                           # Dependencies
└── README.md                                  # Project documentation
```

---

## Data

- **Sources:**
  - EdGap.org
  - National Center for Education Statistics (NCES), Common Core of Data Public School Universe Survey

- **Source Links:**
  - https://www.edgap.org/#5/37.892/-95.977
  - https://nces.ed.gov/ccd/pubschuniv.asp

- **School Year:** 2016–2017
- **Final Analysis Dataset:** 7,227 high schools
- **Geographic Coverage:** 20 U.S. states

- **Description:** The main variables used in the analysis are:
  - `average_act`: average ACT score or SAT-equivalent score
  - `rate_unemployment`: census-tract unemployment rate
  - `percent_college`: percentage of adults with a college degree
  - `percent_married`: percentage of children living in married-couple families
  - `median_income`: median household income
  - `percent_lunch`: percentage of students receiving free or reduced-price lunch
  - `enrollment`: total school enrollment
  - `log_enrollment`: log-transformed school enrollment
  - `state`: state where the school is located
  - `school_type`: type of school
  - `school_level`: school grade level
  - `charter`: charter-school status

### Data Preparation

The EdGap, NCES school information, and NCES enrollment datasets were first loaded and inspected for data types, missing values, invalid values, and available columns.

Only variables relevant to the analysis were retained. Column names were renamed using clear lowercase and `snake_case` formatting.

The datasets use the NCES `NCESSCH` identifier as the common school key. Because the identifier was stored in different formats across the datasets, each ID was standardized as a 12-digit string before merging.

The EdGap dataset was used as the base dataset and joined with the NCES school information and enrollment datasets using left joins.

Several additional cleaning steps were performed:

- Invalid negative ACT scores were replaced with missing values.
- Invalid negative free/reduced-price lunch percentages were replaced with missing values.
- Only schools classified as high schools were retained.
- Duplicate rows were checked.
- Observations with missing ACT scores were removed.
- Missing numerical predictor values were estimated using `IterativeImputer`.
- School enrollment was log-transformed using `log(1 + enrollment)` because enrollment was strongly right-skewed.
- The final cleaned dataset was exported to `data/clean_data/education_clean.csv`.

### Exploratory Data Analysis

Exploratory analysis was used to examine relationships between school performance and the socioeconomic predictors.

The analysis included:

- Pair plots with regression lines
- Summary statistics
- Missing-value analysis
- Geographic distribution of schools
- Correlation analysis
- Boxplots for identifying outliers
- Comparison of raw and log-transformed enrollment

The correlation analysis showed that free/reduced-price lunch participation had the strongest relationship with average ACT score, with a correlation of approximately **-0.78**.

Other relationships included:

- Unemployment rate: approximately **-0.43**
- Percentage of adults with a college degree: approximately **0.46**
- Median household income: approximately **0.46**
- Log enrollment: approximately **0.18**

The data also showed substantial correlations among several socioeconomic predictors, suggesting that some variables contain overlapping information.

---

## Analysis

The complete data preparation and statistical analysis workflow is contained in `code/Education.ipynb`.

The main analysis uses ordinary least squares regression to predict average ACT scores from socioeconomic characteristics and school enrollment.

### Baseline Model

The initial regression model included:

- Unemployment rate
- College attainment
- Median household income
- Free/reduced-price lunch percentage
- Log-transformed enrollment

The baseline model explained approximately **63.1%** of the variation in average ACT scores.

Median household income was not statistically significant when included only as a linear term, while unemployment, college attainment, free/reduced-price lunch participation, and log enrollment were statistically significant.

### Quadratic Model

Exploratory analysis suggested that the relationship between household income and ACT performance was nonlinear. A quadratic income term was therefore added.

The quadratic model produced:

- **R-squared:** 0.641
- **Mean Absolute Error:** 1.119 ACT points

Both the linear and quadratic median-income terms were statistically significant.

### Final Model

Although the quadratic model provided a slightly better statistical fit, the improvement in predictive performance was relatively small. A simpler four-predictor model was therefore selected as the final model.

The final model includes:

- Unemployment rate
- Percentage of adults with a college degree
- Free/reduced-price lunch percentage
- Log-transformed school enrollment

The final model produced:

- **R-squared:** 0.631
- **Mean Absolute Error:** 1.137 ACT points

All four predictors were statistically significant.

An ANOVA comparison showed that the quadratic model was statistically better than the simpler model, but the practical improvement in prediction accuracy was small. The simpler model was retained because it provides nearly the same predictive performance with fewer terms and a more straightforward interpretation.

---

## Results

The analysis provides evidence that socioeconomic conditions are strongly associated with high-school ACT performance.

Higher unemployment rates and higher percentages of students receiving free or reduced-price lunch were associated with lower average ACT scores. In contrast, higher levels of adult college attainment were associated with higher average ACT scores.

School enrollment, the additional predictor introduced in this project, also had a statistically significant positive relationship with ACT performance, although its relationship was weaker than the major socioeconomic predictors.

The final model explained approximately **63.1% of the variation in average ACT scores**, with an average prediction error of approximately **1.14 ACT points**.

One important limitation is the coverage of the EdGap dataset. Although the final analysis includes more than 7,000 schools, these schools represent only 20 states and therefore do not fully represent all U.S. high schools. In addition, the available predictors represent only a limited set of socioeconomic and school characteristics. Other factors not included in the dataset may also influence academic performance.

The relationships identified in this project should therefore be interpreted as associations rather than causal effects.

---

## Analysis Files

All data preparation, missing-value imputation, exploratory analysis, visualization, and regression modeling are performed in:

- [`code/Education.ipynb`](code/Education.ipynb)

Clean dataset:

- [`data/clean_data/education_clean.csv`](data/clean_data/education_clean.csv)

---

## Authors

- [@PatrickPhan](https://github.com/tphan356)

---

## License

This project is licensed under the MIT License.

---

## Requirements

This project was developed in Python using Jupyter Notebook. The main libraries used are:

- pandas
- NumPy
- Matplotlib
- Seaborn
- DuckDB
- Plotly
- scikit-learn
- statsmodels
- openpyxl

All required Python packages are listed in:

`requirements.txt`

---

## Acknowledgements

- EdGap.org
- National Center for Education Statistics (NCES)
- Common Core of Data (CCD)
- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- DuckDB
- Plotly
- scikit-learn
- statsmodels
