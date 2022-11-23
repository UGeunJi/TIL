**requests 모듈**

- 참고 사이트: http://realpython.com/python-requests/
```py
import requests
```
```py
response = requests.get('http://google.com')
```
```py
response.status_code # 응답 코드: 200
```
**응답 받은 페이지가 성공적이지 않을 때**
```py
# option 1 (상태 체크)
response = requests.get('https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR')

if response.status_code == 200:
    print("status OK")
else:
    print("문제가 발생했습니다", response.status_code)
```
```py
# option 2 (Exception 발생)
response = requests.get('https://search.daum.net/searc?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR')
response.raise_for_status()

response = requests.get('http://google.com')
response.raise_for_status()
with open("mygoogle.html", 'w', encoding = 'utf8') as fd:  # utf8: unicode 인코딩 방식
    fd.write(response.text)
```
**User Agent**
- URL을 Request하는 Client의 종류를 실어 보냄
- 같은 URL을 Request 하더라도 모바일 디바이스와 PC가 받는 데이터가 다른 이유임
- Crawler 같은 자동화 프로그램이 서버에 접근하면 여러 문제가 생길 수가 있으므로 차단할 필요가 있다.
- 이 부분을 마치 Browser가 요청하듯이 바꿀 수 있는 방법이 User Agent를 조정하는 것임
- Google에서 user agent string으로 검색하면
- https://www.whatismybrowser.com/detect/what-is-my-user-agent/ 사이트에서
- 현재 브라우저의 User Agent를 표시해줌
- Client마다 서버로 보내는 정보가 다르다는 것을 확인할 수 있음
```py
user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36"

headers = {"User-Agent": user_agent}
response = requests.get("http://google.com", headers)
response.raise_for_status()
with open("mygoogle2.html", 'w', encoding = 'utf8') as fd:  # utf8: unicode 인코딩 방식
    fd.write(response.text)
```
### Workshop 1

**네이버 웹툰**
- http://comic.naver.com/webtoon/weekday
```py
user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36"

headers = {"User-Agent": user_agent}
response = requests.get("http://comic.naver.com/webtoon/weekday", headers)
response.raise_for_status()


from bs4 import BeautifulSoup

soup = BeautifulSoup(response.text, 'lxml')
```
**lxml**
- 구문분석기
- 형식을 정확히 지키지 않은 HTML 코드를 분석할 때 html.parser보다 나음
- 닫히지 않은 태그, 계층 구조가 잘못된 태그, <head>나 <body> 태그가 없는 등의 문제에서 일일이 멈추지 않고 문제를 수정
- 속도 빠름
```py
print(soup.prettify())
```
```py
soup.title
```
```py
soup.title.text
```
```py
soup.title.get_text()
```
```py
# 이 문서에서 최초로 등장한 a 태그
soup.find('a')
```
```py
soup.a.attrs # a 태그의 속성 모두를 알려줌
```
```py  
# "웹툰 올리기" 버튼에 해당하는 태그를 소스에서 찾기
soup.find('a', {'class':'Nbtn_upload'})  # a 태그의 href 속성의 '값'을 출력
```
```py
soup.select_one('a.Nbtn_upload')
```
**요일별 전체 웹툰에서 제목만 모두 가져오기**
```py
user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36"

headers = {"User-Agent": user_agent}
response = requests.get("http://comic.naver.com/webtoon/weekday", headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')

soup.find_all('a', {'class':'title'})

titles = soup.find_all('a', {'class':'title'})

titles
```
```py
titles = soup.find_all('a', {'class':'title'})
for title in titles:
    print(title.text)
```
```py
titles = soup.select('a.title')
for title in titles:
    print(title.text)
```
```py
soup.select('li.rank01')
```
```py  
soup.select('a.title')
```
```py  
# option 1
for i in range(1,10):
    print(soup.select_one("li.rank0{} a".format(i)).text)
```
```py  
# option 2
ol = soup.find('ol', {'id':'realTimeRankUpdate'})
lis = ol.find_all('li')
for li in lis:
    a = li.find('a')
    print(a.text)
```
```py  
# option 3
ranks = soup.select('ol#realTimeRankFavorite li a')
for rank in ranks:
    print(rank.text)
```
**만화 '독립일기'의 제목, 링크, 평점 가져오기**

