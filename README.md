import requests
from bs4 import BeautifulSoup
import pandas as pd
import csv
response = requests.get('https://books.toscrape.com/catalogue/category/books/travel_2/index.html')
soup = BeautifulSoup(response.text, 'html.parser')
title = soup.find('title')
course_name = title.get_text().strip().split('|')[0].strip()
file_name = course_name + '.csv'
print(file_name)
frist_travel_book = soup.find('article',  attrs = {'class':'product_pod'})
print(frist_travel_book)
frist_travel_book_name = frist_travel_book.find('h3').get_text().strip()
print(frist_travel_book_name)
frist_travel_book_rating = frist_travel_book.find('p', attrs = {'class':'star-rating'}).get('class')[1]
print(frist_travel_book_rating)
frist_travel_book_price = frist_travel_book.find('div', attrs = {'class':'product_price'}).find('p',{'class' :"price_color"})
frist_travel_book_price = float(frist_travel_book_price.get_text().split('Â£')[1])
print(frist_travel_book_price)
travel_books = soup.find_all('article',  attrs = {'class':'product_pod'})
print(travel_books)
print(len(travel_books))
for book in travel_books :
    travel_book_name = book.find('h3').get_text().strip()
    rates = {'One' : 1 , 'Two' : 2 , 'Three' : 3 , 'Four' : 4 , 'Five' : 5}
    travel_book_rating = rates[book.find('p', attrs = {'class':'star-rating'}).get('class')[1]]
    travel_book_price = book.find('div', attrs = {'class':'product_price'}).find('p',{'class' :"price_color"})
    travel_book_price = float(travel_book_price.get_text().split('Â£')[1])
    print(f'Name : {travel_book_name} ||  Rating : {travel_book_rating} || Price :{travel_book_price}')
    print('---'*40)
