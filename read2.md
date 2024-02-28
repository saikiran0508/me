import pandas as pd
import numpy as np

# Assuming you already have a DataFrame df with 'country' and 'class' columns

# Define conditions for the new column
conditions = [
    (df['country'] == 'UK') & (df['class'] == 'Personal'),
    # Add more conditions as needed
]

# Define values for the new column corresponding to each condition
values = ['fpb']

# Add more values as needed, matching the conditions

# Create the new column based on the conditions
df['new_column'] = np.select(conditions, values, default='default_value')

# Replace 'default_value' with the default value you want if none of the conditions are met

# Display the updated DataFrame
print(df)
