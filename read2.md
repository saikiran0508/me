from datetime import datetime

def convert_to_days(time_str):
    # Define the base datetime
    base_datetime = datetime(1900, 1, 1, 0, 0, 0)

    # Parse the input time string
    parsed_time = datetime.strptime(time_str, '%m/%d/%Y %I:%M:%S %p') if '/' in time_str else datetime.strptime(time_str, '%I:%M:%S %p')

    # Calculate the difference
    time_difference = parsed_time - base_datetime

    # Convert the difference to days
    days_difference = time_difference.total_seconds() / (60 * 60 * 24)

    return days_difference

# Example usage:
time1 = '1/6/1900 9:20:15 PM'
time2 = '8:02:07 AM'

days1 = convert_to_days(time1)
days2 = convert_to_days(time2)

print("Difference in days for time1:", days1)
print("Difference in days for time2:", days2)
