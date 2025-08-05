import xlwings as xw

file_path = r"your_file.xlsx"

# Open Excel workbook
app = xw.App(visible=False)
wb = app.books.open(file_path)

# Loop through all sheets
for sheet in wb.sheets:
    sheet.range("1:1").font.bold = True  # First row bold
    used_range = sheet.used_range

    # Apply borders to all used range
    # xlwings does not support direct border styling in one step,
    # so for complex borders, openpyxl is still better.

    # AutoFit all columns
    sheet.autofit('c')  # 'c' = columns

    # Hide gridlines
    sheet.api.DisplayGridlines = False

# Save and close
output_file = r"your_file_autofit.xlsx"
wb.save(output_file)
wb.close()
app.quit()
print(f"True AutoFit applied and saved as {output_file}")
