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
