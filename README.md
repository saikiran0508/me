import pandas as pd

# Example DataFrame
# df = pd.read_excel('your_file.xlsx') 

# Replace blanks ("") with NaN
df['G174641'] = df['G174641'].replace("", pd.NA)

# Convert columns to numeric (if needed), coercing errors to NaN
df['G174641'] = pd.to_numeric(df['G174641'], errors='coerce')
df['E174641'] = pd.to_numeric(df['E174641'], errors='coerce')

# Apply the formula logic
def calculate_value(e, g):
    try:
        if pd.isna(g) or g == 0:
            return 0
        return e - g
    except:
        return 0

df['Result'] = df.apply(lambda row: calculate_value(row['E174641'], row['G174641']), axis=1)
