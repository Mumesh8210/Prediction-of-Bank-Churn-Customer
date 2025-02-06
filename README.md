# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**
Here's the modified code that checks if the output file already exists and if the "population" sheet already contains data. If it does, the code will overwrite the existing data instead of appending to it:

Here is a Python code snippet that calculates the required details:


Here's the modified Python code to get the first and last working days of the previous month:

```
Here's the Python code using pandas and openpyxl libraries to save two DataFrames to different sheets in an Excel file:

```
import pandas as pd
from openpyxl import Workbook
from openpyxl.styles import Alignment, Border, Side
from openpyxl.utils import get_column_letter

Assuming df and new_df are your DataFrames
df = pd.DataFrame({'Column1': ['Data1', 'Data2'], 'Column2': ['Data3', 'Data4']})
new_df = pd.DataFrame({'Column3': ['Data5', 'Data6'], 'Column4': ['Data7', 'Data8']})

Create an Excel workbook
wb = Workbook()
ws1 = wb.active
ws1.title = "Randomizer"
ws2 = wb.create_sheet("Assignments")

Write DataFrames to Excel sheets
for r in df.values.tolist():
    ws1.append(r)
for r in new_df.values.tolist():
    ws2.append(r)

Set header row values
ws1['A1'] = 'Randomizer'
ws2['A1'] = 'Assignments'

Auto-fit columns and add borders
for column_cells in ws1.columns:
    length = max(len(str(cell.value)) for cell in column_cells)
    ws1.column_dimensions[get_column_letter(column_cells[0].column)].width = length + 2
for row in ws1.rows:
    for cell in row:
        cell.alignment = Alignment(horizontal='center')
        cell.border = Border(left=Side(style='thin'), right=Side(style='thin'), top=Side(style='thin'), bottom=Side(style='thin'))

for column_cells in ws2.columns:
    length = max(len(str(cell.value)) for cell in column_cells)
    ws2.column_dimensions[get_column_letter(column_cells[0].column)].width = length + 2
for row in ws2.rows:
    for cell in row:
        cell.alignment = Alignment(horizontal='center')
        cell.border = Border(left=Side(style='thin'), right=Side(style='thin'), top=Side(style='thin'), bottom=Side(style='thin'))

Save the workbook
wb.save("output.xlsx")
```

This code creates a new Excel workbook, adds two sheets ("Randomizer" and "Assignments"), wr
,,,
from datetime import datetime, timedelta
import calendar

today = datetime.today()
first_day_of_current_month = today.replace(day=1)
last_day_of_previous_month = first_day_of_current_month - timedelta(days=1)
first_day_of_previous_month = last_day_of_previous_month.replace(day=1)

Get the first working day of the previous month
first_working_day_of_previous_month = first_day_of_previous_month
while first_working_day_of_previous_month.weekday() >= 5:  # 5 = Saturday, 6 = Sunday
    first_working_day_of_previous_month += timedelta(days=1)

Get the last working day of the previous month
last_working_day_of_previous_month = last_day_of_previous_month
while last_working_day_of_previous_month.weekday() >= 5:  # 5 = Saturday, 6 = Sunday
    last_working_day_of_previous_month -= timedelta(days=1)

print("First Working Day of Previous Month:", first_working_day_of_previous_month.strftime('%d%m%Y'))
print("Last Working Day of Previous Month:", last_working_day_of_previous_month.strftime('%d%m%Y'))
```

```
from datetime import datetime, timedelta

def get_previous_month_details():
    today = datetime.today()
    first_day_of_current_month = today.replace(day=1)
    last_day_of_previous_month = first_day_of_current_month - timedelta(days=1)
    first_day_of_previous_month = last_day_of_previous_month.replace(day=1)

    previous_month_number = last_day_of_previous_month.month
    previous_month_year = last_day_of_previous_month.year

    first_day_of_previous_month_str = first_day_of_previous_month.strftime('%d%m%Y')
    last_day_of_previous_month_str = last_day_of_previous_month.strftime('%d%m%Y')

    return {
        'previous_month_number': str(previous_month_number).zfill(2),
        'previous_month_year': str(previous_month_year),
        'first_day_of_previous_month': first_day_of_previous_month_str,
        'last_day_of_previous_month': last_day_of_previous_month_str,
        'date_range': f"{first_day_of_previous_month_str} - {last_day_of_previous_month_str}"
    }

details = get_previous_month_details()
print(details)
```
Here's the modified code that checks if the output file already exists and if the "population" sheet already contains data. If it does, the code will overwrite the existing data instead of appending to it:

