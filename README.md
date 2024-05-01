import os

def generate_file_paths(country_names, report_names, dates):
    file_paths = []
    for country in country_names:
        for report in report_names:
            for date in dates:
                file_name = f"{country}_{report}_{date}.txt"
                file_path = os.path.join("path_to_directory", file_name)
                file_paths.append(file_path)
    return file_paths

# Example lists of country names, report names, and dates
country_names = ["USA", "Canada", "UK"]
report_names = ["Sales", "Finance", "Inventory"]
dates = ["2024-01-01", "2024-01-02", "2024-01-03"]

# Generating file paths
file_paths = generate_file_paths(country_names, report_names, dates)

# Printing the generated file paths
for path in file_paths:
    print(path)
