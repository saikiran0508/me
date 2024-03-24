from datetime import datetime

def time_to_decimal(time_str):
    try:
        # Parse the time string to a datetime object
        time_obj = datetime.strptime(time_str, '%I:%M:%S %p')
    except ValueError:
        try:
            time_obj = datetime.strptime(time_str, '%m/%d/%Y %I:%M %p')
        except ValueError:
            return "Invalid time format"
    
    # Convert time to decimal number
    decimal_time = time_obj.hour + time_obj.minute / 60 + time_obj.second / 3600
    return round(decimal_time, 2)

# Test the function
time_values = ['2:39:59 AM', '1/6/1900 9:20 PM']

for time_value in time_values:
    decimal_time = time_to_decimal(time_value)
    print(f"{time_value} -> {decimal_time}")

