from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
driver.get("https://example.com")

# Click the button with visible text "Submit"
button = driver.find_element(By.XPATH, "//button[text()='Submit']")
button.click()






option = driver.find_element(By.XPATH, "//div[contains(@class, 'ms-list-itemLink') and contains(text(), 'Download')]")
option.click()
