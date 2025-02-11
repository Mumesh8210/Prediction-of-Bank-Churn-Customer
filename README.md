bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**

import pandas as pd
import numpy as np
from datetime import datetime
from openpyxl import load_workbook
from openpyxl.styles import Alignment, Border, Side
#define the function
def process_excel():
    # Get the list of Excel files in the current directory
    import os
    files = [f for f in os.listdir() if f.endswith('.xlsx')]
    
    if not files:
        print("No Excel files found in the directory.")
        return
    
    file_path = files[0]  # Read the first Excel file found
    
    # Load the Excel file
    df = pd.read_excel(file_path, sheet_name=0)  # Read the first sheet
    
    # Add new columns at the beginning
    df.insert(0, 'Random Numbers', np.random.randint(10000, 99999, size=len(df)))
    df.insert(1, 'Sample', '')  # Empty column for 'Sample'
    df.insert(2, 'Date Sample Pulled', datetime.today().strftime('%Y-%m-%d'))
    df.insert(3, 'Date Worked', '')  # Empty column for 'Date Worked'
    
    # Write the updated data to a new sheet named 'sample'
    with pd.ExcelWriter(file_path, mode='a', if_sheet_exists='replace', engine='openpyxl') as writer:
        df.to_excel(writer, sheet_name='sample', index=False)
    
    # Load workbook and sheet
    wb = load_workbook(file_path)
    ws = wb['sample']
    
    # Define styles for center alignment and borders
    align = Alignment(horizontal='center', vertical='center')
    border = Border(left=Side(style='thin'),
                    right=Side(style='thin'),
                    top=Side(style='thin'),
                    bottom=Side(style='thin'))
    
    # Apply styles to all cells in the sheet
    for row in ws.iter_rows():
        for cell in row:
            cell.alignment = align
            cell.border = border
    for col in ws.columns:
        max_length = 0
        col_letter = col[0].column_letter  # Get the column letter
        for cell in col:
            try:
                if cell.value:
                    max_length = max(max_length, len(str(cell.value)))
            except:
                pass
        adjusted_width = max_length + 2
        ws.column_dimensions[col_letter].width = adjusted_width
    
    
    wb.save(file_path)
    print(f"Updated data successfully written to 'sample' sheet in {file_path} with formatting applied.")

#Process the first available Excel file in the current directory
process_excel()


import pandas as pd

#File paths (Update these with actual file paths)
file_1 = "sample_data.xlsx"  # File containing sample data
file_2 = "reviewer_data.xlsx"  # File containing reviewer names and sample sizes

#Sheet names (if applicable)
sheet_name_1 = "Sheet1"  # Sheet with sample data
sheet_name_2 = "Sheet1"  # Sheet with reviewer data

#Load data
df_samples = pd.read_excel(file_1, sheet_name=sheet_name_1)  # Load sample data
df_reviewers = pd.read_excel(file_2, sheet_name=sheet_name_2)  # Load reviewer data

#Ensure the reviewer file has 'Reviewer' and 'Sample Size' columns
if 'Reviewer' not in df_reviewers.columns or 'Sample Size' not in df_reviewers.columns:
    raise ValueError("The reviewer file must have 'Reviewer' and 'Sample Size' columns.")

#Create a list to store assigned data
assigned_samples = []

# Initialize index for sample distribution
sample_index = 0  

#Loop through each reviewer and assign samples
for _, row in df_reviewers.iterrows():
    reviewer = row['Reviewer']
    sample_size = row['Sample Size']
    
    # Get the samples for this reviewer
    assigned = df_samples.iloc[sample_index:sample_index + sample_size].copy()
    
    # Assign reviewer name to the samples
    assigned['Reviewer'] = reviewer
    
    # Add to final list
    assigned_samples.append(assigned)
    
    # Update the sample index
    sample_index += sample_size

#Concatenate all assigned samples
df_final = pd.concat(assigned_samples, ignore_index=True)

#Save to a new Excel file
output_file = "assigned_samples.xlsx"
df_final.to_excel(output_file, index=False)

print(f"Sample distribution completed! Check the file: {output_file}")
