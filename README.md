# Public-Utility-Company-Regression-Model
Public Utility Company Revenue Forecasting

A Google Colab notebook that builds and compares two regression models for forecasting a utility company's (Hotazel Steam) monthly revenue, using production volume and seasonal dummy variables. Built in Python with pandas, numpy, matplotlib, and statsmodels.

Data

Source file: AICPA_regressionAnalysisData.csv

48 monthly observations (Jan 2011 – Dec 2014), split by a type column into:

dt4training — 36 months (2011–2013), used to fit the models
dt4testing — 12 months (2014), held out for evaluation

Columns:

Column	Description
type	Training/testing split label
date	Month-end date
revenue	Monthly revenue (target variable)
production	Monthly production volume
coolDD	Cooling degree days
heatDD	Heating degree days
Methodology
Import & prep data — load the CSV, parse date to datetime.
Winter dummy variable — winter_DV = 1 if the month is Dec/Jan/Feb, else 0; winter_interaction = production × winter_DV.
Split into dt4training / dt4testing based on the type column.
Model 1 (Winter) — OLS regression of revenue on production, winter_DV, winter_interaction (with a constant), fit on the training set.
Evaluate Model 1 on the test set via Mean Absolute Percentage Error (MAPE).
Fall dummy variable — fall_DV = 1 if the month is Sep/Oct/Nov, else 0; fall_interaction = production × fall_DV.
Model 2 (Fall) — same OLS approach, using production, fall_DV, fall_interaction.
Evaluate Model 2 on the test set via MAPE.
Visualize — scatter plot of actual test-set revenue vs. production, overlaid with three fitted lines: non-winter, winter, and fall (using each model's coefficients).
Memo to stakeholders — written summary comparing the two models and recommending one.
Results
Model 1 — Winter Dummy Variable
Term	Coefficient
const	5,629,257.08
production	13.51
winter_DV	-201,742.73
winter_interaction	14.16

Test MAPE ≈ 15.90%

Model 2 — Fall Dummy Variable
Term	Coefficient
const	6,118,386.30
production	18.30
fall_DV	-477,240.43
fall_interaction	-7.67

Test MAPE ≈ 22.02%

Conclusion: The Winter Dummy Variable model outperforms the Fall Dummy Variable model (lower MAPE), suggesting winter seasonality has a more meaningful, stable relationship with revenue for this dataset.

Visualization

A scatter plot of test-set revenue vs. production, with three regression lines overlaid:

Chartreuse — non-winter line (Model 1, winter_DV = 0)
Blue — winter line (Model 1, winter_DV = 1)
Orange — fall line (Model 2, fall_DV = 1)
Memo Summary (Step 7)

To: Hotazel Steam · From: Grace Shaw · RE: Hotazel Steam Predicting Revenue

Two seasonal-dummy regression models were compared; the Winter model (MAPE ≈ 15.90%) clearly outperformed the Fall model (MAPE ≈ 22.02%).
Recommendation: use the Winter Dummy Variable model for forecasting.
Limitations noted: Heat Degree Days (heatDD) were not included in either model; no outlier analysis was performed; evaluation relied solely on the available historical dataset.
Suggested next steps: run residual/outlier diagnostics to confirm linear regression assumptions hold, and test Spring and Summer dummy variables to see if either improves on the Winter model's MAPE.
Requirements
numpy
pandas
matplotlib
statsmodels
