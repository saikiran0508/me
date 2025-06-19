import pandas as pd
import win32com.client as win32

# === Your DataFrame ===
# Example: replace this with your actual DataFrame
# df = your_dataframe

# Step 1: Remove timezone info from datetime columns if any
for col in df.select_dtypes(include=['datetimetz']).columns:
    df[col] = df[col].dt.tz_localize(None)

# Step 2: Convert to list of lists
header = [df.columns.tolist()]         # Row 1 (column names)
data = df.values.tolist()              # Row 2+ (values)

# Combine header + data
full_data = header + data

# Step 3: Open Excel
excel = win32.gencache.EnsureDispatch('Excel.Application')
excel.Visible = False

# Open your .xlsb file
wb = excel.Workbooks.Open(r'C:\Path\To\your_file.xlsb')  # <== UPDATE path
ws = wb.Sheets('Sheet1')                                 # <== UPDATE sheet name

# Step 4: Delete everything in the sheet
ws.Cells.ClearContents()

# Step 5: Paste DataFrame as values (fast block write)
num_rows = len(full_data)
num_cols = len(full_data[0]) if full_data else 0

if num_rows > 0 and num_cols > 0:
    start_cell = ws.Cells(1, 1)
    end_cell = ws.Cells(num_rows, num_cols)
    target_range = ws.Range(start_cell, end_cell)
    target_range.Value = full_data

# Step 6: Save and close
wb.Save()
wb.Close(SaveChanges=True)
excel.Quit()

