from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.options import Options
import time
import pandas as pd

# Setup Chrome
options = Options()
options.add_argument("--start-maximized")
# options.add_argument("--headless")  # Use only when stable

driver = webdriver.Chrome(options=options)

# Load Qlik dashboard URL
dashboard_url = "https://qlik.yourdomain.com/some-dashboard-link"
driver.get(dashboard_url)

# Wait for Qlik to load (adjust sleep or use WebDriverWait)
time.sleep(15)

# Find all qv-objects (you can also refine to only grids if needed)
objects = driver.find_elements(By.CLASS_NAME, "qv-object")

# Loop through each qv-object to find tables
for obj in objects:
    try:
        table = obj.find_element(By.CSS_SELECTOR, ".qv-grid-object-content table")
        rows = table.find_elements(By.TAG_NAME, "tr")
        data = []
        for row in rows:
            cols = row.find_elements(By.TAG_NAME, "td")
            data.append([col.text.strip() for col in cols])
        df = pd.DataFrame(data)
        print(df.head())

        # Save to Excel (optional)
        df.to_excel("qlik_exported_data.xlsx", index=False)
        break  # remove this if multiple tables

    except Exception as e:
        continue  # Not a grid object

driver.quit()
