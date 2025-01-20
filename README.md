# Yulu Bike Sharing Hypothesis Testing

![Yulu Banner](https://cdn.bikedekho.com/upload/newsimages/300X520/cover_6450b34e63c5d-300X520.png)

## Introduction
Yulu, a leading micro-mobility service provider, seeks to analyze the factors influencing the demand for shared electric cycles. This project uses statistical hypothesis testing and exploratory data analysis to provide actionable insights for demand forecasting and strategic planning.

---

## Features of the Project
1. **Exploratory Data Analysis (EDA)**:
   - Visualize and summarize data.
   - Detect outliers and anomalies.
   - Analyze relationships between variables.
2. **Hypothesis Testing**:
   - Evaluate the effect of working days on bike rentals.
   - Assess seasonal and weather-based differences in rentals.
   - Determine dependencies between weather and season.
3. **Statistical Methods**:
   - 2-Sample T-Test.
   - One-way ANOVA.
   - Chi-square Test of Independence.

---

## Dataset Overview
The dataset contains the following features:

| Column       | Description                                                 |
|--------------|-------------------------------------------------------------|
| `datetime`   | Timestamp of the observation.                               |
| `season`     | Season (1: Spring, 2: Summer, 3: Fall, 4: Winter).          |
| `holiday`    | Whether the day is a holiday (1) or not (0).                |
| `workingday` | Whether the day is a working day (1) or not (0).            |
| `weather`    | Weather condition (1: Clear, 2: Misty, 3: Light Rain/Snow). |
| `temp`       | Actual temperature (°C).                                    |
| `atemp`      | Feels-like temperature (°C).                                |
| `humidity`   | Relative humidity (%).                                      |
| `windspeed`  | Wind speed (km/h).                                          |
| `count`      | Total number of bike rentals.                               |

---

## Project Workflow

### Step 1: Setting Up the Environment
- Install the necessary libraries:
  ```bash
  pip install pandas numpy matplotlib seaborn scipy
  ```
- Clone this repository:
  ```bash
  git clone https://github.com/username/yulu-hypothesis-testing.git
  ```

### Step 2: Data Preprocessing and EDA
1. **Load the dataset**:
   ```python
   import pandas as pd
   df = pd.read_csv("bike_sharing.csv")
   ```
2. **Explore the data**:
   - View dataset structure using `.info()` and `.describe()`.
   - Visualize distributions of variables using histograms and boxplots.
3. **Handle missing values and outliers**:
   - Use `.isnull()` to check for missing values.
   - Handle outliers using IQR or capping techniques.

### Step 3: Hypothesis Testing

#### **1. Effect of Working Days on Rentals**
- Test: **2-Sample T-Test**
- Hypotheses:
  - H0: Rentals are the same on working and non-working days.
  - H1: Rentals differ on working and non-working days.
- Code:
  ```python
  from scipy.stats import ttest_ind
  workingday_0 = df[df['workingday'] == 0]['count']
  workingday_1 = df[df['workingday'] == 1]['count']
  t_stat, p_value = ttest_ind(workingday_0, workingday_1, equal_var=False)
  print(f"T-statistic: {t_stat}, P-value: {p_value}")
  ```

#### **2. Seasonal Effect on Rentals**
- Test: **One-way ANOVA**
- Hypotheses:
  - H0: Rentals are the same across all seasons.
  - H1: Rentals differ across seasons.
- Code:
  ```python
  from scipy.stats import f_oneway
  season_data = [df[df['season'] == season]['count'] for season in df['season'].unique()]
  f_stat, p_value = f_oneway(*season_data)
  print(f"F-statistic: {f_stat}, P-value: {p_value}")
  ```

#### **3. Weather Effect on Rentals**
- Test: **One-way ANOVA**
- Hypotheses:
  - H0: Rentals are the same across all weather conditions.
  - H1: Rentals differ across weather conditions.
- Code:
  ```python
  weather_data = [df[df['weather'] == weather]['count'] for weather in df['weather'].unique()]
  f_stat, p_value = f_oneway(*weather_data)
  print(f"F-statistic: {f_stat}, P-value: {p_value}")
  ```

#### **4. Dependency Between Weather and Season**
- Test: **Chi-square Test of Independence**
- Hypotheses:
  - H0: Weather is independent of season.
  - H1: Weather depends on season.
- Code:
  ```python
  from scipy.stats import chi2_contingency
  contingency_table = pd.crosstab(df['season'], df['weather'])
  chi2_stat, p_value, dof, expected = chi2_contingency(contingency_table)
  print(f"Chi-square Statistic: {chi2_stat}, P-value: {p_value}")
  ```

---

## Results Interpretation
- For each test, a **p-value ≤ 0.05** indicates rejecting the null hypothesis, meaning the factor has a significant effect.
- **Example Interpretation**:
  - If the t-test for `workingday` has a p-value of 0.02, conclude that working days significantly affect rentals.

---

## Visualizations
- Use **Seaborn** for insightful plots:
  ```python
  import seaborn as sns
  sns.barplot(x='season', y='count', data=df)
  plt.title("Seasonal Rentals")
  plt.show()
  ```

---

## Key Learnings
- Hypothesis testing provides evidence-based conclusions for business decisions.
- Data visualization reveals patterns that enhance strategic planning.
- Combining statistical and visual insights leads to robust recommendations.

---

## Contributors
- **Shreyash Darade**: Data Analyst and Developer.

Feel free to contribute by submitting a pull request or suggesting improvements!

---

## Contact
For queries or feedback, reach out at: [shreyashdarade555@gmail.com](mailto:shreyashdarade555@gmail.com).
