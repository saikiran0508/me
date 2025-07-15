import win32com.client
import pandas as pd

# Connect to Outlook
outlook = win32com.client.Dispatch("Outlook.Application").GetNamespace("MAPI")

# Get Global Address List
address_list = outlook.AddressLists("Global Address List")
entries = address_list.AddressEntries

# For Exchange users, resolve to get full properties like job title, department, etc.
contacts_data = []

for i in range(1, entries.Count + 1):
    entry = entries.Item(i)
    try:
        exch_user = entry.GetExchangeUser()
        if exch_user:
            contacts_data.append({
                "Name": exch_user.Name,
                "Email": exch_user.PrimarySmtpAddress,
                "Job Title": exch_user.JobTitle,
                "Department": exch_user.Department,
                "Company": exch_user.CompanyName
            })
    except Exception as e:
        print(f"Error with entry {i}: {e}")

# Load into DataFrame
df_gal = pd.DataFrame(contacts_data)

# Display top few rows
print(df_gal.head())
