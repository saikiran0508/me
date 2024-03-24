import pandas as pd
from datetime import datetime, time

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert time in h:mm format to numerical format
def time_to_numeric(time_val):
    if isinstance(time_val, datetime):
        time_obj = time_val.time()
    else:
        time_obj = datetime.strptime(str(time_val), '%H:%M:%S').time()
    
    total_hours = time_obj.hour + time_obj.minute / 60 + time_obj.second / 3600
    return total_hours / 24

# Convert the columns containing time values from h:mm format to numerical format
df['Time1_numeric'] = df['Time1'].apply(time_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(time_to_numeric)

# Display the DataFrame with the converted columns
print(df)


















import pandas as pd

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert datetime object to numerical format
def datetime_to_numeric(datetime_val):
    return datetime_val.timestamp() / (24 * 3600)  # Convert to a fraction of a day

# Convert the columns containing datetime values to numerical format
df['Time1_numeric'] = df['Time1'].apply(datetime_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(datetime_to_numeric)

# Display the DataFrame with the converted columns
print(df)
