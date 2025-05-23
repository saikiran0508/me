from selenium import webdriver

# Start the driver
driver = webdriver.Chrome()

# Open a website
driver.get("https://www.google.com")

# Open a new tab using JavaScript
driver.execute_script("window.open('');")

# Switch to the new tab
driver.switch_to.window(driver.window_handles[1])

# Open another URL in the new tab
driver.get("https://www.bing.com")
