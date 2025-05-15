import win32com.client
import os
from datetime import datetime

# === CONFIGURATION ===
SAVE_FOLDER = r"C:\Your\Target\Folder"  # Change to your desired folder path
KEYWORD = "Daily Report"  # Optional: Filter by subject or keyword in subject
ONLY_TODAY = True  # Set to False to get attachments from all time

# === SCRIPT ===
outlook = win32com.client.Dispatch("Outlook.Application").GetNamespace("MAPI")
inbox = outlook.GetDefaultFolder(6)  # 6 = Inbox

messages = inbox.Items
messages.Sort("[ReceivedTime]", True)  # Sort latest first

today = datetime.today().date()
downloaded = 0

for message in messages:
    try:
        if ONLY_TODAY and message.ReceivedTime.date() != today:
            break  # Stop when older emails are reached

        if KEYWORD.lower() in message.Subject.lower():
            attachments = message.Attachments
            for attachment in attachments:
                save_path = os.path.join(SAVE_FOLDER, attachment.FileName)
                attachment.SaveAsFile(save_path)
                print(f"Downloaded: {attachment.FileName}")
                downloaded += 1

    except Exception as e:
        print(f"Error processing email: {e}")

print(f"\nDone. Total attachments downloaded: {downloaded}")
