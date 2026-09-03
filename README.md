# ⚡ Electricity Consumption Analysis

A Python-based exploratory data analysis project that examines electricity usage, tariffs, and billing patterns across four cities — built and run entirely in **Google Colab**.

The project analyzes historical consumption data across cities, companies, and appliances, then includes an interactive tool that estimates a user's own monthly electricity bill based on their appliance usage.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Tools & Technologies](#tools--technologies)
- [How to Run (Google Colab)](#how-to-run-google-colab)
- [Analysis Breakdown](#analysis-breakdown)
- [Bill Prediction Logic](#bill-prediction-logic)
- [Sample Output](#sample-output)
- [Key Insights](#key-insights)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Project Overview

This project explores an electricity usage dataset spanning **4 cities**, multiple **companies**, and **12 months** of billing data, along with appliance-level usage hours (fan, refrigerator, AC, monitor, TV).

The analysis covers two parts:

1. **Exploratory Data Analysis (EDA)** — tariff rates, monthly bills, consumption patterns, revenue, and appliance usage, all visualized with Matplotlib and Seaborn.
2. **Bill Estimation Tool** — a formula-driven calculator (city-wise averages, plus an interactive CLI version) that estimates a monthly electricity bill from appliance wattage and usage hours.

## Dataset

**File:** `Electricity_dataset(4cities).csv`

| Column | Description |
|---|---|
| `City` | City where usage was recorded |
| `Company` | Electricity provider/company |
| `Months` | Billing month |
| `TariffRate` | Tariff rate (₹ per kWh) |
| `MonthlyHours` | Total monthly usage hours |
| `ElectricityBill` | Billed amount (₹) |
| `Fan_hours` | Daily fan usage hours |
| `Refrigerator_hours` | Daily refrigerator usage hours |
| `AirConditioner_hours` | Daily AC usage hours |
| `Monitor_hours` | Daily monitor usage hours |
| `Television_hours` | Daily TV usage hours |

## Tools & Technologies

- **Python 3** (Google Colab)
- **pandas** — data loading, cleaning, and aggregation
- **numpy** — numeric operations
- **matplotlib** & **seaborn** — visualizations
- **tabulate** — clean tabular console output

## How to Run (Google Colab)

1. Open the notebook in [Google Colab](https://colab.research.google.com/).
2. Upload the dataset:
   ```python
   from google.colab import files
   uploaded = files.upload()   # select Electricity_dataset(4cities).csv
   ```
   Or mount Google Drive if the file is stored there:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
3. Install `tabulate` if it isn't already available:
   ```python
   !pip install tabulate
   ```
4. Run all cells in order (**Runtime → Run all**). The script executes every analysis function sequentially and ends with the interactive bill-prediction tool, which will prompt for input directly in the Colab output cell.

> **Note:** the final function, `user_input_usage_analysis()`, uses `input()` prompts — in Colab these appear as text boxes under the cell. Run that cell separately if you want to answer prompts without re-running the full analysis each time.

## Analysis Breakdown

| Function | What it shows |
|---|---|
| `show_original_data()` | Preview of the raw dataset |
| `city_wise_tariff()` | Average tariff rate per city |
| `avg_bill_per_month()` | Average electricity bill by month, per city |
| `avg_monthly_consumption()` | Average monthly consumption (kWh) per city |
| `total_monthly_hours_per_company()` | Total usage hours per company, plotted per-company across months |
| `total_revenue()` | Total revenue by company and by city (formatted in ₹) |
| `avg_tariff_by_company()` | Average tariff rate charged by each company |
| `total_appliance_usage()` | Total usage hours across all appliances (fan, fridge, AC, monitor, TV) |
| `automated_electricity_bill_prediction()` | City-wise estimated monthly bill, derived from average appliance usage × tariff rate |
| `user_input_usage_analysis()` | Interactive tool — select a city (or custom tariff), choose appliances used, enter 7 days of usage, and get a personalized bill estimate with a usage trend chart |

## Bill Prediction Logic

Both prediction functions convert appliance usage hours into estimated **kWh**, using fixed wattage assumptions:

| Appliance | Wattage |
|---|---|
| Fan | 62.5 W |
| Refrigerator | 150 W |
| Air Conditioner | 1500 W |
| Monitor | 22.5 W |
| Television | 125 W |

```text
kWh = (hours × wattage) / 1000
Monthly kWh = Average Daily kWh × 30
Estimated Bill (₹) = Monthly kWh × Tariff Rate
```

This is a **rule-based estimation**, not a trained machine learning model — it applies fixed wattage assumptions and averaged tariff rates rather than learning from historical billing patterns. A natural next step (see [Future Improvements](#future-improvements)) would be replacing this formula with a regression model trained on the dataset's actual `ElectricityBill` values.

## Sample Output

Running the script produces console tables (via `tabulate`) alongside matplotlib/seaborn charts, for example:

```text
🔹 Improved City-wise Predicted Monthly Electricity Bill:
+----------+-------------------------------+-------------------------------+-------------------------------+
| City     |   Average Monthly Units (kWh) |   Average Tariff Rate (₹/kWh) |   Estimated Monthly Bill (₹)  |
+==========+===============================+===============================+=================================+
| ...      |                          ...  |                           ... |                            ... |
+----------+-------------------------------+-------------------------------+-------------------------------+
```

*(Add a screenshot of your actual Colab output/charts here once run — e.g. `images/tariff_by_city.png`, `images/monthly_bill_trend.png` — following the pattern `![City-wise Tariff Rate](images/tariff_by_city.png)`.)*

## Key Insights

> To be filled in after reviewing your actual Colab output — replace with real figures.

- Highest-tariff city: *TODO*
- City with highest average monthly consumption: *TODO*
- Company generating the most total revenue: *TODO*
- Appliance with the highest total usage hours: *TODO*

## Future Improvements

- Replace the fixed-wattage formula with a **trained regression model** (e.g. Linear Regression on `ElectricityBill` vs. appliance hours + tariff) for genuinely predictive, not just formula-based, estimates
- Validate wattage assumptions against real appliance specs, or let users input their own wattage
- Add a simple Streamlit/Gradio front end so the bill estimator doesn't rely on Colab's `input()` prompts
- Expand the dataset beyond 4 cities for broader generalization
- Add error bars / confidence intervals to the city-wise predictions
- Export analysis results and charts automatically to a `reports/` folder

## Author

**Soumil**

A Python-based data analytics project focused on electricity consumption trends, billing analysis, and appliance-usage-driven bill estimation.
