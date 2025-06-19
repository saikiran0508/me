import pandas as pd

# Make sure the columns are numeric
df['I174641'] = pd.to_numeric(df['I174641'], errors='coerce')
df['J174641'] = pd.to_numeric(df['J174641'], errors='coerce')

# Perform division with error handling
df['Result'] = df.apply(
    lambda row: row['I174641'] / row['J174641'] if pd.notna(row['I174641']) and pd.notna(row['J174641']) and row['J174641'] != 0 else 0,
    axis=1
)
