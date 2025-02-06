bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**





import pandas as pd
from openpyxl import Workbook
from openpyxl.styles import Border, Side
from openpyxl.utils.dataframe import dataframe_to_rows

Assuming you already have two DataFrames: df and new_df
Example:
df = pd.DataFrame({'Column1': [1, 2, 3], 'Column2': ['A', 'B', 'C']})
new_df = pd.DataFrame({'ColumnA': [10, 20, 30], 'ColumnB': ['X', 'Y', 'Z']})

Create a new Excel workbook
wb = Workbook()

Remove the default sheet created by openpyxl
wb.remove(wb.active)

Function to add a DataFrame to a sheet with autofit and borders
def add_sheet_with_formatting(wb, sheet_name, dataframe):
    Create a new sheet
    ws = wb.create_sheet(title=sheet_name)
    
    # Write the DataFrame to the sheet
    for row in dataframe_to_rows(dataframe, index=False, header=True):
        ws.append(row)
    
    # Autofit columns
    for column in ws.columns:
        max_length = 0
        column_letter = column[0].column_letter
        for cell in column:
            try:
                if len(str(cell.value)) > max_length:
                    max_length = len(str(cell.value))
            except:
                pass
        adjusted_width = (max_length + 2) * 1.2  # Adjust width with some padding
        ws.column_dimensions[column_letter].width = adjusted_width
    
    # Autofit rows (set row height to accommodate text)
    for row in ws.iter_rows():
        for cell in row:
            ws.row_dimensions[cell.row].height = 15  # Set a standard row height
    
    # Apply borders to all cells with data
    thin_border = Border(
        left=Side(style='thin'),
        right=Side(style='thin'),
        top=Side(style='thin'),
        bottom=Side(style='thin')
    )
    
    for row in ws.iter_rows(min_row=1, max_row=ws.max_row, min_col=1, max_col=ws.max_column):
        for cell in row:
            cell.border = thin_border

# Add df to the first sheet named "randomizer"
add_sheet_with_formatting(wb, "randomizer", df)

# Add new_df to the second sheet named "assignments"
add_sheet_with_formatting(wb, "assignments", new_df)

# Save the workbook
output_file = "Formatted_Data.xlsx"
wb.save(output_file)

print(f"Excel file '{output_file}' created with two sheets: 'randomizer' and 'assignments'.")
