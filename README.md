import pandas as pd

# Ensure E2 and X2 are datetime columns
df['E2'] = pd.to_datetime(df['E2'], errors='coerce')
df['X2'] = pd.to_datetime(df['X2'], errors='coerce')

# Apply logic
def calc_diff(e, x):
    try:
        if pd.isna(x) or x == pd.Timestamp(0):
            return 0
        return (e - x).days
    except:
        return 0

df['Day_Diff'] = df.apply(lambda row: calc_diff(row['E2'], row['X2']), axis=1)
