import pandas as pd

# Read the Excel file
# df = pd.read_excel('your_file.xlsx') 

# Convert to datetime (if not already)
df['G174641'] = pd.to_datetime(df['G174641'], errors='coerce')
df['E174641'] = pd.to_datetime(df['E174641'], errors='coerce')

# Apply the logic
def date_diff(e, g):
    try:
        if pd.isna(g):
            return 0
        return (e - g).days
    except:
        return 0

df['Result'] = df.apply(lambda row: date_diff(row['E174641'], row['G174641']), axis=1)
