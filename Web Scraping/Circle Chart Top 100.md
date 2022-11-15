## PyMySQL을 이용한 MySQL 테이블 Circle Chart Top 100 insert code

국내 차트인 Melon Top100과 비교하기 위해 해외 점수가 포함된 타 플랫폼인 Circle Chart의 데이터를 준비

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

### 서클차트 2022년 

```py
link = 'https://circlechart.kr/page_chart/onoff.circle?serviceGbn=ALL&termGbn=week'

driver = webdriver.Chrome()
driver.get(link)

time.sleep(3)

html = driver.page_source

driver.close()
driver.quit()

bs = BeautifulSoup(html, 'lxml')

music_names = bs.find_all('div', {'class':'font-bold mb-2'})[:100]
names = bs.find_all('div',{'class':'text-sm text-gray-400 font-bold'})[:100]
agency = bs.find_all('td',{'class':'text-left text-xs'})[:100]
rank = 1

for i in range(len(names)):
    sql = f"""
    INSERT INTO circle_digital_chart_top100 VALUES(
    {rank}, "{music_names[i].text}","{names[i].text}", "{agency[i].find('span').text}",2022);
    """
    
    cursor.execute(sql)
    rank += 1
```

### 서클차트 2012~2021

```py
year = 2012
rank = 1

for i in range(10):
    rank = 1
    link = f'https://circlechart.kr/page_chart/onoff.circle?nationGbn=K&serviceGbn=ALL&targetTime={year}&hitYear={year}&termGbn=year&yearTime=3'
    
    driver = webdriver.Chrome()
    driver.get(link)
    
    time.sleep(3)
    
    html = driver.page_source
    
    driver.close()
    driver.quit()
    
    bs = BeautifulSoup(html, 'lxml')
    
    music_names = bs.find_all('div', {'class':'font-bold mb-2'})[:100]
    names = bs.find_all('div',{'class':'text-sm text-gray-400 font-bold'})[:100]
    agency = bs.find_all('td',{'class':'text-left text-xs'})[:100]
    
    for i in range(len(names)):
        sql = f"""
        INSERT INTO circle_digital_chart_top100 VALUES(
        {rank}, "{music_names[i].text}","{names[i].text}", "{agency[i].find('span').text}",{year});
        """
        
        cursor.execute(sql)
        rank += 1
        
    year += 1
    
db.commit()
db.close()
```
