import win32com.client

# Path to your Excel file
file_path = r"C:\path\to\your\file.xlsm"

# Open Excel
excel = win32com.client.Dispatch("Excel.Application")
excel.Visible = True  # Set to False to run it in background

# Open the workbook
wb = excel.Workbooks.Open(file_path)

# Run the macro (name it exactly as in Excel)
excel.Application.Run("MyMacro")

# Optional: Save and close
# wb.Save()
# wb.Close()

# Quit Excel
# excel.Quit()

