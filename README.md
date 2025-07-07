import pandas as pd
import numpy as np
import datetime

# Read the Excel file
df = pd.read_excel("your_file.xlsx")

# Problematic column
col = "manual_date_column"

# Fix function
def correct_excel_date(val):
    if pd.isna(val):
        return np.nan
    
    if isinstance(val, pd.Timestamp):
        # Excel's epoch bug offset
        base_date = pd.Timestamp("1899-12-30")
        return (val - base_date).days
    
    elif isinstance(val, datetime.time):
        # This is usually Excel zero shown as 00:00:00
        if val == datetime.time(0, 0):
            return 0
        else:
            return val  # or np.nan or flag if unexpected

    return val  # Return as-is for other types

# Apply correction
df[col] = df[col].apply(correct_excel_date)
