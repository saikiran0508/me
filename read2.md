from datetime import datetime, timedelta

def get_formatted_date(days_ago):
    target_date = datetime.now() - timedelta(days=days_ago)
    formatted_date = target_date.strftime("%d%b%Y").upper()
    return formatted_date

# Example usage:
print(get_formatted_date(0))  # Output: 29JUL2024
print(get_formatted_date(1))  # Output: 28JUL2024
