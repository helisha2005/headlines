# headlines
import requests
from bs4 import BeautifulSoup

# URL of Reuters top news
url = "https://www.reuters.com/news/archive/topNews"

# Send a GET request to the website
headers = {
    'User-Agent': 'Mozilla/5.0'
}
response = requests.get(url, headers=headers)

# Parse the HTML content
soup = BeautifulSoup(response.content, "html.parser")

# Find headline containers
headlines = soup.find_all("h3", class_="story-title")  # Older class
if not headlines:
    headlines = soup.find_all("h2")  # Try a fallback

# Print the top headlines
print("Top Headlines from Reuters:")
for i, headline in enumerate(headlines[:10], 1):
    print(f"{i}. {headline.get_text(strip=True)}")
