import pandas as pd
from pandas.tseries.offsets import DateOffset

# Convert E2 to datetime
df['E2'] = pd.to_datetime(df['E2'], errors='coerce')

# Today's date
today = pd.Timestamp.today()

# 1st day of the month, 13 months ago
thirteen_months_ago = (today - DateOffset(months=13)).replace(day=1)

# Apply logic
df['Status'] = df['E2'].apply(
    lambda x: "> 13 Months" if pd.isna(x) or x < thirteen_months_ago or x > today else "Last-13"
)
