import pandas as pd

# Read the Excel file
excel_file = "your_excel_file.xlsx"
df = pd.read_excel(excel_file)

# Convert specific columns to numeric type
columns_to_convert = ['Column1', 'Column2']  # Replace 'Column1' and 'Column2' with your actual column names
df[columns_to_convert] = df[columns_to_convert].apply(pd.to_numeric, errors='coerce')

# Write the modified DataFrame back to an Excel file
output_excel_file = "modified_excel_file.xlsx"
df.to_excel(output_excel_file, index=False)





import pandas as pd

# Load Excel file into DataFrame
file_path = "your_excel_file.xlsx"
xls = pd.ExcelFile(file_path)
df1 = pd.read_excel(xls, 'Sheet1')  # Load the first sheet

# Display the DataFrame to understand its structure and the column names
print(df1.head())

# Assuming your custom formatted columns are 'CustomCol1' and 'CustomCol2', and you want to convert them to numeric
# Replace 'CustomCol1' and 'CustomCol2' with your actual column names
df1['CustomCol1'] = pd.to_numeric(df1['CustomCol1'], errors='coerce')
df1['CustomCol2'] = pd.to_numeric(df1['CustomCol2'], errors='coerce')

# Display DataFrame after conversion
print(df1.head())

# Now you can write this DataFrame back to Excel if needed
# df1.to_excel("output_file.xlsx", index=False)
