# Convert timezone-aware datetime columns to tz-naive
for col in df.select_dtypes(include=['datetimetz']).columns:
    df[col] = df[col].dt.tz_localize(None)

# Paste data to Excel
num_rows, num_cols = df.shape

for i in range(num_rows):
    for j in range(num_cols):
        ws.Cells(i + 2, j + 1).Value = df.iloc[i, j]
