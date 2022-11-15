## PyMySQL을 이용해 MySQL 테이블에 Melon Artist Rank Top 50 데이터 insert

현재 가장 영향력있는 아티스트 50인에 대한 데이터입니다.

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

```py
link = 'https://www.melon.com/artistplus/artistchart/index.htm?chartGubunCode=DP0000%27,headers=header01'
driver = webdriver.Chrome()
driver.get(link)

for i in range(4):
    driver.find_element(By.XPATH,'//*[@id="conts"]/div[3]/div[3]/button').click()
    time.sleep(1)
    
time.sleep(3)

html = driver.page_source

driver.close()
driver.quit()

bs = BeautifulSoup(html, 'html.parser')
inx = len(bs.find_all('li',{'class':'artistplus_li'}))
ar = bs.find_all('li',{'class':'artistplus_li'})

score_ar = []
rank = 1

for i in range(inx):
    score_ar = []
    scores = ar[i].find('tr').find_next('tr').find_all('div')
    
    # 가수명
    name = ar[i].find('div',{'class':'wrap_info'}).find('a').text
    
    # 팬수
    fan = (ar[i].find('dd',{'class':'gubun'}).text.strip().replace('\t','').replace('\n',''))
    
    for score in scores:
        score_ar.append(score.text)
        
    sql = f"""
    INSERT INTO artist_rank_top50 VALUES(
    {rank}, "{name}","{fan}", {float(score_ar[0])},{float(score_ar[1])},{float(score_ar[2])},{float(score_ar[3])},{float(score_ar[4])});
    """
    
    cursor.execute(sql)
    rank +=1
    ```
