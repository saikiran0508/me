from datetime import datetime
import pandas as pd
import numpy as np

def convert_to_date(val):
    try:
        if pd.isnull(val) or str(val).strip() in ['0', '', '0000-00-00']:
            return pd.NaT

        val_str = str(val).strip()

        # Handle Excel serial numbers
        if val_str.replace('.', '', 1).isdigit():
            val_float = float(val_str)
            if val_float > 59:
                return pd.to_datetime('1899-12-30') + pd.to_timedelta(int(val_float), unit='D')

        # Try specific formats first
        for fmt in ('%d-%m-%y %H:%M:%S', '%d-%m-%Y %H:%M:%S', '%d-%m-%y', '%Y-%m-%d'):
            try:
                return datetime.strptime(val_str.split('.')[0], fmt)
            except:
                continue

        # Fallback to pandas parsing with dayfirst=True
        return pd.to_datetime(val_str, errors='coerce', dayfirst=True)

    except:
        return pd.NaT

# Apply to your DataFrame
df['clean_date'] = df['your_column'].apply(convert_to_date)

# Strip time portion if needed
df['clean_date'] = df['clean_date'].dt.date
