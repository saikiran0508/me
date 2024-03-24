import openpyxl

# Load the workbook
file_path = "your_excel_file.xlsx"
workbook = openpyxl.load_workbook(file_path)

# Access the desired sheet
sheet = workbook['Sheet1']  # Replace 'Sheet1' with the actual sheet name

# Specify the columns you want to convert to numeric format
columns_to_convert = ['A', 'B']  # Replace 'A', 'B' with the column letters or numbers

# Iterate over rows and convert the cell values to numeric
for column in columns_to_convert:
    for row in range(1, sheet.max_row + 1):
        cell = sheet[column + str(row)]
        try:
            cell.value = float(cell.value) if cell.value else None
        except ValueError:
            pass  # Handle non-numeric values here if needed

# Save the workbook
workbook.save("output_file.xlsx")



















import pandas as pd
from pyxlsb import open_workbook

# Load the XLSB file into a DataFrame
file_path = "your_excel_file.xlsb"
with open_workbook(file_path) as wb:
    with wb.get_sheet('Sheet1') as sheet:
        data = sheet.rows()
        df = pd.DataFrame(data)

# Specify the columns you want to convert (assuming column 0 and 1 for example)
columns_to_convert = [0, 1]  # Replace 0, 1 with the actual column indices

# Convert time values to total minutes
for column_idx in columns_to_convert:
    df[column_idx] = df[column_idx].apply(lambda x: int(x * 24 * 60) if pd.notnull(x) else x)

# Now you can save the modified DataFrame to a new Excel file if needed
output_file_path = "output_file.xlsx"
df.to_excel(output_file_path, index=False)


