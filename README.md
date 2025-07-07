import pandas as pd
import numpy as np
import datetime

# Read Excel file
df = pd.read_excel('your_file.xlsx')

# Replace 'your_column' with the actual column name
col = 'your_column'

def correct_excel_date(val):
    if pd.isna(val):
        return np.nan

    # Excel wrongly formatted 0 as datetime.time(0, 0)
    if isinstance(val, datetime.time):
        if val == datetime.time(0, 0):
            return 0
        else:
            return val  # Keep it or flag

    # Excel date interpreted as Timestamp (e.g., 1900-01-03 00:00:00)
    if isinstance(val, pd.Timestamp):
        base = pd.Timestamp('1899-12-30')  # Excel's epoch origin
        return (val - base).days

    # If already int or float
    if isinstance(val, (int, float)):
        return val

    # If it's a string that might be '00:00:00' or something else
    if isinstance(val, str):
        val = val.strip()
        if val == '00:00:00':
            return 0
        try:
            # Try to parse as datetime
            parsed = pd.to_datetime(val, errors='coerce')
            if pd.notna(parsed):
                base = pd.Timestamp('1899-12-30')
                return (parsed - base).days
        except:
            pass
        try:
            return float(val)
        except:
            return val  # return as-is if completely unparseable

    return val  # fallback

# Apply to column
df[col] = df[col].apply(correct_excel_date)
