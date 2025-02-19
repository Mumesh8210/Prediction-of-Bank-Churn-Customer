bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**



import pandas as pd
from openpyxl import load_workbook
from openpyxl.styles import Alignment, Border, Side

# Load the Excel file
file_path = "your_file.xlsx"  # Update with your file path
wb = load_workbook(file_path)

# List of sheets to format
sheets = ["raw data", "data with randomizer", "cases for review"]

# Define border style
thin_border = Border(left=Side(style='thin'), 
                     right=Side(style='thin'), 
                     top=Side(style='thin'), 
                     bottom=Side(style='thin'))

# Format each sheet
for sheet_name in sheets:
    ws = wb[sheet_name]
    
    # Loop through all cells and apply formatting
    for row in ws.iter_rows():
        for cell in row:
            # Center align text
            cell.alignment = Alignment(horizontal="center", vertical="center")
            # Apply border
            cell.border = thin_border

    # Auto-fit columns
    for col in ws.columns:
        max_length = 0
        col_letter = col[0].column_letter  # Get column letter (A, B, C, etc.)
        
        for cell in col:
            try:
                if cell.value:
                    max_length = max(max_length, len(str(cell.value)))
            except:
                pass
        
        adjusted_width = max_length + 2  # Adding padding
        ws.column_dimensions[col_letter].width = adjusted_width

# Save the formatted file
wb.save("formatted_file.xlsx")
print("Formatting applied successfully!")