#### 한 페이지만 파싱
```py
headers = {"User-Agent": user_agent}
response = requests.get("https://comic.naver.com/webtoon/list?titleId=748105&weekday=thu", headers)
response.raise_for_status()

soup = BeautifulSoup(response.text, 'lxml')

titles = soup.select('td.title')
for title in titles:
    print(title.text)

tt = soup.find('td', {'class':'title'})
for href in tta:
    a = href.find('a')
    print(a['href'])

tt = soup.find('td', {'class':'title'})

tta

tt.a['href']
```
---
```py
# find문 사용

tds = soup.find_all('td', {'class':'title'})
for td in tds:
    a = td.find('a')
    print(a.get_text())
    print('http://comic.naver.com/' + a['href'])

total_rate = 0

divs = soup.find_all('div', {'class':'rating_type'})
for div in divs:
    strong = div.find('strong')
    rate = float(strong.text)

    total_rate = total_rate + rate
print(total_rate/len(divs))
```
```py
# select 사용

titles = soup.select('td.title a')
for title in titles:
    print(title.text)
    print('http://comic.nvaver.com' + title['href'])

total_s = 0

divis = soup.select('div.rating_type strong')
for divv in divis:
    total_s += float(divv.text)
print(total_s / len(divis))
```
```py
# select 사용

titles = soup.select('td.title a')
total_s = 0

divis = soup.select('div.rating_type strong')
for title, divv in zip(titles, divis):
    print(title.text)
    print('http://comic.nvaver.com' + title['href'])
    total_s += float(divv.text)
print(total_s / len(divis))
```
```py
# 여러 페이지 데이터 파싱
for page in range(1, 22):
    url = "https://comic.naver.com/webtoon/list?titleId=748105&weekday=thu&page={}".format(page)

    headers = {"User-Agent": user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()
    
    soup = BeautifulSoup(response.text, 'lxml')
    
    titles = soup.select('td.title a')
    
    for title in titles:
        print(title.text)
        print('http://comic.nvaver.com' + title['href'])

    total_s = 0

    divis = soup.select('div.rating_type strong')
    for divv in divis:
        total_s += float(divv.text)
    print(total_s / len(divis))
    
    print("{} page".format(page))
    print("평균 평점: ", total_s/len(divis))
    print()
    print('*'*100)
```    
    
```py
imgs = soup.select('div.wrap_thumb > a > img')
for img in imgs:
    print(img['src'])
```
### Workshop 2

**다음(daum.net)에서 2021년 영화순위 검색**
- https://search.daum.net/search?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR
- 1. 2021년도의 이미지 링크를 출력
- 2. 2021 ~ 2010 이미지 링크 출력
- 3. 해당 링크 이미지를 요청해서 파일로 저장(response.content: 이진 데이터)
```py
# 1번
url = "https://search.daum.net/search?w=tot&q=2021%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR"

headers = {"User-Agent": user_agent}
response = requests.get(url, headers)
response.raise_for_status()
    
soup = BeautifulSoup(response.text, 'lxml')

cl = soup.find('ol', {'class':'type_plural list_exact movie_list'})

imgs = cl.select('div.wrap_thumb > a > img')
for img in imgs:
    print(img['src'])

url = "https://search.daum.net/search?w=tot&q=2020%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR"

headers = {"User-Agent": user_agent}
response = requests.get(url, headers)
response.raise_for_status()
    
soup = BeautifulSoup(response.text, 'lxml')

cl = soup.find('ol', {'class':'type_plural list_exact movie_list'})

imgs = cl.select('div.wrap_thumb img')
for img in imgs:
    print(img['src'])
```
```py  
# 2번

for year in range(2021, 2010, -1):
    url = "https://search.daum.net/search?w=tot&q={}%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR".format(year)
    
    headers = {"User-Agent": user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()

    soup = BeautifulSoup(response.text, 'lxml')
    
    cl = soup.find('ol', {'class':'type_plural list_exact movie_list'})
   
    imgs = cl.select('div.wrap_thumb > a > img')
    for img in imgs:
        print(img['src'])
```
```py  
# 3번
for year in range(2021, 2010, -1):
    url = "https://search.daum.net/search?w=tot&q={}%EB%85%84%EC%98%81%ED%99%94%EC%88%9C%EC%9C%84&DA=MOR&rtmaxcoll=MOR".format(year)
    
    headers = {"User-Agent": user_agent}
    response = requests.get(url, headers)
    response.raise_for_status()

    soup = BeautifulSoup(response.text, 'lxml')
    
    cl = soup.find('ol', {'class':'type_plural list_exact movie_list'})
   
    imgs = cl.select('div.wrap_thumb > a > img')
    for i, img in enumerate(imgs):  # 30장의 이미지
        image_url = img['src']
        image_res = requests.get(image_url, headers)
        response.raise_for_status()
        
        with open('./image/{}movie_rank_{}.jpg'.format(year, i + 1), 'wb') as fd:
            fd.write(image_res.content)
```
```py
pwd
```
**셀레니움**
- 웹 페이지 테스트 자동화를 할 수 있는 프레임워크
- 셀레니움을 사용하면 완전한 형태의 웹 페이지 소스를 볼 수 있기 때문에 scraping할 때 유용

