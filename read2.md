import requests
from requests.adapters import HTTPAdapter
from requests.packages.urllib3.util.retry import Retry

def fetch_embedded_data(embedded_link):
    session = requests.Session()
    retries = Retry(total=5, backoff_factor=1, status_forcelist=[500, 502, 503, 504])
    session.mount('https://', HTTPAdapter(max_retries=retries))
    try:
        response = session.get(embedded_link)
        response.raise_for_status()
        return response.text
    except requests.exceptions.RequestException as e:
        print("Error:", e)
        return None

# Example embedded data link
embedded_link = 'YOUR_EMBEDDED_DATA_LINK_HERE'

# Fetch embedded data with retry mechanism
embedded_data = fetch_embedded_data(embedded_link)
if embedded_data:
    print("Embedded Data:", embedded_data)
else:
    print("Failed to fetch embedded data after retries.")
