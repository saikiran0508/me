from pyad import *

# Connect to Active Directory
pyad.set_defaults(ldap_server="your_ldap_server_address")

# Specify the path where you want to upload the file
adroot_path = "LDAP://your_adroot_path"
adroot_folder = pyad.adcontainer.ADContainer.from_dn(adroot_path)

# Define the file path of the file to upload
local_file_path = "path_to_local_file"
file_name = "file_name.txt"

# Upload the file to the Active Directory root
with open(local_file_path, 'rb') as f:
    adroot_folder.upload(file_name, f.read())
