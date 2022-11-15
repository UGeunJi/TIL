## PyMySQL 이용해서 MySQL 테이블에 Melon Chart Top 100 데이터 INSERT 하기

- 동적인 사이트라 BeautifulSoup만으론 데이터가 insert되지 않아서 selenium 사용<br>
- 2022년도 데이터는 아직 2022년이 지나지 않아 년 단위는 집계되지 않았기 때문에 2022년 10/31 ~ 11/6일의 주간 데이터로 대체했습니다.

### 2012 ~ 2021 Melon Chart Top 100 insert code
```py
import selenium

from bs4 import BeautifulSoup
import requests
from selenium import webdriver
import time
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
```



```py
import pymysql

db = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='1234', db='melon', charset='utf8')

cursor = db.cursor()
    
for year in range(2012, 2022):
    link = "https://www.melon.com/chart/age/index.htm?chartType=YE&chartGenre=KPOP&chartDate={}#params%5Bidx%5D=1".format(year)

    driver = webdriver.Chrome()
    driver.get(link)

    html = driver.page_source

    time.sleep(3)
    driver.close()
    driver.quit()
    bs = BeautifulSoup(html, 'lxml')

    idx = len(bs.find_all('tr', {'class':'lst50'}))
    idx2 = len(bs.find_all('tr', {'class':'lst100'}))
    tr_all = bs.find_all('tr', {'class':'lst50'})
    tr_all2 = bs.find_all('tr', {'class':'lst100'})

    rank = 1
    
    for i in range(0, idx):
        song_name = tr_all[i].find('div', {'class':'ellipsis rank01'}).text.strip()
        singer_name = tr_all[i].find('div',{'class':'ellipsis rank02'}).find('a').text.strip()
        likes = tr_all[i].find('span', {'class':'cnt'}).text.replace('\n', ' ')
        sql = """INSERT INTO top100 VALUES(
        {0}, {1}, "{2}", "{3}", "{4}");""".format(year, rank, song_name, singer_name, likes)
    
        rank += 1
        cursor.execute(sql)
    
    for i in range(0, idx2):
        song_name = tr_all2[i].find('div', {'class':'ellipsis rank01'}).text.strip()
        singer_name = tr_all2[i].find('div',{'class':'ellipsis rank02'}).find('a').text.strip()
        likes = tr_all2[i].find('span', {'class':'cnt'}).text.replace('\n', ' ')
        sql = """INSERT INTO top100 VALUES(
        {0}, {1}, "{2}", "{3}", "{4}");""".format(year, rank, song_name, singer_name, likes)
    
        rank += 1
        cursor.execute(sql)

db.commit()
db.close()
```

### 2022 Melon Chart Top 100 insert code
```py
import selenium

from bs4 import BeautifulSoup
import requests
from selenium import webdriver
import time
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys

import pymysql

db = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='1234', db='melon', charset='utf8')

cursor = db.cursor()

link = "https://www.melon.com/chart/week/index.htm"

driver = webdriver.Chrome()
driver.get(link)

html = driver.page_source

time.sleep(3)
driver.close()
driver.quit()
bs = BeautifulSoup(html, 'lxml')
    
idx = len(bs.find_all('tr', {'class':'lst50'}))
idx2 = len(bs.find_all('tr', {'class':'lst100'}))
tr_all = bs.find_all('tr', {'class':'lst50'})
tr_all2 = bs.find_all('tr', {'class':'lst100'})

rank = 1
year = 2022
for i in range(0, idx):
    song_name = tr_all[i].find('div', {'class':'ellipsis rank01'}).text.strip()
    singer_name = tr_all[i].find('div',{'class':'ellipsis rank02'}).find('a').text.strip()
    likes = tr_all[i].find('span', {'class':'cnt'}).text.replace('\n', ' ')
    sql = """INSERT INTO top100 VALUES(
    {0}, {1}, "{2}", "{3}", "{4}");""".format(year, rank, song_name, singer_name, likes)
    
    rank += 1
    cursor.execute(sql)
    
for i in range(0, idx2):
    song_name = tr_all2[i].find('div', {'class':'ellipsis rank01'}).text.strip()
    singer_name = tr_all2[i].find('div',{'class':'ellipsis rank02'}).find('a').text.strip()
    likes = tr_all2[i].find('span', {'class':'cnt'}).text.replace('\n', ' ')
    sql = """INSERT INTO top100 VALUES(
    {0}, {1}, "{2}", "{3}", "{4}");""".format(year, rank, song_name, singer_name, likes)
    
    rank += 1
    cursor.execute(sql)

db.commit()
db.close()
```
