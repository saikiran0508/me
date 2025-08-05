from openpyxl import load_workbook
from openpyxl.styles import Font, Border, Side
from openpyxl.utils import get_column_letter

file_path = r"your_file.xlsx"
wb = load_workbook(file_path)

thin = Side(border_style="thin", color="000000")
thick = Side(border_style="thick", color="000000")

for ws in wb.worksheets:
    # Bold first row
    for cell in ws[1]:
        cell.font = Font(bold=True)

    max_row, max_col = ws.max_row, ws.max_column

    # Apply borders
    for row in ws.iter_rows(min_row=1, max_row=max_row, min_col=1, max_col=max_col):
        for cell in row:
            cell.border = Border(top=thin, left=thin, right=thin, bottom=thin)

    # Apply thick outline borders
    for col in range(1, max_col + 1):
        ws.cell(row=1, column=col).border = Border(top=thick, left=thin, right=thin, bottom=thin)
        ws.cell(row=max_row, column=col).border = Border(bottom=thick, left=thin, right=thin, top=thin)
    for row in range(1, max_row + 1):
        ws.cell(row=row, column=1).border = Border(left=thick, top=thin, right=thin, bottom=thin)
        ws.cell(row=row, column=max_col).border = Border(right=thick, top=thin, left=thin, bottom=thin)

    # Auto-fit column width approximation
    for col in ws.columns:
        max_length = 0
        col_letter = get_column_letter(col[0].column)
        for cell in col:
            if cell.value is not None:
                cell_length = len(str(cell.value))  # <-- this should now work
                if cell.row == 1:
                    cell_length += 2  # padding for header
                max_length = max(max_length, cell_length)
        ws.column_dimensions[col_letter].width = max_length * 1.2  # Adjust factor if needed

    # Hide gridlines
    ws.sheet_view.showGridLines = False

wb.save(r"your_file_formatted.xlsx")