**사용 예**
- 자바 스크립트가 동적으로 만든 데이터를 scraping할 때
- 사이트의 다양한 HTML 요소에 클릭, 키보드 입력 등 이벤트를 줄 때

**사용 방법**
- 셀레니움을 사용하려면 사용 중인 웹 브라우저의 드라이버 파일을 다운로드 해야 함
- 크롬 드라이버 파일 다운로드 받기
```
chrome://version/버전 확인
http://chromedriver.chromium.org/downloads에서 chrome 버전과 운영체제에 맞는 드라이버 다운로드 압축 푼 뒤 응용 프로그램을 현재 작업 디렉토리에 복사
```

- selenium 설치
```
conda install selenium
```

**참고사이트**
```
http://www,selenium.dev/documentation/webdriver
```
```py
from IPython.display import Image
Image('webdriver.png')
```
**find_element_by_tag_name**
```py
import selenium
```
```py
from selenium import webdriver
```
```py  
driver = webdriver.Chrome() # driver가 있는 path를 넣어줄 수 있음
```
```py
driver.get("http://naver.com")
```
#### find_element_by_tag_name를 통해 a tag에 접근
#### href 정보까지도 조회
```py
elem = driver.find_element_by_tag_name('a')
```
```py  
elem.get_attribute('href')
```
  
#### 여러 tag를 가져올 때는 find_elements_by_tag_name
```py
elems = driver.find_elements_by_tag_name('a')
for elem in elems:
    print(elem.get_attribute('href'))

driver.quit()
```



```py
driver.back()
```
```py
driver.forward()
```
```py  
driver.refresh()
```
```py  
driver.close()  # brower가 종료
```
```py  
driver.quit()  # brower, driver 종료
```
- 더 자세한 내용은
```
https://www.selenium.dev/documentation/webdriver/elements/
```

**find_element_by_id**
```py
driver = webdriver.Chrome()
```
```py  
driver.get("http://naver.com")
```
```py  
elem = driver.find_element_by_id('query')
```
```py  
elem.send_keys("파이썬")
```
```py  
from selenium.webdriver.common.keys import Keys
elem.send_keys(Keys.ENTER)
```
```py  
elem = driver.find_element_by_tag_name('a')
```
```py  
driver.quit()  # brower, driver 종료
```
**find_element_by_name**
```py
driver = webdriver.Chrome()
driver.get("http://naver.com")
```
```py  
elem = driver.find_element_by_name('query')
elem.send_keys("파이썬")
```
```py  
elem = driver.find_element_by_id('search_btn')
elem.click()
```
**find_element_by_xpath**
```py
elem = driver.find_element_by_xpath('//*[@id="search_btn"]')
elem.click()
```
```py  
driver.quit()
```
```py
# Element를 찾는 데 필요한 함수들
# driver.find_element_by_id
# driver.find_element_by_name
# driver.find_element_by_tag_name
# driver.find_element_by_xpath
# driver.find_element_by_css_selector
```
### Workshop 1

- 네이버 로그인
```py
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 네이버 사이트 이동
driver.get("http://naver.com")

# 로그인 버튼
elem = driver.find_element_by_xpath('//*[@id="account"]/a')
elem.click()

# id / password
elem = driver.find_element_by_id('id')
elem.send_keys("ajtwlsdnrms")

elem = driver.find_element_by_id('pw')
elem.send_keys("wjdrms123!@#")

# 로그인 버튼
elem = driver.find_element_by_xpath('//*[@id="log.login"]')
elem.click()

driver.quit()
```
---
```py
import time

options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 네이버 사이트 이동
driver.get("http://naver.com")

# 로그인 버튼
elem = driver.find_element_by_css_selector('a.link_login')
elem.click()

# id / password
elem = driver.find_element_by_id('id')
elem.send_keys("ajtwlsdnrms")
time.sleep(2)

elem = driver.find_element_by_id('pw')
elem.send_keys("wjdrms123!@#")
time.sleep(1)

elem = driver.find_element_by_id('log.login')
elem.click()

# 종료
driver.quit()
```
### Workshop 2

