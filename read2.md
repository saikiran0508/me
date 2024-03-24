import pandas as pd
from datetime import datetime

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert time in h:mm format to numerical format
def time_to_numeric(time_str):
    time_obj = datetime.strptime(time_str, '%I:%M %p').time()
    total_hours = time_obj.hour + time_obj.minute / 60
    if time_obj.hour == 12:
        return total_hours / 24
    else:
        return total_hours / 24 % 1  # Convert to a fraction of a day

# Convert the columns containing time values from h:mm format to numerical format
df['Time1_numeric'] = df['Time1'].apply(time_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(time_to_numeric)

# Display the DataFrame with the converted columns
print(df)

