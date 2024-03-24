import pandas as pd

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert time in h:mm format to numerical format
def time_to_numeric(time_str):
    hours, minutes = map(int, time_str.split(':'))
    total_hours = hours + minutes / 60
    return total_hours / 24  # Convert to a fraction of a day

# Convert the columns containing time values from h:mm format to numerical format
df['Time1_numeric'] = df['Time1'].apply(time_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(time_to_numeric)

# Display the DataFrame with the converted columns
print(df)

