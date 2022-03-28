# web-scrapping

from bs4 import BeautifulSoup
import requests
from csv import writer

url = "https://clutch.co/directory/mobile-application-developers"
page = requests.get(url)

soup = BeautifulSoup(page.content, 'html.parser')
lists = soup.find_all('section', class_="container")

with open('housing.csv', 'w', encoding='utf8', newline='') as f:
    thewriter = writer(f)
    header = ['Title', 'Location', 'rating', 'rate']
    thewriter.writerow(header)

    for list in lists:
        title = list.find('h3', class_="company_info").text.replace('\n', '')
        location = list.find('div', class_="list-item custom_popover").text.replace('\n', '')
        rating = list.find('div', class_="rating-reviews sg-rating").text.replace('\n', '')
        rate = list.find('div', class_="list-item custom_popover").text.replace('\n', '')


        info = [title, location, rating, rate ]
        thewriter.writerow(info)
