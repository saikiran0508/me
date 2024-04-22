import paramiko
import tempfile
import os

# Set up SSH client
ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

# Connect to the SSH server
ssh_client.connect(hostname='your_host', port=22, username='your_username', password='your_password')

# Create an SCP client
scp_client = ssh_client.open_sftp()

# Specify remote file path
remote_file_path = '/path/to/remote/file.xlsx'

# Create a temporary file
temp_file = tempfile.NamedTemporaryFile(delete=False)
temp_file_path = temp_file.name

try:
    # Download the file to the temporary file
    scp_client.get(remote_file_path, temp_file_path)
    
    # Close the SCP client and SSH connection
    scp_client.close()
    ssh_client.close()

    # Now you can use the temporary file as needed
    print("File downloaded to:", temp_file_path)

    # Do whatever processing you need to do with the temporary file here

finally:
    # Close and delete the temporary file
    temp_file.close()
    os.unlink(temp_file_path)
