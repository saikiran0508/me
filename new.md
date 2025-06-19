import pandas as pd
import xlwings as xw

# Load your DataFrame (or create it)
df = pd.read_excel("source.xlsx")  # Replace with your actual source

# Path to your .xlsb file
xlsb_path = r"C:\path\to\yourfile.xlsb"
sheet_name = "Sheet1"  # Change to your target sheet name
start_cell = "A1"      # Where to begin pasting

# Start Excel app
app = xw.App(visible=False)  # visible=True to watch the paste
wb = app.books.open(xlsb_path)
ws = wb.sheets[sheet_name]

# Optional: clear previous data
ws.range(start_cell).expand().clear_contents()

# Paste as values (headers + data)
data_to_paste = [df.columns.tolist()] + df.values.tolist()
ws.range(start_cell).value = data_to_paste

# Save and close
wb.save()
wb.close()
app.quit()

