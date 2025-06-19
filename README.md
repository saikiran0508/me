import pandas as pd
import win32com.client as win32

# Sample DataFrame (replace with your actual DataFrame)
df = pd.DataFrame({
    'Name': ['Alice', 'Bob'],
    'Age': [25, 30],
    'City': ['London', 'Paris']
})

# Paths
xlsb_path = r'C:\Path\To\your_file.xlsb'
sheet_name = 'Sheet1'  # Replace with your actual sheet name

# Launch Excel
excel = win32.gencache.EnsureDispatch('Excel.Application')
excel.Visible = False  # Set True to watch it work

# Open workbook
wb = excel.Workbooks.Open(xlsb_path)
ws = wb.Sheets(sheet_name)

# === 1. Clear old data except header ===
last_col = ws.UsedRange.Columns.Count
last_row = ws.UsedRange.Rows.Count
clear_range = f"A2:{chr(64 + last_col)}{last_row}"  # A2 to bottom-right cell
ws.Range(clear_range).ClearContents()

# === 2. Paste DataFrame into Excel starting from row 2 ===
for i in range(len(df)):
    for j in range(len(df.columns)):
        ws.Cells(i + 2, j + 1).Value = df.iat[i, j]  # +2 for row (skip header), +1 for 1-indexed Excel columns

# Save & close
wb.Save()
wb.Close(SaveChanges=True)
excel.Quit()

