# Web-Scraping
Web scraping wikipedia website using python to gather information and saving it as CSV

from bs4 import BeautifulSoup
import requests
import pandas as pd

url = 'https://en.wikipedia.org/wiki/List_of_companies_of_Nigeria'
page = requests.get(url)
soup=BeautifulSoup(page.text, 'html')

soup.find('table')

soup.find_all('table')[1]

soup.find('table', class_ = 'wikitable sortable')

table = soup.find_all('table')[1]

(table)

companies = table.find_all('th')

companies

companies = [table.text.strip() for table in companies]

companies

df = pd.DataFrame(columns = companies)

df

column = table.find_all('tr')
for row in column[1:]:
    row_data = row.find_all('td')
    companies_row_data = [data.text.strip() for data in row_data]
    
    length = len(df)
    df.loc[length] =  companies_row_data

df.to_csv(r'C:\Users\PC\Documents\web_scraping\companies.csv', index = False)




