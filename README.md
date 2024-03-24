import pandas as pd

# Read the Excel file into a DataFrame
df = pd.read_excel('your_excel_file.xlsx')

# Function to convert datetime object to numerical format
def datetime_to_numeric(datetime_val):
    reference_date = pd.Timestamp('1900-01-01')
    total_seconds = (datetime_val - reference_date).total_seconds()
    total_hours = total_seconds / 3600
    return total_hours

# Convert the columns containing datetime values to numerical format
df['Time1_numeric'] = df['Time1'].apply(datetime_to_numeric)
df['Time2_numeric'] = df['Time2'].apply(datetime_to_numeric)

# Display the DataFrame with the converted columns
print(df)























def datetime_to_numeric(datetime_val):
    if isinstance(datetime_val, datetime):
        reference_date = datetime_val.replace(hour=0, minute=0, second=0, microsecond=0)
    elif isinstance(datetime_val, time):
        reference_date = datetime.combine(datetime.today(), datetime_val)
    else:
        raise ValueError("Unsupported data type")
        
    total_seconds = (datetime_val - reference_date).total_seconds()
    total_hours = total_seconds / 3600
    return total_hours
