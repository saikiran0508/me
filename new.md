import pandas as pd

# Make sure U2 and T2 are numeric
df['U2'] = pd.to_numeric(df['U2'], errors='coerce')
df['T2'] = pd.to_numeric(df['T2'], errors='coerce')

# Apply the logic
df['Result'] = df.apply(
    lambda row: row['U2'] / row['T2'] if pd.notna(row['U2']) and pd.notna(row['T2']) and row['T2'] != 0 else 0,
    axis=1
)
