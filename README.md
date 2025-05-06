import os
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

# Set download directory
download_dir = "/path/to/downloads"

# Configure Chrome options
chrome_options = Options()
chrome_options.add_experimental_option("prefs", {
    "download.default_directory": download_dir,
    "download.prompt_for_download": False,
    "download.directory_upgrade": True,
    "safebrowsing.enabled": True
})

# Initialize driver
driver = webdriver.Chrome(options=chrome_options)

def is_download_completed(download_path):
    """
    Wait until there are no .crdownload (or .part) files in the folder.
    """
    while True:
        time.sleep(1)  # Wait a bit before checking
        if not any(fname.endswith(".crdownload") for fname in os.listdir(download_path)):
            return True

# Sample loop for multiple files
for url in file_urls:
    driver.get(url)  # Or interact with page to reach download
    driver.find_element("id", "download_button").click()

    # Wait for new tab to open
    time.sleep(1)
    driver.switch_to.window(driver.window_handles[-1])  # Switch to download tab

    # Wait for download to complete
    is_download_completed(download_dir)

    # Close the download tab and return to main
    driver.close()
    driver.switch_to.window(driver.window_handles[0])
