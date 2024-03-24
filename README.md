import pandas as pd
from datetime import datetime

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert time in various formats to numerical format
def time_to_numeric(time_val):
    if isinstance(time_val, datetime):
        # If the value is already a datetime object
        time_obj = time_val.time()
    else:
        # If the value is a string, parse it to datetime object
        time_obj = datetime.strptime(str(time_val), '%I:%M:%S %p' if 'AM' in str(time_val) or 'PM' in str(time_val) else '%H:%M:%S').time()
    
    # Calculate the total hours
    total_hours = time_obj.hour + time_obj.minute / 60 + time_obj.second / 3600
    # Convert to fraction of a day
    return total_hours / 24

# Convert the columns containing time values from various formats to numerical format
df['Time1_numeric'] = df['Time1'].apply(time_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(time_to_numeric)

# Display the DataFrame with the converted columns
print(df)
