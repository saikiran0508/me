import openpyxl
from openpyxl.styles import Font, Border, Side
from openpyxl.utils import get_column_letter

# Load your workbook
file_path = r"your_file.xlsx"
wb = openpyxl.load_workbook(file_path)

# Define border styles
thin = Side(border_style="thin", color="000000")
thick = Side(border_style="thick", color="000000")

for ws in wb.worksheets:
    # --- 1. Make first row bold ---
    for cell in ws[1]:
        cell.font = Font(bold=True)

    # Find max rows and columns with data
    max_row = ws.max_row
    max_col = ws.max_column

    # --- 2. Apply borders ---
    for row in ws.iter_rows(min_row=1, max_row=max_row, min_col=1, max_col=max_col):
        for cell in row:
            # Default thin border for all cells
            cell.border = Border(top=thin, left=thin, right=thin, bottom=thin)

    # Apply thick outline to the data range
    for col in range(1, max_col + 1):
        ws.cell(row=1, column=col).border = Border(
            top=thick,
            left=ws.cell(row=1, column=col).border.left,
            right=ws.cell(row=1, column=col).border.right,
            bottom=ws.cell(row=1, column=col).border.bottom
        )
        ws.cell(row=max_row, column=col).border = Border(
            bottom=thick,
            left=ws.cell(row=max_row, column=col).border.left,
            right=ws.cell(row=max_row, column=col).border.right,
            top=ws.cell(row=max_row, column=col).border.top
        )

    for row in range(1, max_row + 1):
        ws.cell(row=row, column=1).border = Border(
            left=thick,
            top=ws.cell(row=row, column=1).border.top,
            bottom=ws.cell(row=row, column=1).border.bottom,
            right=ws.cell(row=row, column=1).border.right
        )
        ws.cell(row=row, column=max_col).border = Border(
            right=thick,
            top=ws.cell(row=row, column=max_col).border.top,
            bottom=ws.cell(row=row, column=max_col).border.bottom,
            left=ws.cell(row=row, column=max_col).border.left
        )

    # --- 3. Auto adjust column widths ---
    for col in ws.columns:
        max_length = 0
        col_letter = get_column_letter(col[0].column)
        for cell in col:
            try:
                if cell.value:
                    max_length = max(max_length, len(str(cell.value)))
            except:
                pass
        ws.column_dimensions[col_letter].width = max_length + 2

    # --- 4. Turn off gridlines in view ---
    ws.sheet_view.showGridLines = False

# Save the formatted file
output_path = r"your_file_formatted.xlsx"
wb.save(output_path)
print(f"Formatted file saved as {output_path}")
