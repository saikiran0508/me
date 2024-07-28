from exchangelib import Credentials, Account, DELEGATE, FileAttachment
from datetime import datetime, timedelta

# Define your credentials
email = 'your_email@example.com'
password = 'your_password'

# Connect to the account
credentials = Credentials(email, password)
account = Account(email, credentials=credentials, autodiscover=True, access_type=DELEGATE)

# Define the sender and time range (e.g., the last 30 days)
sender_email = 'specific_sender@example.com'
time_range = datetime.now() - timedelta(days=30)

# Find items from the specific sender within the time range
for item in account.inbox.filter(datetime_received__gte=time_range, sender=sender_email).order_by('-datetime_received'):
    for attachment in item.attachments:
        if isinstance(attachment, FileAttachment):
            local_path = f'/path/to/save/{attachment.name}'
            with open(local_path, 'wb') as f:
                f.write(attachment.content)
            print(f'Saved attachment to {local_path}')

print('Finished downloading attachments.')
