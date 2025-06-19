import pandas as pd
import win32com.client as win32

# === Your DataFrame (ensure datetime columns are tz-naive) ===
# df = your real DataFrame
for col in df.select_dtypes(include=['datetimetz']).columns:
    df[col] = df[col].dt.tz_localize(None)

# Convert to list of lists (excluding header)
data_values = df.values.tolist()
num_rows, num_cols = df.shape

# === Excel Automation ===
excel = win32.gencache.EnsureDispatch('Excel.Application')
excel.Visible = False

wb = excel.Workbooks.Open(r'C:\Path\To\your_file.xlsb')
ws = wb.Sheets('Sheet1')

# === Clear old data (except header) ===
ws.Range(f"A2:Z{ws.UsedRange.Rows.Count}").ClearContents()  # Adjust column width as needed

# === Fast write entire DataFrame to Excel ===
# Get top-left cell of target range
start_cell = ws.Cells(2, 1)

# Define target range
end_cell = ws.Cells(1 + num_rows, num_cols)  # rows start at 2, +1 to account for base
target_range = ws.Range(start_cell, end_cell)

# Assign all data at once
target_range.Value = data_values

# Save and close
wb.Save()
wb.Close(SaveChanges=True)
excel.Quit()
