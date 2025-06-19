import pandas as pd
from pandas.tseries.offsets import DateOffset

# Ensure the column is datetime
df['E174641'] = pd.to_datetime(df['E174641'], errors='coerce')

# Today's date
today = pd.Timestamp.today()

# First day of the month 13 months ago
thirteen_months_ago = (today - DateOffset(months=13)).replace(day=1)

# Apply the logic
df['Status'] = df['E174641'].apply(
    lambda x: ">13 Months" if pd.isna(x) or x < thirteen_months_ago or x > today else "Last-13"
)
