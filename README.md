from datetime import datetime
import pandas as pd
import numpy as np

def convert_to_date(val):
    try:
        # Handle missing or zero-like values
        if pd.isnull(val) or str(val).strip() in ['0', '0000-00-00', '']:
            return pd.NaT
        
        # Handle Excel serial numbers
        if str(val).replace('.', '', 1).isdigit():
            val = float(val)
            if val > 59:
                dt = pd.to_datetime('1899-12-30') + pd.to_timedelta(int(val), unit='D')
            else:
                return pd.NaT
        else:
            # Parse string-like dates
            dt = pd.to_datetime(str(val), errors='coerce', dayfirst=True)
        
        # Validate year
        if dt is pd.NaT or dt.year == 1900 or dt.year > datetime.today().year:
            return pd.NaT
        
        return dt.date  # Or use dt if you want datetime instead of date
    
    except:
        return pd.NaT
