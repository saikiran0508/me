from ldap3 import Server, Connection, ALL
import shutil

# Define LDAP server details
server_address = 'your_ldap_server_address'
server_port = 389  # Default LDAP port
username = 'your_username'
password = 'your_password'

# Define paths
local_file_path = 'path_to_your_excel_file.xlsx'
ad_folder_path = 'path_to_your_active_directory_folder'

# Establish connection to LDAP server
server = Server(server_address, port=server_port, get_info=ALL)
conn = Connection(server, user=username, password=password, auto_bind=True)

# Copy the file to the Active Directory folder
shutil.copy(local_file_path, ad_folder_path)

# Close the connection
conn.unbind()
