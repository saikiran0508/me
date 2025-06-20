import pandas as pd

# Convert E2 to datetime
df['E2'] = pd.to_datetime(df['E2'], errors='coerce')

# Today's date
today = pd.Timestamp.today()

# Apply the logic
df['Status'] = df['E2'].apply(
    lambda x: ">15 Weeks" if pd.isna(x) or x < (today - pd.Timedelta(days=105)) or x > today else "Last-15"
)
