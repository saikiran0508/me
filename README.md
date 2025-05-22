from office365.sharepoint.client_context import ClientContext
from office365.runtime.auth.authentication_context import AuthenticationContext

site_url = "https://yourcompany.sharepoint.com/sites/yoursite"
username = "your_email@yourcompany.com"
password = "your_password"

ctx_auth = AuthenticationContext(site_url)
if ctx_auth.acquire_token_for_user(username, password):
    ctx = ClientContext(site_url, ctx_auth)
    file_url = "/sites/yoursite/Shared Documents/filename.xlsx"
    download_path = "filename.xlsx"

    with open(download_path, "wb") as output_file:
        ctx.web.get_file_by_server_relative_url(file_url).download(output_file).execute_query()
    print("Download completed.")
else:
    print("Authentication failed.")
