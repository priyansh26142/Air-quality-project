# Delhi Air Quality Analysis (2022-2025)

## Project Overview

This project analyzes historical air-quality data from the **Central Pollution Control Board (CPCB)** monitoring station at **Anand Vihar, Delhi**.

The analysis covers daily observations from **2022 to 2025** and focuses primarily on particulate matter (PM2.5 and PM10), while also investigating relationships with other pollutants and meteorological variables.

The project demonstrates a complete beginner-level Data Science workflow:

**Data Collection -> Data Cleaning -> Exploratory Data Analysis -> Correlation Analysis -> Hypothesis Testing -> Insights**

---

## Objectives

The main objectives of this project are to:

- Clean and combine multiple years of real-world CPCB air-quality data.
- Investigate missing values and data-quality issues.
- Analyze the distribution of PM2.5.
- Study yearly and monthly PM2.5 patterns.
- Examine relationships between PM2.5 and other variables.
- Analyze the relationship between PM2.5 and PM10.
- Investigate associations between PM2.5 and meteorological variables.
- Perform statistical hypothesis testing on PM2.5 measurements.

---

## Data Source

**Source:** Central Pollution Control Board (CPCB), India  
**Monitoring station:** Anand Vihar, Delhi - DPCC  
**Frequency:** 24-hour / daily data  
**Period:** 2022-2025

Four yearly datasets were downloaded and combined for the analysis.

### Dataset Size

The combined dataset contains:

- **1,461 daily observations**
- Air-pollution variables including PM2.5, PM10, NO, NO2, NOx, NH3, SO2, CO and Ozone
- Meteorological variables including temperature, relative humidity, wind speed, wind direction, solar radiation and barometric pressure

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- SciPy
- Jupyter Notebook / VS Code

---

# Data Cleaning

Real-world environmental data contained several data-quality issues.

The following steps were performed:

### 1. Combined Multiple Years

Data from 2022, 2023, 2024 and 2025 was combined into a single DataFrame.

The final combined dataset contained **1,461 daily observations**.

### 2. Timestamp Standardization

Different yearly files contained slightly different timestamp formats.

The timestamp column was converted into a consistent datetime format using Pandas.

Additional features were derived:

- Year
- Month
- Month Name

### 3. Completely Missing Columns

Several variables contained 100% missing values across the combined dataset.

These columns were removed because they contained no usable information.

### 4. Constant Column

`TOT-RF (mm)` contained only one unique value across the dataset and therefore provided no variation for analysis.

The column was removed.

### 5. Duplicate Analysis

The dataset was checked for:

- Duplicate rows
- Duplicate timestamps

No duplicate rows or timestamps were detected.

### 6. Missing-Value Investigation

Missing values were analyzed instead of being automatically removed or imputed.

For example:

- PM2.5 contained **34 missing daily observations**.
- PM10 contained **38 missing daily observations**.

Several missing observations occurred as consecutive multi-day gaps.

Because interpolating long gaps could introduce artificial pollution measurements, these values were retained as missing (`NaN`) for the main analysis.

### 7. Invalid-Value Checking

Core pollutants were checked for negative concentration values.

No negative values were detected for:

- PM2.5
- PM10
- NO
- NO2
- SO2
- CO
- Ozone

### 8. Outlier Investigation

Potential PM2.5 outliers were investigated using the **Interquartile Range (IQR)** method.

Potential outliers were not automatically removed because unusually high pollution readings may represent genuine pollution events rather than measurement errors.

---

# Exploratory Data Analysis

## PM2.5 Distribution

The PM2.5 histogram showed a **right-skewed distribution**.

Most daily observations were concentrated toward the lower part of the overall range, while a smaller number of observations showed very high PM2.5 concentrations.

This supports investigating extreme observations rather than automatically removing them.

---

## Yearly PM2.5 Analysis

Average daily PM2.5 concentration by year:

| Year | Average PM2.5 (µg/m³) |
|---|---:|
| 2022 | 124.15 |
| 2023 | 127.87 |
| 2024 | 136.04 |
| 2025 | 122.06 |

Among the four years analyzed:

- **2024 had the highest average PM2.5 concentration.**
- **2025 had the lowest average PM2.5 concentration.**

The four-year period did not show a consistent increasing or decreasing pattern. Average PM2.5 increased through 2024 and decreased in 2025.

---

## Monthly PM2.5 Pattern

The analysis showed substantial monthly variation.

