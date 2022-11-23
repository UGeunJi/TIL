**글자 깨지는 거 해결법**
```
<head>
    <meta charset='utf8'>    
    <title> 기초 스크레이핑 </title>
</head>
```

### 웹 크롤링의 기초개념

**웹 크롤링 vs 웹 스크래핑**

- 웹 크롤러(Web Crawler) : 웹 사이트에 있는 수많은 정보 가운데 우리가 원하는 정보를 수집하는 프로그램
- 웹 크롤링(Web Crawling) : 웹 크롤러를 이용해 데이터를 수집하는 행위
- 웹 스크래핑(Web Scraping) : 웹 사이트에서 원하는 정보를 추출하는 것은 웹 크롤링과 동일함. 그러나 전체 사이트의 데이터가 아닌 원하는 정보 **일부만**을 추출

**웹 크롤링 프로세스**

![image](https://user-images.githubusercontent.com/84713532/203452418-c436e3e6-da61-48d2-aa8e-1cf62b14d1f4.png)

- 정보를 얻고자 하는 웹 사이트에 접속해 웹 페이지를 확인
- 키보드의 F12 키 또는 개발자 도구로 들어가 원하는 정보의 위치를 확인하고 분석
- 파이썬 코드를 작성해  접속한 웹 페이지의 html 코드를 불러옴
- 불러온 데이터에서 원하는 정보를 가공한 후 추출
- 추출한 정보를 csv나 데이터베이스 등 다양한 형재로 저장하거나 가공하고 시각화

**클라이언트 서버 개념**

![image](https://user-images.githubusercontent.com/84713532/203452456-9300440b-aefb-4e51-b8ae-186513f342f4.png)

**HTTP 통신의 이해**

![image](https://user-images.githubusercontent.com/84713532/203452475-35ddccba-d29b-40fb-9eab-2a8b34edff67.png)

### 웹 페이지의 구성 요소들

참고 사이트 : https://www.w3schools.com/

**1. HTML**
- 웹페이지의 뼈대

**practice.html**
```
<!doctype html>
<html>
    <head>
        <title> 기초 스크레이핑 </title>
    </head>
    <body>
        스크래핑을 해봅시다
    </body>
</html>
```

```
<!idoctype>: 문서타입이 HTML 문서라는 의미
<html>: HTML 문서의 시작과 끝을 의미, 작성하고자 하는 모든 웹 문서는 <html>과 </html> 태그 사이에 있어야 함
<head>: 웹 브라우저가 문서를 해석하는데 필요한 정보들을 입력하는 곳
<title>: 웹 브라우저의 제목 표시줄에 표시
<body>: 웹 페이지에서 보게 될 주요 정보들
```

**속성추가**
```
<img> 태그의 경우에는 속성을 추가해서 이미지의 가로길이, 세로길이 등으로 이미지의 크기를 조정할 수 있음
<img src=".\image.image01.jpg", width = "200", height = "100">

<a> 태그의 경우도 연결할 링크 정보 등을 넣을 수 있음
<a href = "http://google.com"> Google </a>
```

**종료 태그가 없는 태그들**
```
<br> 줄바꿈
<img> 이미지
<link> 링크
<imput> 사용자의 링크
```

**자주 사용하는 HTML 태그들**
```
<h1> 제목 </h1>: 큰 폰트 사용
<p> 문단 </p>: 줄바꿈 없는 한 문단
<li> 목록 </li>: 목록 만들 때 사용
<table> 표 </table>
<tr>, <td>, <th>: 테이블과 함께 표 만들 때 사용
<div> </div>: 레이아웃을 구분할 때 사용. 블록 단위 부분 공간 정의
<span> </span>: 레이아웃 구분할 때 사용. 줄 단위 부분 공간 정의
```

**html의 계층 구조**
- Tree 형태의 부모 자식 관계로 이해

**2. CSS**
- 문서의 스타일을 꾸며주는 기능

**styles/styles.css**
```
p {
    color: red;
}
```

```
위 css 코드의 의미
: 웹 페이지의 특정 요소가 <p> 태그를 사용할 때, <p> 태그의 텍스트 색상을 모두 빨강색으로 지정
```

**practice_css.html**
```
<!doctype>
<html>
    <head>
        <link href = './styles/style.css' rel = 'stylesheet' type = 'text/css'>
        <title> css 적용 </title>
    </head>
    <body>
        <p> 이 문단이 발강색으로 보여야 합니다. </p>
    </body>
</html>
```

**practice_css.html 코드 설명**
```
<link>: 외부 파일 읽을 수 있음
        href 속성을 이용하여 경로 입력
        rel 속성은 외부 리소스 종류로써 css 파일과 같이 스타일시트를 적용할 때 "stylesheet"를 사용
        type 속성은 외부 리소스의 유형 지정
        
<p>: 외부 css 파일에서 설정한 디자인 스타일이 적용 (예: 빨강색으로 변경)
```

**3. JavaScript**
- 컨텐츠를 동적으로 바꾸는 기능

###  BeautifulSoup 라이브러리
- 크롤링 하는 데 필요한 함수를 한 데 모아 놓은 라이브러리

import bs4    #BeautifulSoup의 약자

```
from 모듈 import 함수, 클래스,
```

# Workshop 1
```
from bs4 import BeautifulSoup
```
```
# 파싱할 대상 문서

html_doc = """
<!doctype html>
<html>
    <head>
        <title> 기초 스크레이핑 </title>
    </head>
    <body>
        스크래핑을 해봅시다
    </body>
</html>
"""
```
- 문서를 해석 -> "파싱"
- BeautifulSoup(파싱할 대상 문서, 구문을 분석할 엔진)
- BeautifulSoup을 이용해서 파싱을 한 후 생성된 객체를 soup이라는 변수에 담기
- 
```
soup = BeautifulSoup(html_doc, 'lxml')    # 구문분석할 엔진 html.parser, lxml
```
```
type(soup)
```
```
print(soup.prettify())
```
```
# soup.find(태그명)
soup.find('head')
```
```
soup.find('title')
```

### Workshop 2
```
# 파싱할 대상 문서

html_doc1 = """
<!doctype html>
<html>
    <head>
        <title> 기초 스크레이핑 </title>
    </head>
    <body>
        <li> 첫 번째 목록 </li>
        <li> 두 번째 목록 </li>
        <li> 세 번째 목록 </li>
    </body>
</html>
"""
```
```
soup1 = BeautifulSoup(html_doc1, 'lxml')
```
```
soup1.find('li')
```
```
li = soup1.find('li')
print(li)
print(type(li))
```
```
li.text
```
```
lis = soup1.find_all('li')
print(lis)
print(type(lis))
```

#### 파이썬 리스트와 유사하게 색인을 할 수 있음
```
lis[0]
```
```
lis[1]
```
```
lis[2]
```
```
lis[0].text
```
```
lis[2].text
```
```
for li in lis:
    print(li.text)
```
### Workshop 3
```
html_doc2 = """
<!dictype html>
<html>
    <head>
        <title> 기초 스크레이핑 </title>
    </head>
    <body>
        <table border = "10">
            <caption> 과일 가격과 개수 </caption>
            <tr>
                <th> 상품 </th>
                <th> 가격 </th>
                <th> 개수 </th>
            </tr>
            <tr>
                <td> 오렌지 </td>
                <td> 100원 </td>
                <td> 10개 </td>
            </tr>
            <tr>
                <td> 사과 </td>
                <td> 150원 </td>
                <td> 5개 </td>
            </tr>
        </table>
        <br>
        <br>
        <table border = "100">
            <caption> 옷 가격과 개수 </caption>
            <tr>
                <th> 상품 </th>
                <th> 가격 </th>
                <th> 개수 </th>
            </tr>
            <tr>
                <td> 코트 </td>
                <td> 100000원 </td>
                <td> 1벌 </td>
            </tr>
            <tr>
                <td> 바지 </td>
                <td> 150000원 </td>
                <td> 10벌 </td>
            </tr>
        </table>
    </body>
</html>
"""
```
```
soup2 = BeautifulSoup(html_doc2, 'lxml')
```
```
tables = soup2.find_all('table')
tables
```
```
# 두번째 테이블만 가져오고 싶다면 (option 1)
tables = soup2.find_all('table')
tables[1]
```
```
# 두번째 테이블만 가져오고 싶다면 (option 2)
table2 = soup2.find('table', {'border':'2'})
table2
```

### Workshop 4
```
html_doc3 = """
<!doctype html>
<html>
    <head>
        <title> 기초 스크레이핑 </title>
    </head>
    <body>
        <a href = "http://www.naver.com"> naver </a>
        <a href = "http://www.google.com"> google </a>
        <a href = "http://www.daum.net"> daum </a>
    </body>
</html>
"""
```
```
soup3 = BeautifulSoup(html_doc3, 'lxml')
```
```
a = soup3.find_all('a')
```
```
a[0].text
```
```
a[1].text
```
```
a[2].text
```
```
for i in a:
    print(i.text)
```
### Workshop 5
```
html_doc = '''
<html>
    <head>
        <meta charset = 'utf-8'>
        <title> 작품과 작가 모음</title>
    </head>
    <body>
        <h1> 책 정보 </h1>
        <p id = 'book1_title', class = 'book_title'> 토지 </p>
        <p id = 'author1', class = 'author'> 박경리 </p>
        
        <p id = 'book2_title', class = 'book_title'> 태백산맥 </p>
        <p id = 'author2', class = 'author'> 조정래 </p>
        
        <p id = 'book3_title', class = 'book_title'> 감옥으로부터의 사색 </p>
        <p id = 'author3', class = 'author'> 신영복 </p>
        
    </body>
</html>
'''
```
```
soup = BeautifulSoup(html_doc, 'lxml')
```
```
print(soup.prettify())
```
```
soup.find('title')
```
```
soup.title # soup.find('title')과 동일
```
```
soup.find('body')
```
```
soup.body  # soup.find('body')와 동일
```
```
soup.find('h1')
```
```
soup.h1
```
```
책제목/작가 형식으로 출력해보기

(예)
토지/박경리
태백산백/조정래
감옥으로부터의 사색/신영복
```
```
book_titles = soup.find_all('p', {'class':'book_title'})
```
```
book_titles
```
```
book_authors = soup.find_all('p', {'class':'author'})
```
```
book_authors
```
```
for book_title, book_author in zip(book_titles, book_authors):
    print(book_title.text, '/', book_author.text)
```
**select 사용하기**
```
soup.find_all('p')
```
```
soup.select('p')   # soup.find_all('p')와 동일한 결과
```
```
soup.find('p')
```
```
soup.select_one('p')  # soup.find('p')와 동일한 결과
```
```
soup.select('p')
```
```
soup.select('body p')  # body 태그의 자손인 p 태그  /  어디에 있는 p인지를 모를 때 사용
```
```
soup.select('body > p')   # body 태그의 자식인 p 태그       find, find_all과는 다르게 select는 태그의 자식을 활용할 수 있다.
```
```
soup.select('p.book_title')  # 태그의 속성이 class일 경우에는 .으로 찾을 수 있음
                             # soup.find_all('p', {'class':'book_title'})과 동일
```
```
soup.select('p.author')   # 태그의 속성이 class일 경우에는 .으로 찾을 수 있음
                          # soup.find_all('p', {'class':'book_author'})과 동일
```
```
soup.select('p#book1_title')   # 태그의 속성이 id일 경우에는 #으로 찾을 수 있음
                               # soup.find_all('p', {'id':'book1_title'})와 동일한 결과
```
```
soup.select('p#author1')   # 태그의 속성이 id일 경우에는 #으로 찾을 수 있음
                            # soup.find_all('p', {'id':'author1'})와 동일한 결과
```
### Workshop
```
html_doc = """
<!doctype html>
<html>
 <head>
   <meta charset="utf-8">
   <title>사이트 모음</title>
 </head>
 <body>
   <p id="title"><b>자주 가는 사이트 모음</b></p>
   <p id="contents">이곳은 자주 가는 사이트를 모아둔 곳입니다.</p>
   <a href="http://www.naver.com" class="portal" id="naver">네이버</a> <br>
   <a href="https://www.google.com" class="search" id="google">구글</a> <br>
   <a href="http://www.daum.net" class="portal" id="daum">다음</a> <br>
   <a href="http://www.nl.go.kr" class="government" id="nl">국립중앙도서관</a>
 </body>
</html>
"""
```
```
# a 태그들로 이루어진 요소들을 출력
soup = BeautifulSoup(html_doc, 'lxml')
```
```
soup.find_all('a')
```
```
soup.select('a')
```
```
# class가 portal인 요소들을 출력 - 2가지 방법
soup1 = BeautifulSoup(html_doc, 'lxml')
```
```
soup1.select('body a')
```
```
soup1.select('a.portal')
```
```
portal = soup1.find_all('a', {'class':'portal'})
portal
```
```
# id가 naver인 요소들을 출력
soup2 = BeautifulSoup(html_doc, 'lxml')
```
```
soup2.select('a#naver')
```
```
id = soup2.find_all('a', {'id':'naver'})
id
```
```
# a 태그의 href 속성이 있는 모든 태그들을 출력
soup.select('a[href]')
```
**속성의 값 보기**
```
soup.a.attrs # 해당태그(a 태그)의 속성 전체를 확인할 수 있음
```
```
soup.p.attrs
```
```
soup.a['href']     # 속성의 값을 확인
```
```
soup.a['class']
```
```
soup.a['id']
```
