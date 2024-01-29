import pandas as pd
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

