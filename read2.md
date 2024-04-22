import paramiko

try:
    # Set up SSH client
    ssh_client = paramiko.SSHClient()
    ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

    # Connect to the SSH server
    ssh_client.connect(hostname='your_host', port=22, username='your_username', password='your_password')

    print("Connection successful!")

    # If the connection is successful, you can proceed with your other operations here
    
    # Close the SSH connection
    ssh_client.close()

except paramiko.SSHException as e:
    print("Error:", e)
