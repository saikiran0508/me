import pandas as pd

# Ensure the column is datetime
df['E174641'] = pd.to_datetime(df['E174641'], errors='coerce')

# Get the first day of the month
df['Month_Start'] = df['E174641'].dt.to_period('M').dt.to_timestamp()
