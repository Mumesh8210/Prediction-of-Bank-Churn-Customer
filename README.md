bu# Prediction-of-Bank-Churn-Customer
*This project aims to develop a machine learning model that can predict the likelihood of a bank customer churning or leaving the bank. Customer churn is a critical issue in the banking industry, and 
being able to predict it can help banks take proactive steps to retain customers and minimize revenue los*




*The first step in this project would be to gather the necessary data. This data can be obtained from the bank's database or from external sources such as customer surveys or other market research. Once the data has been collected, it will need to be pre-processed and cleaned to remove any missing or irrelevant information.*



*Next, the data will be divided into two sets: a training set and a testing set. The training set will be used to train the machine learning model, while the testing set will be used to evaluate its performance*


*Various machine learning algorithms can be used to develop the classification model, such as logistic regression, decision trees, random forests, or support vector machines. The performance of the model can be evaluated using various metrics such as accuracy, precision, recall, and F1 score.*


**Once the model has been trained and evaluated, it can be used to predict whether a new customer is likely to churn or not. This information can be used by the bank to take appropriate measures such as offering special promotions or incentives to retain customers who are at risk of churning.
Overall, the goal of this project is to develop a machine learning model that can help banks to identify customers who are likely to churn and take appropriate measures to retain them.**

# Select only the required columns from the extracted data
columns_to_keep = ["Reviewer", "Serial Number", "Amount", "HardHID", "Added Date"]

# New columns to add
new_columns = ["Column", "Assigned", "Assigned Date", "Reviewed", "Reviewed Date", "Due Date"]

# Ensure the selected columns exist in the data
filtered_columns = [col for col in columns_to_keep if col in final_df.columns]

# Create a new DataFrame with selected columns
final_df_selected = final_df[filtered_columns].copy()

# Add new columns with empty values
for col in new_columns:
    final_df_selected[col] = ""

# Save the modified data to a new file
final_df_selected.to_excel("Final_Selected_Data.xlsx", index=False)

print("Filtered data saved successfully!")
