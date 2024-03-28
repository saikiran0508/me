import csv
from datetime import datetime

# Function to calculate the difference in days between two date-time values
def calculate_days_difference(datetime1, datetime2):
    # Convert the date-time strings to datetime objects
    dt1 = datetime.strptime(datetime1, '%m/%d/%Y %I:%M%p')
    dt2 = datetime.strptime(datetime2, '%m/%d/%Y %I:%M%p')

    # Calculate the difference in seconds
    time_difference = (dt2 - dt1).total_seconds()

    # Convert seconds to days
    days_difference = time_difference / (24 * 60 * 60)

    return days_difference

# Read the input CSV file
input_file = 'input.csv'
output_file = 'output.csv'

with open(input_file, 'r') as csvfile:
    reader = csv.reader(csvfile)
    next(reader)  # Skip header row
    data = list(reader)

# Calculate the differences and store them in a list
differences = []
for row in data:
    datetime1 = row[0]  # Assuming column 1 contains the first date-time value
    datetime2 = row[1]  # Assuming column 2 contains the second date-time value
    difference = calculate_days_difference(datetime1, datetime2)
    differences.append([difference])

# Write the differences to a new CSV file
with open(output_file, 'w', newline='') as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(['Difference in Days'])  # Write header
    writer.writerows(differences)

print("Differences calculated and saved to", output_file)
