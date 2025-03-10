import requests
from bs4 import BeautifulSoup

base_url = 'http://books.toscrape.com/catalogue/page-{}.html'
page = 1
prices = []

while True:
    response = requests.get(base_url.format(page))
    soup = BeautifulSoup(response.text, 'html.parser')
    books = soup.find_all('article', class_='product_pod')

    if not books:
        break

    for book in books:
        price = book.find('p', class_='price_color').text.strip()
        prices.append(price)

    page += 1

for price in prices:
    print(price)
