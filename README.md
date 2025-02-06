bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**







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
for r in df.columns:
    ws1.append([r])
for r in df.values.tolist():
    ws1.append(r)

for r in new_df.columns:
    ws2.append([r])
for r in new_df.values.tolist():
    ws2.append(r)

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

