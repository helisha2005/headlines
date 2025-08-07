# headlines
import requests
from bs4 import BeautifulSoup


url = "https://www.reuters.com/news/archive/topNews"


headers = {
    'User-Agent': 'Mozilla/5.0'
}
response = requests.get(url, headers=headers)


soup = BeautifulSoup(response.content, "html.parser")

headlines = soup.find_all("h3", class_="story-title")  # Older class
if not headlines:
    headlines = soup.find_all("h2")  # Try a fallback

print("Top Headlines from Reuters:")
for i, headline in enumerate(headlines[:10], 1):
    print(f"{i}. {headline.get_text(strip=True)}")
