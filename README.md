import pandas as pd
import numpy as np

def convert_to_date(val):
    try:
        # Handle missing or zero-like values
        if pd.isnull(val) or str(val).strip() in ['0', '0000-00-00', '']:
            return pd.NaT
        
        # Convert Excel serial date numbers (integers or floats)
        if str(val).replace('.', '', 1).isdigit():  # allows float as string
            val = float(val)
            if val > 59:  # Excel has a leap year bug at day 60
                return pd.to_datetime('1899-12-30') + pd.to_timedelta(int(val), unit='D')
        
        # Parse normal string date formats
        return pd.to_datetime(str(val), errors='coerce', dayfirst=True)
    
    except:
        return pd.NaT

# Example usage
df['clean_date'] = df['your_column'].apply(convert_to_date)

# Optional: Drop the time part if not needed
df['clean_date'] = df['clean_date'].dt.date  # Will convert datetime to Python date object

# If you want string format instead:
# df['clean_date'] = df['clean_date'].dt.strftime('%Y-%m-%d')
