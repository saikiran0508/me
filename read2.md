from office365.sharepoint.client_context import ClientContext
from office365.runtime.auth.user_credential import UserCredential

# SharePoint site and credentials
site_url = "https://yourcompanyname.sharepoint.com/sites/yoursitename"
username = "your_username"  # replace with your SharePoint username (e.g., your email address)
password = "your_password"  # replace with your SharePoint password
file_url = "/sites/yoursitename/Shared Documents/yourfile.txt"  # replace with your file's relative URL
download_path = "C:/path/to/save/yourfile.txt"  # replace with the local path where you want to save the file

# Authenticate using username and password
ctx = ClientContext(site_url).with_credentials(UserCredential(username, password))

# Download the file
with open(download_path, "wb") as local_file:
    file = ctx.web.get_file_by_server_relative_url(file_url)
    file.download(local_file).execute_query()

print(f"File downloaded to {download_path}")
