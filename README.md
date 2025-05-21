from office365.runtime.auth.user_credential import UserCredential
from office365.sharepoint.client_context import ClientContext

# SharePoint site and file details
site_url = "https://yourcompany.sharepoint.com/sites/yoursite"
relative_url = "/sites/yoursite/Shared Documents/yourfile.docx"
download_path = "yourfile.docx"

# Authentication
username = "your.email@yourcompany.com"
password = "your_password"

ctx = ClientContext(site_url).with_credentials(UserCredential(username, password))
response = ctx.web.get_file_by_server_relative_url(relative_url).download(download_path).execute_query()

print("File downloaded successfully.")
