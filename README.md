# U.S. High School Educational Inequality Analysis

This project examines whether socioeconomic characteristics and school enrollment can predict average ACT or SAT-equivalent performance across U.S. high schools.

---

## Project Overview

This project investigates the relationship between socioeconomic conditions and academic performance in U.S. high schools. School performance is measured using average ACT scores or SAT-equivalent scores from EdGap. School enrollment from the National Center for Education Statistics (NCES) is added as an additional predictor to examine whether school size provides useful information beyond socioeconomic factors.

- Objective: Determine how well socioeconomic characteristics and school enrollment predict average ACT performance.

- Domain: Education / Educational Inequality

- Key Techniques: Data cleaning, missing-value imputation, exploratory data analysis, multiple linear regression, polynomial regression, model comparison, and residual analysis.

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

- Source: EdGap and NCES Common Core of Data

- Description: The data are from the 2016–2017 school year and include school ACT/SAT-equivalent performance, unemployment rate, adult college attainment, median household income, free/reduced-price lunch participation, and school enrollment. After data preparation, the final analysis contains 7,227 high schools from 20 states.

- License: See the original data sources for applicable licensing and usage information.

---

## Analysis

The full analysis is contained in `code/Education.ipynb`.

The notebook should be run from top to bottom to reproduce the results. The analysis includes data cleaning and merging, missing-value imputation, exploratory data analysis, log transformation of school enrollment, multiple linear regression, evaluation of a quadratic income model, and comparison of model performance.

The final regression model uses unemployment rate, adult college attainment, free/reduced-price lunch participation, and log-transformed school enrollment to predict average ACT performance.

---

## Results

The final model explains approximately 63.1% of the variation in average ACT scores and has a mean absolute error of approximately 1.14 ACT points.

Higher unemployment and free/reduced-price lunch participation are associated with lower ACT scores, while higher adult college attainment is associated with higher scores. School enrollment is also statistically significant, although its relationship with ACT performance is weaker than the socioeconomic predictors.

A quadratic income model slightly improves model performance, increasing (R^2) from 0.631 to 0.641, but the improvement in predictive accuracy is small. The simpler model is therefore retained for easier interpretation.

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

This project is licensed under the MIT License - see the LICENSE file for details.

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
