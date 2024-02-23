7ŭimport pandas as pd
import pyodbc
from datetime import datetime, timedelta

excel_df = pd.read_excel("your_file.xlsx")
today = datetime.now()
excel_df['MonthColumn'] = (today - timedelta(days=today.day)).strftime('%m/%d/%y')

conn_str = r'DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};DBQ=your_database.accdb;'
conn = pyodbc.connect(conn_str)

cursor = conn.cursor()
cursor.execute("SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = 'YourTableName'")
columns_info = cursor.fetchall()

column_types = {column_info[0]: column_info[1] for column_info in columns_info}
excel_df = excel_df.astype(column_types)

excel_df.to_sql('YourTableName', conn, if_exists='replace', index=False)

conn.close()
print("Data added to Access database.")




from PIL import Image
import easyocr
import numpy as np

# Load the full image
full_image = Image.open("C:\\Users\\yella\\Videos\\Captures\\NPTEL - Brave 29-01-2024 20_50_10.png")

# Define the region you want to crop
snap_region = (100, 100, 400, 400)  # Example coordinates

# Crop the region from the full image
snap_image = full_image.crop(snap_region)
snap_image.show()

# Convert the cropped image to a numpy array
snap_array = np.array(snap_image)

# Initialize EasyOCR reader
reader = easyocr.Reader(['en'])

# Use OCR to read text from the cropped image
result = reader.readtext(snap_array)

# Display Results
for detection in result:
    print(detection[1])  # Text extracted







import easyocr
import subprocess

def perform_ocr(image_path):
    reader = easyocr.Reader(['en'])  # Specify the language(s) you want to recognize

    # Perform OCR on the image
    result = reader.readtext(image_path)

    # Return the OCR results
    return result

def print_results_to_notepad(results):
    # Create a new Notepad process
    notepad_process = subprocess.Popen(["notepad.exe"], stdin=subprocess.PIPE, text=True)

    # Write the OCR results to Notepad
    for line in results:
        notepad_process.stdin.write(line[1] + "\n")  # Assuming the text is in the second element of the tuple

    # Close Notepad after writing
    notepad_process.stdin.close()

if __name__ == "__main__":
    # Replace 'path/to/your/image.jpg' with the actual path to your image file
    image_path = 'path/to/your/image.jpg'

    # Perform OCR on the image
    ocr_results = perform_ocr(image_path)

    # Print the results to Notepad
    print_results_to_notepad(ocr_results)
import pandas as pd

# Example DataFrame
data = {'date_column': [45323, 45324, 45325, 45326, 45327]}
df = pd.DataFrame(data)

# Convert five-digit number to date format
df['date_column'] = pd.to_datetime(df['date_column'], unit='D', origin='1970-01-01')

print(df)



SELECT *
FROM your_table
WHERE (id, timestamp) IN (
    SELECT id, MAX(timestamp)
    FROM your_table
    GROUP BY id
);
=IF(RIGHT(A1,1)="2", A1 & " as " & A1, A1 & " as " & A1 & "2")



SELECT t1.*
FROM your_table t1
INNER JOIN (
    SELECT id, MAX(timestamp) AS max_timestamp
    FROM your_table
    GROUP BY id
) t2 ON t1.id = t2.id AND t1.timestamp = t2.max_timestamp;
SELECT *
FROM (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY id ORDER BY timestamp DESC) AS rn
    FROM your_table
) AS sub
WHERE rn = 1;
