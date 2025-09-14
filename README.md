Here’s a polished README you can paste directly into your repo. Replace screenshot file names if needed, and update links if you change folders.

# HR Analytics: Attrition & Engagement Dashboard

An interactive Power BI dashboard analyzing employee attrition and engagement from the IBM HR Analytics dataset. The project includes a Jupyter cleaning pipeline, engineered features for KPIs, and DAX measures powering insights by department, tenure, and gender.

## Preview

![Alt Text](HR-Analytics-Attrition-Engagement-Dashboard/dashboard_image.png)


![Alt Text](images/dashboard_image_2.png)

  


- Track headcount, attrition rate, satisfaction, and tenure to highlight risk areas.  
- Enable slice-and-dice analysis by department, tenure band, gender, and income band.  
- Compare outcomes against clear targets using gauges (e.g., Attrition Goal = 10%).

## Dataset

- Source: IBM HR Analytics Employee Attrition & Performance (public snapshot).  
- Note: Snapshot data does not include hire/exit dates; rates are cross-sectional, not time‑series.

## Repository structure

- data/  
  - hr_clean.csv — final dataset used by the report  
  - hr_clean_sample.csv — small sample for quick cloning (optional)  
- notebooks/  
  - hr_cleaning.ipynb — Jupyter pipeline to standardize categories and engineer features  
- pbix/  
  - HR_Attrition_Engagement.pbix — Power BI report  
- screenshots/  
  - overview.png, department_tenure.png — images used in this README  
- sql/ (optional)  
  - helper views or examples  
- README.md, LICENSE, .gitignore

## Engineered features (Python)

- attrition_flag: 1 if Attrition = “Yes”, else 0  
- satisfaction_avg: mean of JobSatisfaction, EnvironmentSatisfaction, WorkLifeBalance  
- tenure_band: bins of YearsAtCompany → 0–1, 1–3, 3–5, 5–10, 10+  
- income_band: quantile bands (Q1–Q5) of MonthlyIncome  
- standardized categories: Department, JobRole, BusinessTravel, MaritalStatus, Gender, OverTime

## Core DAX measures (Power BI)

- Total Employees = DISTINCTCOUNT('hr_clean'[EmployeeNumber])  
- Attritions = CALCULATE(COUNTROWS('hr_clean'), 'hr_clean'[attrition_flag] = 1)  
- Attrition Rate = DIVIDE([Attritions], [Total Employees])  
- Avg Satisfaction = AVERAGE('hr_clean'[satisfaction_avg])  
- Avg Years at Company = AVERAGE('hr_clean'[YearsAtCompany])  
- Optional targets/constants:  
  - Attrition Goal = 0.10  
  - Gauge Min = 0  
  - Gauge Max = 0.30

## Visuals

- KPI cards: Total Employees, Attrition Rate, Avg Satisfaction  
- Bars: Attrition Rate by Department; Attrition Rate by tenure_band  
- Slicer: Gender (add JobRole as optional)  
- Gauges: Attrition Rate vs 10% goal; Avg Satisfaction vs target (e.g., 3.2)  
- Optional: Matrix heatmap Department × Gender; scatter of Avg Satisfaction vs Attrition Rate by Department

## Quick start

1) Data preparation  
- Open notebooks/hr_cleaning.ipynb and run all cells to generate data/hr_clean.csv.

2) Open the dashboard  
- Launch pbix/HR_Attrition_Engagement.pbix in Power BI Desktop.  
- Confirm dataset path points to data/hr_clean.csv (refresh if needed).

3) Explore  
- Use Gender slicer and hover tooltips to inspect department and tenure risk.  
- Adjust Gauge target measures (e.g., Attrition Goal) to match organizational targets.

## Key insights (example)

- Early tenure (0–1 years) exhibits the highest attrition rate, signaling onboarding/engagement opportunities.  
- Specific departments show elevated rates; pairing attrition with satisfaction pinpoints where to act first.

## How to reproduce locally

- Requirements: Python 3.x, Jupyter, pandas; Power BI Desktop  
- Steps:  
  - pip install -r requirements.txt (optional if you add one)  
  - Run the notebook → generate hr_clean.csv → open the PBIX file → Refresh

## Roadmap

- Add tooltip page with micro‑KPIs on hover.  
- Publish a short demo video/GIF.  
- Extend with recruitment/hiring data to enable time‑series attrition.

## License

This project is released under the MIT License. See LICENSE for details.

## Acknowledgments

- IBM HR Analytics dataset community contributors and example analyses that inspired feature engineering and KPI selection.
