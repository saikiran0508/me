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
