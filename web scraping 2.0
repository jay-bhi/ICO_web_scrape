import pandas as pd 
from scrapy import Selector
import requests

url = 'https://www.icocalendar.io/active-icos'
html = requests.get(url).content
sel = Selector(text = html)

Projects = sel.xpath('//div[@class = "title-block"]//text()').extract()
Projects = pd.DataFrame(Projects)
project_x = {'Project':Projects[0]}
project_x = pd.DataFrame(project_x)
needed_data = project_x[project_x['Project'] != 'Text Link']

project_x_needed_data = pd.DataFrame(needed_data)

project_name = needed_data.head(100)
project_name = project_name.reset_index()
project_name = project_name.rename(columns = {'index':'S/N'})
#print(project_name)

#trash = needed_data['Project'].tail(12)

Types = sel.xpath('//a[@class = "card-blck"]//text()').extract()
Types = pd.DataFrame(Types)
Types = {'Types': Types[0]}
Types = pd.DataFrame(Types)
Types = Types.reset_index()
Types = Types.rename(columns = {'index': 'S/N'})

#print(Types)

PROJECT = project_name.merge(Types, on = 'S/N')
#print(PROJECT)

crypto_web_scrape = pd.read_csv(r'C:\Users\HP\Desktop\VS code Python files\crypto.csv')
crypto_web_scrape = crypto_web_scrape.reset_index()
crypto_web_scrape = crypto_web_scrape.rename(columns = {'index':'S/N'})

CRYPTO_Data = PROJECT.merge(crypto_web_scrape, on = 'S/N')
CRYPTO_Data = CRYPTO_Data.drop(columns = 'Launch Type')
CRYPTO_Data = CRYPTO_Data.rename(columns = {'Types':'Launch Type'})
#print(CRYPTO_Data)
#print(CRYPTO_Data.info())
#print(crypto_web_scrape.head(10))
#print(crypto_web_scrape.info())

CRYPTO_Data.to_csv('Crypto_Data.csv')



