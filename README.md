import pandas as pd
import numpy as np

def convert_to_date(val):
    # Handle nulls and zeros
    if pd.isnull(val) or val == 0 or val == '0':
        return pd.NaT
    
    # If it's a float or int and looks like Excel serial
    try:
        val_float = float(val)
        if val_float > 20000:  # Rough cutoff for Excel date serials
            return pd.to_datetime('1899-12-30') + pd.to_timedelta(int(val_float), unit='D')
    except:
        pass
    
    # Try parsing as datetime
    try:
        return pd.to_datetime(val).date()
    except:
        return pd.NaT

# Example dataframe
df = pd.DataFrame({
    'mixed_date': [45820, '2025-01-14 00:00:00', '2024-01-18 00:00:00.000000', 0, '0', None]
})

# Apply the function
df['clean_date'] = df['mixed_date'].apply(convert_to_date)
