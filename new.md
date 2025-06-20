import pandas as pd

# Ensure columns are numeric
df['AC18'] = pd.to_numeric(df['AC18'], errors='coerce')
df['M18'] = pd.to_numeric(df['M18'], errors='coerce')

# Apply the formula with error handling
df['Result'] = df.apply(
    lambda row: 1 - row['AC18'] / row['M18'] if pd.notna(row['AC18']) and pd.notna(row['M18']) and row['M18'] != 0 else 0,
    axis=1
)
