# Web-Scraping
Web scraping wikipedia website using python to gather information and saving it as CSV

Importing beautiful soup 

from bs4 import BeautifulSoup

Importing requests 

import requests

Importing pandas

import pandas as pd

inserting the url/webpage for webcraping

url = 'https://en.wikipedia.org/wiki/List_of_companies_of_Nigeria'
page = requests.get(url)
soup=BeautifulSoup(page.text, 'html')

extracting the webpage

soup.find('table')

extracting the exact table that is needed

soup.find_all('table')[1]

extracting the exact table that is needed

soup.find('table', class_ = 'wikitable sortable')

extracting the exact table that is needed and saving it as variable 'table'

table = soup.find_all('table')[1]

checking out the table

(table)

saving it as variable 'companies'

companies = table.find_all('th')

checking out the variable 'companies'

companies

striping off the unneeded information

companies = [table.text.strip() for table in companies]

checking it out

companies

saving it as a dataframe

df = pd.DataFrame(columns = companies)

checking out the dataframe

df

extracting the other data(body) of the information and joining it with the titles

column = table.find_all('tr')
for row in column[1:]:
    row_data = row.find_all('td')
    companies_row_data = [data.text.strip() for data in row_data]
    
    length = len(df)
    df.loc[length] =  companies_row_data

saving it as a csv file

df.to_csv(r'C:\Users\PC\Documents\web_scraping\companies.csv', index = False)




