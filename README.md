import paramiko

# Define the SSH connection parameters
hostname = 'your_hostname'
port = 22
username = 'your_username'
password = 'your_password'

# Connect to the SSH server
ssh_client = paramiko.SSHClient()
ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh_client.connect(hostname, port, username, password)

# Open an SFTP session
sftp_client = ssh_client.open_sftp()

# Define the remote and local file paths
remote_file_path = '/path/to/remote/file.txt'
local_file_path = '/path/to/local/file.txt'

# Download the file
sftp_client.get(remote_file_path, local_file_path)

# Close the SFTP session and SSH connection
sftp_client.close()
ssh_client.close()