Selected monthly averages:

| Month | Average PM2.5 (µg/m³) |
|---|---:|
| January | 235.89 |
| February | 132.99 |
| July | 42.21 |
| October | 137.88 |
| November | 263.82 |
| December | 237.15 |

**November recorded the highest four-year monthly average**, while **July recorded the lowest**.

The results indicate a strong seasonal pattern in PM2.5 concentrations.

---

# PM2.5 and PM10 Relationship

A scatterplot was used to investigate the relationship between PM2.5 and PM10.

The calculated Pearson correlation was approximately:

**r = 0.836**

This represents a **strong positive linear relationship**.

Higher PM2.5 concentrations generally occurred alongside higher PM10 concentrations.

Correlation represents association and does not by itself establish causation.

---

# Correlation Analysis

PM2.5 correlations with selected variables were:

| Variable | Correlation with PM2.5 |
|---|---:|
| PM10 | +0.836 |
| CO | +0.503 |
| NO2 | +0.367 |
| Relative Humidity | +0.161 |
| SO2 | +0.013 |
| Wind Speed | -0.152 |
| Ozone | -0.245 |
| Temperature | -0.569 |

### Key Observations

- PM10 showed the strongest positive correlation with PM2.5.
- CO showed a moderate positive relationship with PM2.5.
- Temperature showed a moderately strong negative relationship with PM2.5.
- SO2 showed almost no linear relationship with PM2.5 in this dataset.

These correlations represent statistical associations and should not be interpreted as proof of causation.

---

# Hypothesis Testing

A **Welch's independent two-sample t-test** was performed to compare daily PM2.5 concentrations between 2022 and 2025.

### Hypotheses

**Null Hypothesis (H0):**

The population mean PM2.5 concentration is equal in 2022 and 2025.

**Alternative Hypothesis (H1):**

The population mean PM2.5 concentration differs between 2022 and 2025.

### Results

- Mean PM2.5 (2022): **124.15 µg/m³**
- Mean PM2.5 (2025): **122.06 µg/m³**
- t-statistic: **0.307**
- p-value: **0.759**
- Significance level: **0.05**

Since:

**p-value > 0.05**

the null hypothesis was **not rejected**.

### Interpretation

At the 5% significance level, the test did not provide sufficient evidence to conclude that mean daily PM2.5 differed between 2022 and 2025.

---

# Key Findings

1. PM2.5 concentrations showed substantial day-to-day and monthly variation.

2. The PM2.5 distribution was right-skewed and contained several high-concentration observations.

3. 2024 recorded the highest annual average PM2.5 among the four years analyzed.

4. Strong monthly variation was observed, with the highest average PM2.5 in November and the lowest in July.

5. PM2.5 and PM10 had a strong positive correlation of approximately **0.84**.

6. Temperature showed a negative association with PM2.5, with a correlation of approximately **-0.57**.

7. The difference in mean daily PM2.5 between 2022 and 2025 was not statistically significant in the Welch t-test at the 5% significance level.

---

# Project Structure

```text
delhi-air-quality-analysis/
|
|-- data/
|   |-- raw/
|   |   |-- 2022.csv
|   |   |-- 2023.csv
|   |   |-- 2024.csv
|   |   `-- 2025.csv
|   |
|   `-- cleaned/
|       `-- air_quality_cleaned_2022_2025.csv
|
|-- notebooks/
|   |-- 01_data_cleaning.ipynb
|   `-- 02_exploratory_data_analysis.ipynb
|
|-- charts/
|
|-- report/
|
|-- requirements.txt
|-- .gitignore
`-- README.md
```

---

# Limitations

- The analysis represents one monitoring station: Anand Vihar, Delhi.
- Some variables contain missing observations.
- Several missing PM2.5 and PM10 observations occur in consecutive periods.
- Correlation does not establish causation.
- Daily air-quality observations form a time series, so consecutive measurements may not be statistically independent.
- The independent t-test is used as an introductory statistical comparison and does not model temporal dependence or seasonality.

---

# Future Work

Possible extensions include:

- Comparing multiple CPCB monitoring stations across Delhi.
- Comparing air quality across multiple Indian cities.
- Performing detailed seasonal analysis.
- Investigating lagged relationships between weather and pollution.
- Developing an interactive Power BI dashboard.
- Applying time-series forecasting methods.
- Building machine-learning models for PM2.5 prediction.

---

## Author

**Priyansh Jain**

Data Science Project
