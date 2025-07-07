from datetime import datetime

def clean_date_column(value):
    # If it's already a number or empty, return as-is
    if pd.isna(value):
        return None
    if isinstance(value, (int, float)):
        return int(value)
    if isinstance(value, str) and value.strip() == "":
        return None

    # If it's a datetime-like object
    if isinstance(value, datetime):
        excel_start_date = datetime(1900, 1, 1)
        # Days since 1900-01-01
        days = (value - excel_start_date).days + 1  # Excel's date system starts from day 1
        if days <= 0:
            return 0
        return days

    return value  # fallback (may customize this)

# Apply the function
df['ManualDateColumn_Cleaned'] = df['ManualDateColumn'].apply(clean_date_column)