```
import os
import pandas as pd

Get the current working directory
current_dir = os.getcwd()
print(f"Current working directory: {current_dir}")

Define the output file name
output_file_name = 'combined_data.xlsx'

Get a list of all Excel files in the current directory (excluding the output file)
excel_files = [
    os.path.join(current_dir, file_name)
    for file_name in os.listdir(current_dir)
    if (file_name.endswith('.xlsx') or file_name.endswith('.xls')) and file_name != output_file_name
]

Read all Excel files into DataFrames and combine them
combined_df = pd.concat([pd.read_excel(file) for file in excel_files], ignore_index=True)

Define the output file path
output_file_path = os.path.join(current_dir, output_file_name)

Check if the output file already exists
if os.path.exists(output_file_path):
    # Read the existing Excel file
    existing_df = pd.read_excel(output_file_path, sheet_name='population')
    
    # Check if the existing DataFrame is the same as the new combined DataFrame
    if existing_df.equals(combined_df):
        print("No changes detected. Output file remains the same.")
    else:
        # Overwrite the existing Excel file with the new combined DataFrame
        with pd.ExcelWriter(output_file_path, engine='openpyxl', mode='a', if_sheet_exists='replace') as writer:
            combined_df.to_excel(writer, index=False, sheet_name='population')
        print(f"Output file updated with new data.")
else:
    # Write the combined DataFrame to a new Excel file
    with pd.ExcelWriter(output_file_path, engine='openpyxl') as writer:
        combined_df.to_excel(writer, index=False, sheet_name='population')
    print(f"Output file created with new data.")
```

This code checks if the output file already exists and if the "population" sheet already contains data. If it does, the code will overwrite the existing data instead of appending to it. If the data is the same, the code will print a message indicating that no changes were detected.
Here's the Python code using pandas and openpyxl libraries to save two DataFrames to different sheets in an Excel file:

```
import pandas as pd
from openpyxl import Workbook
from openpyxl.styles import Alignment, Border, Side
from openpyxl.utils import get_column_letter

Assuming df and new_df are your DataFrames
df = pd.DataFrame({'Column1': ['Data1', 'Data2'], 'Column2': ['Data3', 'Data4']})
new_df = pd.DataFrame({'Column3': ['Data5', 'Data6'], 'Column4': ['Data7', 'Data8']})

Create an Excel workbook
wb = Workbook()
ws1 = wb.active
ws1.title = "Randomizer"
ws2 = wb.create_sheet("Assignments")

Write DataFrames to Excel sheets
for r in df.values.tolist():
    ws1.append(r)
for r in new_df.values.tolist():
    ws2.append(r)

Set header row values
ws1['A1'] = 'Randomizer'
ws2['A1'] = 'Assignments'

Auto-fit columns and add borders
for column_cells in ws1.columns:
    length = max(len(str(cell.value)) for cell in column_cells)
    ws1.column_dimensions[get_column_letter(column_cells[0].column)].width = length + 2
for row in ws1.rows:
    for cell in row:
        cell.alignment = Alignment(horizontal='center')
        cell.border = Border(left=Side(style='thin'), right=Side(style='thin'), top=Side(style='thin'), bottom=Side(style='thin'))

for column_cells in ws2.columns:
    length = max(len(str(cell.value)) for cell in column_cells)
    ws2.column_dimensions[get_column_letter(column_cells[0].column)].width = length + 2
for row in ws2.rows:
    for cell in row:
        cell.alignment = Alignment(horizontal='center')
        cell.border = Border(left=Side(style='thin'), right=Side(style='thin'), top=Side(style='thin'), bottom=Side(style='thin'))

Save the workbook
wb.save("output.xlsx")
```

This code creates a new Excel workbook, adds two sheets ("Randomizer" and "Assignments"), writes the DataFrames to the respective sheets, auto-fits the columns, centers the text, and adds borders around the cells. Finally, it saves the workbook as "output.xlsx".

