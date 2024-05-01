import paramiko
import re
import os

# Define the connection parameters
hostname = 'your_server_hostname'
port = 22
username = 'your_username'
password = 'your_password'

# Define the directory on the server where the files are located
remote_directory = '/path/to/remote/directory/in/winscp'

# Define the countries and report names you want to filter for
countries = ['Country1', 'Country2']  # Add more countries if needed
report_names = ['Gen01', 'Gen04']  # Add more report names if needed

# Create an SSH client
ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

# Connect to the server
ssh.connect(hostname, port, username, password)

# Create an SCP client
scp = ssh.open_sftp()

# List files in the remote directory
files = scp.listdir(remote_directory)

# Filter files based on country and report name
filtered_files = {}
for file_name in files:
    for country in countries:
        for report_name in report_names:
            regex_pattern = fr"{country}_{report_name}_\d{{2}}[A-Z]{{3}}\d{{4}}"  # regex for filename format
            if re.match(regex_pattern, file_name):
                if country not in filtered_files:
                    filtered_files[country] = []
                filtered_files[country].append(file_name)

# Define local directory to save downloaded files
local_directory = '/path/to/local/directory'

# Download filtered files and segregate by country
for country, files in filtered_files.items():
    country_directory = os.path.join(local_directory, country)
    os.makedirs(country_directory, exist_ok=True)
    for file_name in files:
        remote_file_path = f"{remote_directory}/{file_name}"
        local_file_path = os.path.join(country_directory, file_name)
        scp.get(remote_file_path, local_file_path)
        print(f"Downloaded {file_name} for {country}")

# Close the SCP and SSH clients
scp.close()
ssh.close()

print("All files downloaded successfully.")