**구글 이미지 검색**
```py
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

# 구글 이미지 검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

keyword = '딸기'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit()  # elem.send_keys(Keys_ENTER)과 동일

# 작은 이미지 클릭
image_elem = driver.find_element_by_css_selector('img.rg_i.Q4LuWd')
image_elem.click()

# 오른쪽에 있는 큰 이미지의 주소를 흭득
image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
image_url = image_elem.get_attribute('src')
print(image_url)

# 이미지 주소로 request해서 응답받은 이미지를 저장
import requests

user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36"

headers = {"User-Agent": user_agent}
response = requests.get(image_url, headers)
response.raise_for_status()

with open('./strawberry/1.jpg', 'wb') as fd:
            fd.write(response.content)
```
```py
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47')

driver = webdriver.Chrome(options=options)

# 구글 이미지검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

# 검색
keyword = '감자'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit() # elem.send_keys(Keys.ENTER) 와 동일

# 작은 이미지 클릭
image_elems= driver.find_elements_by_css_selector('img.rg_i.Q4LuWd')

count = 1
for image_elem in image_elems:
    image_elem.click()
    time.sleep(2)

    # 오른쪽에 있는 큰 이미지의 주소를 획득
    image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
    image_url = image_elem.get_attribute('src')
    print(image_url)

    # 이미지 주소로 request 해서 응답받은 이미지를 저장
    import requests

    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47"

    headers = {"User-Agent" : user_agent}
    response = requests.get(image_url, headers)
    response.raise_for_status()

    with open('./potato/{}.jpg'.format(count), 'wb') as fd:
                fd.write(response.content)
    count += 1
    if count > 10:
        break

driver.quit()
```
- 사용자의 Scroll 반영
```py
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47')

driver = webdriver.Chrome(options=options)

# 구글 이미지검색 사이트 이동
driver.get("https://www.google.co.kr/imghp?hl=ko&tab=ri&ogbl")

# 검색
keyword = '감자'
elem = driver.find_element_by_name('q')
elem.send_keys(keyword)
elem.submit() # elem.send_keys(Keys.ENTER) 와 동일

# Java Script의 스크롤 기능을 통해서 더 많은 이미지를 가져옴
prev_height = driver.execute_script('return document.body.scrollHeight')
print(prev_height)

while True:
    driver.execute_script('window.scrollTo(0, document.body.scrollHeight)')
    time.sleep(1)
    curr_height = driver.execute_script('return document.body.scrollHeight')
    print(curr_height)
    if prev_height == curr_height:
        break
    prev_height = curr_height

# 작은 이미지 클릭
image_elems= driver.find_elements_by_css_selector('img.rg_i.Q4LuWd')

count = 1
for image_elem in image_elems:
    image_elem.click()
    time.sleep(2)

    # 오른쪽에 있는 큰 이미지의 주소를 획득
    image_elem = driver.find_element_by_xpath('//*[@id="Sva75c"]/div/div/div[3]/div[2]/c-wiz/div/div[1]/div[1]/div[3]/div/a/img')
    image_url = image_elem.get_attribute('src')
    print(image_url)

    # 이미지 주소로 request 해서 응답받은 이미지를 저장
    import requests

    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36 Edg/106.0.1370.47"

    headers = {"User-Agent" : user_agent}
    response = requests.get(image_url, headers)
    response.raise_for_status()

    with open('./potato/{}.jpg'.format(count), 'wb') as fd:
                fd.write(response.content)
    count += 1
    if count > 30:
        breakdriver.quit()

driver.quit()
```
**구글 무비**
- https://play.google.com/store/movies/top
- 스크롤된 모든 데이터에 대해
- 가격이 할인된 영화만 출력하되
- 출력 양식 : 영화제목, 할인전/후 가격, 링크
```py
# 1. 첫 화면 접속
options = webdriver.ChromeOptions()
options.add_argument('user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.0.0 Safari/537.36')

driver = webdriver.Chrome(options=options)

driver.get("https://play.google.com/store/movies/top")
```
```py  
# 2. 화면 스크롤
while True:
    driver.execute_script('window.scrollTo(0, document.body.scrollHeight)')
    time.sleep(1)
    curr_height = driver.execute_script('return document.body.scrollHeight')
    print(curr_height)
    if prev_height == curr_height:
        break
    prev_height = curr_height


driver.page_source
```
```py  
# 3. 필요한 정보 가져오기 위한 구문 분석
soup = BeautifulSoup(driver.page_source, 'lxml')

# print(soup.prettify)

movies = soup.select('div.VfPpkd-EScbFb-JIbuQc.UVEnyf')

len(movies)

count = 0
for movie in movies:
    # 영화 제목
    title = movie.select_one('div.Epkrse')
    title = title.text

    # 할인 전 가격
    original_price = movie.select_one('span.SUZt4c.P8AFK')
    if original_price:
        original_price = original_price.text
        
    else:    # 할인 전 가격이 없으면 세일하는 항목이 아님 
        continue
    
    # 할인 후 가격
    discount_price = movie.select_one('span.VfPpfd.VixbEe')
    discount_price = discount_price.text

    # 링크 정보
    link = movie.select_one('a.Si6A0c.ZD8Cqc')
    link = 'http://play.google.com' + link['href']
    link
    
    print('제목: ', title)
    print('할인 전 가격: ', original_price)
    print('할인 후 가격: ', discount_price)
    print('링크 정보: ', link)
    print('*' * 100)
    count += 1
print(count)

driver.quit()
```
