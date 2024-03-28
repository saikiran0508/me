from datetime import datetime

def excel_datetime_to_days(excel_datetime):
    # Reference datetime in Excel
    reference_datetime = datetime(1900, 1, 1, 0, 0, 0)

    # Parse Excel datetime string
    if ' ' in excel_datetime:
        dt_format = "%m/%d/%Y %I:%M:%S %p"  # Excel datetime format with date and time
    else:
        dt_format = "%I:%M:%S"  # Time format only
        
    excel_dt = datetime.strptime(excel_datetime, dt_format)

    # Calculate timedelta and convert to days
    delta = excel_dt - reference_datetime
    return delta.days + delta.seconds / (24 * 3600)  # Convert seconds to days

# Test cases
excel_datetimes = ["1/6/1900 9:20:15 PM", "8:02:07"]
for excel_dt in excel_datetimes:
    days = excel_datetime_to_days(excel_dt)
    print(f"{excel_dt}: {days} days")
