import openpyxl

# Load the Excel workbook
workbook = openpyxl.load_workbook('your_excel_file.xlsx')

# Assuming your data is in the first sheet, you may need to change it accordingly
sheet = workbook.active

# Iterate through each cell in the column
for cell in sheet['A']:
    # Change the cell format to number
    cell.number_format = '0.00'

# Save the changes
workbook.save('formatted_excel_file.xlsx')
