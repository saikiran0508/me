# me
only me


import pandas as pd
import pyodbc
from datetime import datetime, timedelta

excel_df = pd.read_excel("your_file.xlsx")
today = datetime.now()
excel_df['MonthColumn'] = (today - timedelta(days=today.day)).strftime('%m/%d/%y')

conn_str = r'DRIVER={Microsoft Access Driver (*.mdb, *.accdb)};DBQ=your_database.accdb;'
conn = pyodbc.connect(conn_str)
cursor = conn.cursor()

excel_df.to_sql('YourTableName', conn, if_exists='replace', index=False)

conn.close()
print("Data added to Access database.")
