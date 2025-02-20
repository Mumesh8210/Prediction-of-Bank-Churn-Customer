bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**


Here's a complete Python script that:

1. Creates an Excel file with two sheets:

"Raw Data": Contains previous quarter dates and a random column of values.

"Case for Review": Contains assigned dates (current date) and reviewed dates (randomized).



2. Uses pandas and openpyxl to handle Excel operations.




---

Complete Code:

import pandas as pd
import numpy as np
from datetime import date, timedelta

def get_previous_quarter_workdays(exclude_dates=None):
    """Fetches all business days (Mon-Fri) from the previous quarter."""
    today = date.today()
    current_quarter = (today.month - 1) // 3 + 1
    
    if current_quarter == 1:
        start_date = date(today.year - 1, 10, 1)
        end_date = date(today.year - 1, 12, 31)
    elif current_quarter == 2:
        start_date = date(today.year, 1, 1)
        end_date = date(today.year, 3, 31)
    elif current_quarter == 3:
        start_date = date(today.year, 4, 1)
        end_date = date(today.year, 6, 30)
    else:
        start_date = date(today.year, 7, 1)
        end_date = date(today.year, 9, 30)

    # Generate all business days (Monday to Friday)
    all_days = pd.date_range(start=start_date, end=end_date, freq='B')

    # Remove excluded dates if provided
    if exclude_dates:
        exclude_dates = pd.to_datetime(exclude_dates)
        all_days = all_days[~all_days.isin(exclude_dates)]  

    return all_days

# Step 1: Generate previous quarter workdays
excluded_holidays = ['2024-12-25', '2024-11-28']  # Example holidays
previous_quarter_dates = get_previous_quarter_workdays(exclude_dates=excluded_holidays)

# Step 2: Create "Raw Data" sheet with random values
raw_data_df = pd.DataFrame({
    "Previous Quarter Dates": previous_quarter_dates,
    "RANDOM": np.random.randint(100, 500, size=len(previous_quarter_dates))  # Random values
})

# Step 3: Create "Case for Review" sheet
current_date = pd.to_datetime(date.today())  # Today's date
review_dates = previous_quarter_dates + pd.to_timedelta(np.random.randint(1, 10, size=len(previous_quarter_dates)), unit='D')

case_for_review_df = pd.DataFrame({
    "Date of Reviews Assigned": previous_quarter_dates,
    "Assigned Date": current_date,
    "Reviewed": np.random.choice([True, False], size=len(previous_quarter_dates)),  # Randomly assign True/False
    "Reviewed Date": review_dates
})

# Step 4: Write to Excel
excel_filename = "Previous_Quarter_Analysis.xlsx"
with pd.ExcelWriter(excel_filename, engine='openpyxl') as writer:
    raw_data_df.to_excel(writer, sheet_name="Raw Data", index=False)
    case_for_review_df.to_excel(writer, sheet_name="Case for Review", index=False)

print(f"Excel file '{excel_filename}' has been created successfully!")


---

 
