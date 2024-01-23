# me
only me


import pandas as pd
import pyodbc
from datetime import datetime, timedelta

# Read Excel file
excel_df = pd.read_excel("your_file.xlsx")

# Add a new column with the previous month's date
today = datetime.now()
excel_df['MonthColumn'] = (today - timedelta(days=today.day)).strftime('%m/%d/%y')

# Connect to Access database
conn_str = r'DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};DBQ=your_database.accdb;'
conn = pyodbc.connect(conn_str)
cursor = conn.cursor()

# Create a new table in Access with the Excel data
excel_df.to_sql('YourTableName', conn, if_exists='replace', index=False)

# Close the connection
conn.close()

print("Data added to Access database.")
