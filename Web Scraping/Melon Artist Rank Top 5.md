## PyMySQL을 이용해 MySQL 테이블에 Melon Artist Top 5 데이터 insert

현재 아티스트 Top 5 그룹의 점수, 팬 성비, 팬 나이대의 데이터 insert (2022/11/16일 기준)

### import 부분
```py
import pymysql
from bs4 import BeautifulSoup
import requests
from selenium import webdriver
import time
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
```

### db 선언 부분
```py
db = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='1234', db='melon', charset='utf8')
cursor = db.cursor()
```

### BeautifulSoup 선언 부분
```py
user_agent = "Mozilla/5.0"

header01 = {"User-Agent" : user_agent}
response = requests.get('https://www.melon.com/artistplus/artistchart/index.htm?chartGubunCode=DP0000',headers=header01)
response.raise_for_status()

bs = BeautifulSoup(response.text, 'lxml')
ls = bs.find_all('strong',{'class':'ellipsis'})

lis = bs.find_all('div',{'class':'graph'})
inx = len(bs.find('div',{'class':'wrap_artist_chart'}).find('ul').find_all('li'))

b = []
rank = 1

for i in range(1, inx+1):
    b = []
    name = ls[i-1].text
    t = f"artist rank{i}"
    per = bs.find('p',{'class':t}).text.strip()
    for li in lis[i-1].find_all('li'):
        b.append(li.find('span',{'class':'graph_bar'}).text)
    sql = f"""
    INSERT INTO artist_rank_top5 VALUES(
    {rank}, "{per}","{name}", "{b[0]}","{b[1]}","{b[3]}","{b[4]}","{b[5]}","{b[6]}","{b[7]}","{b[8]}");
    """
    cursor.execute(sql)
    rank += 1
```
