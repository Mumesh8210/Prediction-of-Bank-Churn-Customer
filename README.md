bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**


import pandas as pd
import os

def process_excel():
    # Get the list of Excel files in the current directory
    files = [f for f in os.listdir() if f.endswith('.xlsx')]
    
    if not files:
        print("No Excel files found in the directory.")
        return
    
    file_path = files[0]  # Read the first Excel file found
    
    # Load the Excel file
    df = pd.read_excel(file_path, sheet_name=0)  # Read the first sheet
    
    # Filter data where 'Notary Required' is 'Y'
    filtered_df = df[df['Notary Required'].astype(str).str.strip() == 'Y']
    
    # Remove duplicates based on 'ClaimID'
    filtered_df = filtered_df.drop_duplicates(subset=['ClaimID'])
    
    # Write the filtered data to a new sheet named 'sample'
    with pd.ExcelWriter(file_path, mode='a', if_sheet_exists='replace', engine='openpyxl') as writer:
        filtered_df.to_excel(writer, sheet_name='sample', index=False)
    
    print(f"Filtered data successfully written to 'sample' sheet in {file_path}.")

#Process the first available Excel file in the current directory
process_excel()

