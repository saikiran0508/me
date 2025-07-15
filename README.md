import win32com.client
import pandas as pd

# Start Outlook and access the default Contacts folder
outlook = win32com.client.Dispatch("Outlook.Application").GetNamespace("MAPI")
contacts_folder = outlook.GetDefaultFolder(10)  # 10 = olFolderContacts
contacts = contacts_folder.Items

# Prepare list to hold contact details
contact_data = []

# Iterate through each contact item
for contact in contacts:
    try:
        contact_data.append({
            'Full Name': contact.FullName,
            'Email': contact.Email1Address,
            'Job Title': contact.JobTitle,
            'Department': contact.Department,
            'Company': contact.CompanyName,
            'Business Phone': contact.BusinessTelephoneNumber,
            'Mobile Phone': contact.MobileTelephoneNumber,
            'Mailing Address': contact.MailingAddress
        })
    except Exception as e:
        print("Error reading contact:", e)

# Convert list to DataFrame
df_contacts = pd.DataFrame(contact_data)

# Show the DataFrame
print(df_contacts)
