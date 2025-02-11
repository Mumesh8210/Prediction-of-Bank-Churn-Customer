bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**

import pandas as pd

# File paths (update these with your actual file names)
calculator_file = "calculator.xlsx"  # File 1
sample_data_file = "sample_data.xlsx"  # File 2

# Read the sample size from File 1
calculator_df = pd.read_excel(calculator_file, sheet_name=0, header=None)  # Read without headers
sample_size = int(calculator_df.iloc[23, 2])  # C24 is in row index 23, column index 2

# Read agent names from D20-D25 (if needed)
agent_names = calculator_df.iloc[19:25, 3].dropna().tolist()  # Row 19-25, Column D (index 3)

# Read the "Sample" sheet from File 2
sample_df = pd.read_excel(sample_data_file, sheet_name="Sample")

# Extract only the required columns
selected_columns = ["Account Number", "Case Number"]
if all(col in sample_df.columns for col in selected_columns):
    filtered_df = sample_df[selected_columns]
else:
    raise ValueError("Required columns not found in the 'Sample' sheet.")

# Select only the required number of rows based on sample size
final_sample = filtered_df.head(sample_size)  # Change to `.sample(n=sample_size)` for random selection

# Save the extracted data into a new file
output_file = "extracted_sample.xlsx"
final_sample.to_excel(output_file, index=False)

print(f"Extracted {sample_size} rows and saved to {output_file}.")
