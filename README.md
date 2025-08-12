import pandas as pd
from datetime import datetime
from dateutil.relativedelta import relativedelta

# Example data
df = pd.DataFrame({
    "Month": ["August-2025", "July-2025", "June-2025", "May-2025", "April-2025"],
    "Value": [10, 20, 30, 40, 50]
})

# Step 1: Convert Month column to datetime
df["Month_dt"] = pd.to_datetime(df["Month"], format="%B-%Y")

# Step 2: Get current month and the range
today = datetime.today()
start_date = (today.replace(day=1) - relativedelta(months=3))  # 3 months ago (excluding current month)
end_date = (today.replace(day=1) - relativedelta(days=1))       # End of last month

# Step 3: Filter
df_last3 = df[(df["Month_dt"] >= start_date) & (df["Month_dt"] <= end_date)]

# Step 4: Drop helper column if not needed
df_last3 = df_last3.drop(columns="Month_dt")

print(df_last3)
