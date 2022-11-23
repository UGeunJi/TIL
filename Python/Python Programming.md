# 많이 사용하는 단축기

- shift + Enter : 실행
- Alt + Enter : 실행 (후에 셀이 추가)
- a : 위로 셀이 추가
- b : 아래로 셀이 추가
- m : 마크다운 모드로 변경
- y : 코드 모드로 변경
- x : 셀 삭제
- dd : 셀 삭제
- ctrl + shift + '-' : 커서가 위치한 곳에서 셀이 나뉨
- shift + 'M' : 선택된 셀들이 병합
- Esc : 에디터 모드 셀포커스 모드 전환

# Python Code 실행하기
## 1
### 1.1
#### 1.1.1
##### 1.1.1.1

**프로그램 실행방법** 
```py
print("Hello world~!")
print("Hello world~!")
```
```py
print("Hello world~!")
print("Hello world~!")
```
%run "hello.py" # run이란 매직명령어로 파이썬 스크립트 실행

# cmd 창 (or anaconda prompt 창)에서
# python hello.py
```py
%pwd
```
# Markdown language


[Markdown Cheetseet](https://www.markdownguide.org/cheat-sheet/)

**bold text**
```py
![Python Image]("Python Image.jpg")
```
```py
from IPython.display import Image
Image("Python Image.jpg", width = 100)
```
# 탭 완성기능
```py
an_apple = "apple"
```
```py
print(an_apple), type(an_apple)
```
```py
an_example = 42
```
```py
print(an_example), type(an_example)
```
```py
an_float = 14.42
```
```py
print(an_float), type(an_float)
```
an_<tab 키>

# python list 자료형
```py
score = [90, 100, 75, 100]

score
```
```py
score.pop(-1)

score
```
```py
score.append(80)

score
```
```py
score.pop(1)

score
```
```py
set(score)
```
```py
list(score)
```
```py
score.append(100)

score
```
```py
score.append(100)

score
```
```py
set(score)
```
```py
list(score)
```
score.
set.            + <tab 키> # 리스트 객체에서 제공한느 여러 메서드들이 보여짐
dict.

# 도움말
```py
score?
```
```py
?score
```
```py
print? # 파이썬에서 제공하는 함수
```
# 내가 만든 함수

# 1. 정의
```py
def addition(a, b):
    """
    Add two numbers together
    return a + b
    """
    c = a + b
    return c
```
# 2. 호출
```py
addition(3, 4)
```
```py
addition(100, 20)
```
```py
addition?
```
```py
addition??
```
```py
def calculator(a, b, y):
    if y == '+':
        c = a + b
    elif y == '-':
        c = a - b
    elif y == '*':
        c = a * b
    elif y == '/':
        c = a / b
    return c
```
```py
calculator(3, 2, '*')
```
```py
%run "Hello.py" # 파이썬 스크립트를 실행할 때 사용
```
```py
%pwd # 현재 작업중인 디렉토리 명을 알고 싶을 때 사용
```
# %load "Hello.py"
```py
print("hello world")
```
```py
a = 2
b = 3
```
```py
%time c = a + b    # time 뒤에 나오는 statement를 수행하는데 걸린 시간
```
```py
%timeit c = a + b    # timeif 뒤에 나오는 statement를 여러번 수행해서 평균 시간을 출력
```
# 기본 문법

# 파이썬의 타입(자료형)은 미리 지정이 되어있지 않음
# 입력되는 데이터의 종륭에 따라서 결정

## example
# int a, float b, str ana
```py
a = 3
b = 4
```
```py
type(a)
```
```py
type(b)
```
```py
a = 3; b = 4    # 한줄에 여러 문장을 작성할 때는 세미콜론을 사용
```
# 들여쓰기
```py
if a == 3:
    print("a는 3입니다")
```
```py
print("배고픕니다")
print("점심은 뭐 먹을까요")
print("나중에 메뉴 랜덤으로 정해주는 거 하나 만들어야겠습니다")
```
# 숫자 계산하기
```py
1 + 1
```
```py
2 - 1
```
```py
2 * 3
```
```py
4/2
```
```py
5/2
```
```py
5 // 2
```
```py
5 % 2
```
```py
2 ** 10
```
```py
import math
```
```py
print(math.sqrt(2))
```
```py
math.sqrt(3)
```
```py
a = 2
print(type(a))
```
```py
1.5/2.6
```
```py
b = 2.3
print(type(b))
```
# 자료형 변환 (type casting)
# a: int -------> float    (실수형으로 변환)
```py
c = float(a)


c
```
```py
print(type(c))
```
# b: float ----> int  (정수형으로 변환)
```py
d = int(b)
type(b)
```
```py
s = '10'
type(s)
```
```py
s2 = int(s)
```
```py
s2
```
```py
a = 3    # 오른쪽에 있는 값을 왼쪽의 변수에 할당
```
```py
a == 3    # 왼쪽 값과 오른쪽 값이 같은지 비교
```
```py
a == 4
```
```py
# 영문자 숫자를 함께 사용
a1 = 4

A1 = 10
```
```py
# 대소문자 구분
a1
```
```py
A1
```
```py
# 숫자로 시작하는 변수
10a = 10        # Error

_a = 10
```
```py
# 특수문자(+, -, / , $, %, &)는 변수에 사용할 수 없음
$a = 10
```
```py
if a == 3:
    print("a는 3입니다")
```
```py
divmod(3, 2)
```
```py
divmod(100, 3)
```
```py
x, y, z = 10, 20, 30
```
```py
x * y
```
```py
x ** z
```
# 파이썬에 이미 예약된 키워드는 사용할 수 없음(if, for, while, and, or, str)

# if = 2         (X)
# str = "hello"  (X)
```py
a, b = 2, 3
```
# a : 2 -> 3
# b : 3 -> 2
```py    
a, b = b, a    # a와 b를 맞바꿈
```
```py
a
```
```py
b
```
```py
temp = a # a를 backup
a = b
b = temp
```
```py
a, b
```
```py
# 할당할 값의 개수 맞추기
a, b, c = 10, 20
```
```py
del a
```
```py
a
```
```py
x = None
```
```py
x
```
```py
type(x)
```
```py
a = 10
a = a + 10
a += 10     # a = a + 10

a
```
```py
a = 20
a -= 10
a
```
```py
a = 20
a *= 10
a
```
```py
a = 20
a /= 10
a
```
```py
print(int(0.2467 * 12 + 4.159))
```
```py
prob2 = 1 - 4 * 1 * (-2)  # 판별식
prob2
```
```py
import math         # 모듈 사용
```
```py
prob2_1 = (((-1) + math.sqrt(1 - 4 * 1 * (-2))) / 2 * 1)
prob2_1
```
```py
prob2_2 = (((-1) - math.sqrt(1 - 4 * 1 * (-2))) / 2 * 1)
prob2_2
```
```py
a = 1; b = 1; c = -2 
```
```py
x1 = (-b + (b ** 2 - 4 * a * c) ** 0.5) / 2 * a          # math 모듈 사용 X
x2 = (-b - (b ** 2 - 4 * a * c) ** 0.5) / 2 * a
```
```py
x1, x2
```
# 입력값을 변수에 저장하기
```py
input()
```
```py
input()
```
```py
input()
```
```py
a = input()
```
```py
a
```
```py
type(a)
```
```py
a = input("숫자를 입력하세요: ")
b = input("숫자를 입력하세요: ")
```
```py
a, b
```
```py
a + b
```
```py
int(a) + int(b)
```
```py
two_numbers = input("두 숫자를 입력하세요: ")
```
```py
two_numbers.split
```
# 문자열에서 제공하는 split() 함수는 whiltespace(스페이스 등)을 기준으로 나눈 결과를 리스트로 반환
```py
two_numbers_list = two_numbers.split()
```
```py
"abc,def".split(',')
```
```py
two_numbers.split?
```
```py
two_numbers_list
```
```py
a,b = map(int, two_numbers_list)

a, b
```
# map(적용하고자 하는 함수, list(sequence객체))
```py
a, b = map(int, ['10', '20'])     # map() 함수: list 안에 있는 원소 모두를 일괄 적용할 때 사용
a, b
```
```py
type(a), type(b)
```
```py
numbers = input("숫자를 입력하세요: ")
```
```py
numbers_list = numbers.split()
```
```py
numbers_list
```
```py
numbers_list = list(map(int, numbers_list))
numbers_list
```
# (1) 두개 이상 입력받기
```py
n = input("숫자를 입력하세요: ")
```
# (2) 구분자를 통해 나누기
```py
l = n.split()
l
```
# (3) 형변환
```py
l1, l2 = map(int, l)
l1, l2
```
### Workshop

**정수 세개를 입력 받고 합계 출력하기**
```py
a = input("세개의 정수를 입력하세요: ")

p = a.split()            # split 사용 후, map() 함수로 묶은 다음 정수화
p 
a1, a2, a3 = map(int, p)
a1, a2, a3
```
```py
d = a1 + a2 + a3
d
```
```py
x, y, z = map(int, input("세 개의 정수를 입력하세요: ").split())       # 위의 과정을 한 번에 축약한 방식
print(x + y + z)
```
**평균 점수 구하기**
```py
Korean = int(input())
English = int(input())            # int 한 번에 처리한 방식
Science = int(input())
```
```py
(Korean + English + Science) // 3
```
```py
(Korean + English + Science) // 3
```
```py
Korean = input()              # int 따로 추가해서 마무리한 방식
English = input()
Science = input()              
```
```py
(int(Korean) + int(English) + int(Science)) // 3
```
```py
k, e, m, s = map(int, input().split())
A = (k + e + m + s) // 4
A
```
```py
def my_student_info(name, school_ID, phoneNumber):
    print("--------------------------------")
    print("학생이름: ", name)
    print("학급번호: ", school_ID)
    print("전화번호: ", phoneNumber)
```
```py
my_student_info("우근", "01", "010-4563-8147")
my_student_info("대영", "02", "010-1234-8147")
```
# 전역 변수 변경
```py
a = 5
```
```py
def func1():
    a = 1 # 지역 변수. func1()에서만 사용
    print("[func1] 지역 변수 a = ", a)

def func2():
    a = 2 # 지역 변수. func2()에서만 사용
    print("[func2] 지역 변수 a = ", a)
    
def func3():
    print("[func3] 지역 변수 a = ", a)
    
def func4():
    global a    # 함수 내에서 전역 변수를 변경하기 위해 선언
    a = 4       # 전역 변수의 값 변경
    print("[func4] 지역 변수 a = ", a)
```
```py
func1()   # 함수 func1() 호출
func2()   # 함수 func1() 호출
print("전역 변수 a = ", a)  # 전역 변수 출력
```
```py
func3()   # 함수 func3() 호출 - 기존 전역 변수 출력
func4()   # 함수 func4() 호출 - 전역 변수 변경
func3()   # 함수 func3() 호출 - 변경된 전역 변수 출력
```
```py
(lambda x : x ** 2) (3)
```
```py
mySquare = lambda x : x ** 2
mySquare(12)
```
```py
mySimpleFunc = lambda x, y, z : 2 * x + 3 * y + z
mySimpleFunc(1, 2, 3)
```
# 출력 방법 알아보기

- print(값1, 값2, 값3, ...)
- print(변수1, 변수2, 변수3, ...)
```py
print(1, 2, 3, 4)
```
```py
print(k, e, m, s)
```
- print(값1, 값2, 값3, ..., sep = '문자' 또는 '문자열')
- print(변수1, 변수2, 변수3, ..., sep = '문자' 또는 '문자열')
```py
print(1, 2, 3, 4, sep = ', ')
```
```py
print(k, e, m, s, sep = ', ')
```
```py
print(2, 3 , sep = ' X ')
```
```py
print(1, 2, 3, sep = '\n')     # 개행문자(\n)라는 제어문자를 지정하면 줄바꿈이 되어서 출력
```
```py
print(1, 2, 3, sep = '\t')     # 개행문자(\t)라는 제어문자를 지정하면 탭이 되어서 출력
```

- print(값1, 값2, 값3, ..., end = '문자' 또는 '문자열')
- print(변수1, 변수2, 변수3, ..., end = '문자' 또는 '문자열')
```py
print(1, 2, 3, 4, '\t', end = '이히')
```
```py
print(1, 2, 3, 4)         # 자동으로 \n 처리가 되도록 되어있다.
print(5, 6, 7, 8)
```
```py
print(1, 2, 3, 4, end = ' ')         # 스페이스를 마지막에 붙여줌으로써 바꿔줌
print(5, 6, 7, 8)
```
### Workshop

**날짜와 시간 출력하기**

- 2022/10/17/16:26:06
```py
print(2022, '/', 10, '/', 17, '/', 16, ':', 26, ':', '06')
```
```py
print('2022/10/17/16:26:06')
```
```py
year = 2022
month = 10
day = 17
hour = 16
minute = 26
second = 6
```
# 날짜
```py
print(year, month, day, sep = '/', end = ' ')
print(hour, minute, '0%d'% second, sep = ':')
```
```py
print('%02d'% second)      # 전체 두자리수로 표현하고 남는 자리는 0으로 표현
```
# bool 자료형과 비교연산자
```py
result = (a == 4)
```
```py
result, type(result)
```
```py
10 != 9
```
```py
"Python" == "python"
```
```py
10 > 20
```
```py
1 == 1.0
```

# Day 1 review

- split 사용하여 입력값 덧셈
- sep = '', end = '' (list value 설정)
- bool 연산자와 비교 연산자

---

# Day 2

- and
- or
- not
```py
True and True
```
```py
True and False
```
```py
true and false      # 첫글자 대문자로 하지 않으면 bool로 판단하지 않음
```
```py
False or True
```
```py
Not True        # 논리 연산자는 모두 소문자로
```
```py
not True
```
# 비교 연산자와 논리 연산자를 함께 사용
```py
10 == 10
```
```py
10 != 5
```
```py
10 == 10 and 10 != 5
```
```py
10 == 10 and 10 == 5
```
# 자료형 변환
```py
print(int(1.5))
print(float(1))
print(str(1))
```
```py
bool(1)
```
```py
bool(0)
```
### Workshop
```py
k, e, m, s = map(int, input("각 과목의 점수를 입력하세요: ").split())
k >= 50 and e >= 50 and m >= 50 and s >= 50
```
```py
Korean = 92
English = 95
Mathmatics = 30
Science = 90
```
```py
print(Korean >= 50 and English >= 50 and Mathmatics >= 50 and Science >= 50)
```
```py
not(Korean < 50 or English < 50 or Mathmatics < 50 or Science < 50)
```
- all(), any()
```py
all(______)  # 모두가 True이어야 한다.
```
```py
any(______)  # 하나라도 False면 False로 출력한다.
```
```py
is_pass = [Korean >= 50, English >= 50, Mathmatics >= 50, Science >= 50]

all(is_pass)
```
```py
is_fail = [Korean < 50, English < 50, Mathmatics < 50, Science < 50]

is_fail
```
```py
not(any(is_fail))
```
### 3개의 과일에 벌레 5마리 이상 발견되면 폐기처리
```py
a, b, c = map(int, input("과일의 벌레수를 입력해주세요: ").split())
if(a >= 5):
    print("a과일 폐기처리")
else:
    print("a과일 적합")
if(b >= 5):
    print("b과일 폐기처리")
else:
    print("b과일 적합")
if(c >= 5):
    print("c과일 폐기처리")
else:
    print("c과일 적합")
```
### 일주일 간 평균기온 구하기
```py
su, mo, tu, we, th, fi, sa = map(int, input("각 요일의 기온을 입력해주세요. 단위는 drgree celsius: ").split())
average_temperature = (su + mo + tu + we + th + fi + sa) / 7
print(int(average_temperature))
```
# 문자열 사용하기
```py
s1 = 'hello'
s2 = "hello"
s3 = '''hello'''
s4 = """hello"""
print(type(s1))
print(type(s2))
print(type(s3))
print(type(s4))
```
```py
print(s1, s2, s3, s4)
```

hello "python"을 출력
```py
s1 = 'hello "python"'
type(s1)
```
```py
print(s1)
```
```py
hello 'python'을 출력
```
```py
s2 = "hello 'python'"
```
```py
print(s2)
```
```py
s3 = """hello "python" """      # 띄어쓰기 한 칸 필요하다
```
```py
s4 = '''hello 'python' '''      # 띄어쓰기 한 칸 필요하다
```
```py
print(s3)
```
```py
print(s4)
```
```
here is
python world
it is
real!!!
```
```py
s5 = '''here is
python world
it is
real!!!'''
print(s5)                # ''' '''은 만능이라고 생각할 수 있다.
```
```py
s6 = """here is
python world
it is
real!!!"""
print(s6)                # """ """도 만능이라고 생각할 수 있다.
```
```py
s6.count('i')      # 입력값이 몇 개인지 세어주는 메서드
```
```py
s6.count('\n')
```
```py
s6.count('!')
```
```py
hello 'python'
```
```py
s7 = 'hello \'python\''          # \은 escaping이라고 하며 따로 구분해주는 역할을 한다.
s7
```
### Workshop
```py
s = ''''python' is a "programming language"
that lets you work quickly
and
integrate systems more effectively.'''
```
```py
print(s)
```
# list and tuple

- list = [value, value, value, ...]  
#### 대괄호로 묶어줌

programming_scores = [학생 1의 점수, 학생 2의 점수, ...]
철수의 점수 = [파이썬 점수, 자바 점수, C 점수, C++ 점수, veilog 점수, ...]
```py
scores = [90, 95, 100, 100, 90, 95]

scores
```
```py
type(scores)
```
```py
person = [name, age, height, weight]

person1 = ["UGeun", 25, 178, 70]
person1
```
**빈 리스트 만들기**
- 리스트 = []
- 리스트 = list()
```py
empty_list1 = []
empty_list1
```
```py
empty_list2 = list()
empty_list2
```
- range(횟수)
```py
range(10)
```
```py
a = list(range(10))
a
```
- range(시작, 끝)
```py
b = list(range(2, 8))
b
```
```py
print(a)
print(b)
```
- range(시작, 끝, 증가폭)
```py
c = list(range(2, 8, 2))
c
```
```py
d = list(range(8, 2, -1))
d
```
- list = (value, value, value, ...)
#### 소괄호로 묶어줌

- 튜플 = (값, 값, 값, ...)
- 튜플 = 값, 값, 값, ...
```py
a = (1, 2, 3, 4)
a
```
```py
type(a)
```
```py
b = 1, 2, 3, 4

b
```
```py
type(b)
```
```py
c = (1,)     # 원소가 하나인 tuple을 생성하고 싶다면 ,(comma)를 찍어줘야 한다.
```
- tuple1 = tuple(range(times))
```py
a = tuple(range(10))
a
```
- tuple1 = tuple(range(start, end))
- tuple1 = tuple(range(start, end, interval))
```py
b = tuple(range(1, 15))
b
```
```py
c = tuple(range(1, 15, 3))

c
```
```py
int(5.3)
```
```py
float(5)
```
# list to tuple and tuple to list
```py
list_a = list(a)
```
```py
list_a
```
```py
tuple_a = tuple(a)
```
```py
tuple_a
```
### Workshop
```py
list_1 = list(range(5, -10, -2))
list_1
```
```py
a = int(input())
tuple_1 = tuple(range(-10, 10, a))
tuple_1
```
```py
step = int(input())
print(tuple(range(-10, 10, step)))
```
# 시퀀스 자료형 활용하기

- 시퀀스 자료형: list, tuple range, str

- value in sequence object
```py
a = [1, 2, 3, 4, 5]
```
```py
1 in a
```
```py
10 in a
```
```py
10 not in a
```
```py
b = (1, 2, 3, 4, 5)
10 in b
```
```py
c = "Hello"
'H' in c
```
```py
 'h' in c         # 대소문자 구분
```
```py
range(10)
```
```py
1 in range(10)
```
```py
10 in range(10)
```
- sequence object1 + sequence object2
```py
a = [1, 2, 3, 4, 5]
b = [6, 7, 8, 9, 10]

a + b                    # 그럼 병합 메서드는 왜 존재하는가?
```
```py
c = (1, 2, 3, 4, 5)
d = (6, 7, 8, 9, 10)

c + d
```
```py
range(5) + range(5)         # 범위에 대한 정보만 가지고 있지, 실체는 없는 상태기 때문에 더할 수 없다.
```
```py
list(range(5)) + list(range(5))
```
```py
s1 = "Hello "
s2 = "world!"

s1 + s2
```
- sequence object * integer
- integer * sequence object
```py
[1, 2, 3] * 3
```
```py
3 * [1, 2, 3]
```
```py
2 * range(2)      # 실체 X
```
```py
2 * list(range(2))
```
```py
'Hello ' * 3
```
```py
3 * (1, 2, 3)
```
- len(sequence object)
```py
a = [1, 2, 3]      # length 길이 알아볼 때 사용

len(a)
```
```py
b = (1, 2, 3, 4, 5)

len(b)
```
```py
len(range(10))
```
```py
len("Hello")
```
```py
 c = [2, 4, 5, 1]      # 앞에 띄어도 실행가능

len(c)
```
```py
scores = [90, 80, 100, 90]    # 2번째에 있는 영어 점수만 알고 싶을 때

scores[1]           # index start from 0, so get second element from 'scores' list
```
```py
# scores = [100, 90, ......................., 80] 일 때 마지막 거를 가져오고 싶다면
# scores = [-1]을 사용
```
```py
scores[3]     # 마지막 원소
```
```py
scores[-1]    # 음수 인덱스 (마지막 원소를 가져올 때 편리)
```
```py
len(scores) -1
```
```py
scores[len(scores) - 2]
```
```py
b = (1, 2, 3)
```
```py
b[4]
```
```py
range(10)[4]
```
```py
list(range(10))
```
```py
list(range(10, 100, 10))
```
```py
range(10, 100, 10)[2]
```
```py
range(10, 100, 10)[len(range(10, 100, 10)) - 1]
```
```py
range(10, 100, 10)[-1]
```
```py
s = "Hello"
```
```py
s[0]
```
```py
s[4]
```
```py
s[-1]
```
```py
s[3]
```
```py
s[-2]
```
- sequence object[index] = value
- 위의 문법은 list 객체에서만 유효. tuple, range, str 에서는 요소 값을 변경할 수 없다.
```py
scores = [90, 100, 100, 70]

scores[0] = 95

scores
```
```py
shape = (1200, 900)
shape[0] = 1000            # tuple은 value 변경이 불가능하다.
```
```py
range(10)[0] = 100
```
```py
s = "Hello World!"
s[0] = 'h'
```
- del 시퀀스객체[index]
- 위의 문법은 list 객체에서만 유효. tuple, range, str 에서는 요소 값을 변경할 수 없다.
```py
a = [1, 2, 3, 4]

del a[2]

a
```
```py
b = (1, 2, 3, 4)
del b[2]
```
```py
s = "Hello"
del s[1]
```
- sequence object[start_index:end_index]
```py
a = [10, 20, 30, 40, 50]
# a[start:end]
a[0:3]        # 3번째는 포함 안됨 (0 ~ 2번째까지 가져오는 문법)
```
```py
a[:3]  # 0번째는 생략 가능
```
```py
a[2:5]
```
```py
a[2:]  # 마지막 번째 생략 가능
```
```py
a[:]     # 시작인덱스와 끝인덱스를 모두 생략하면 처음부터 끝까지 가져옴
```
```py
a[3:-1]
```
- sequence object[start_index:end_index:interval]
```py
a = list(range(0, 100, 10))
a
```
```py
a[0:5]
```
```py
a[0:5:2]
```
```py
a[-1::-1]
```
```py
a[0::1]
```

### Workshop
```py
year = [2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018]
population = [10249679, 10195318, 10143645, 10103233, 10022181, 9930616, 9857426, 9838892]
```
```py
year[5:]
```
```py
population[5:]
```
```py
print(year[-3:])
```
```py
print(population[-3:])
```
```
# year와 population을 연결지어서 한 번에 출력할 수 있음
# zip(sequence object1, sequence object2)
```
```py
zip(year, population)
```
```py
map(int, ["10", "20", "30"])      # 형태만 존재
```
```py
list(zip(year, population))       # 실체까지 출력
```
```py
list(zip(year[-3:], population[-3:]))
```
```py
dict(zip(year[-3:], population[-3:]))
```
---
```py
n = -32, 75, 97, -10, 9, 32, 4, -15, 0, 76, 14, 2
```
```py
tuple(n)

n
```
```py
n[-1::-2]
```
```py
n[1:len(n):2]
```
```py
n[1::2]
```
---
```py
a = list(input().split())
del a[-1:-6:-1]
tuple(a)
```
```py
x = input()
```
```py
s = x.split()
s
```
```py
del s[-5:]

s
```
```py
x = input().split()
del x[-5:]
print(tuple(x))
```
---

### Workshop
```py
pin = '881204-1068234'
```
```py
pin.split('-')
```
```py
x = list(pin)

x
```
```py
if(x[7] == '1'):
    print("male")
else:
    print("female")
```
```py
pin_list = pin.split('-') # 다른 풀이
```
```py
second = pin_list[1]
second
```
```py
second[0]
```
```py
if second[0] == '1':
    print('male')
else:
    print('female')
```
# 최종 코드

if pin.split('-')[1][0] == '1':
    print('male')
else:
    print('female')

---

print("phone number 출력 문자열")
y = input()
z = list(y)
z[:-4] = '*******'
print(list(z))
print(str(z))
print(z)

def solution(angle):
    answer = (angle // 90) * 2 + (angle % 90 > 0) * 1
    return answer

solution(130)

solution(40)

solution(90)

solution(180)

phone_number = input()

phone_number

phone_number[:-4]

len(phone_number[:-4])

# s1 = 시퀀스 객체 * 정수
s1 = '*'* len(phone_number[:-4])

s2 = phone_number[-4:]

ss = s1 + s2

ss

# 최종 코드

phone_number = input()
s1 = '*'* len(phone_number[:-4])
s2 = phone_number[-4:]
s1 + s2

# dictionary

- dictionary = {key1:value1, key2:value2, key3:value3, ...}

year_pop = {2016:9981304, 2017:4072902, 2018:1204857}

type(year_pop)

# 딕셔너리에서는 어떤 값을 찾아가기 위한 유일한 수단이 '키가 됨
# (Note.) 리스트, 튜플, 문자열 등에서는 어떤 값을 찾아가기 위해 원소의 위치를 직접 계산을 했었음

# 2016년도의 population을 알고 싶다면
year_pop[2016]

# 딕셔너리에서는 어떤 값을 찾아가기 위한 유일한 수단 '키'이므로
# '키'는 중복이 되어서는 안됨

# 아래와 같이 키 값(2016)을 중복해서 사용해도 문법적으로 오류는 안나지만
# 실제로 중복된 키(2016)로 색인했을 때 올바른 값을 얻어낼 수 없음
# 중복된 값 중 뒤에 있는 값이 조회가 됨
year_pop = {2016:9981304, 2016:4072902, 2018:1204857}

year_pop[2016]

year_pop[2016]

# 딕셔너리는 순서가 있는 자료형이 아님 (list나 tuple과는 달리 순서가 없어도 상관없다.)
year_pop = {2016:9981304, 2017:4072902, 2018:1204857}
year_pop

# dictionary's key: string, float, bool, tuple, and so on
# dictionary's value: all form including list, dictionary 

# 딕셔너리의 키 값으로는 읽기 가능한 자료형이 와야 함(리스트, 딕셔너리 올 수 없음)

lux = {'health': 490, 'melee': 500, 'armor': 18.72}

lux

lux = {[1, 2, 3]: 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 리스트가 들어간 경우

lux = {{'k': 'v'}: 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 딕셔너리가 들어간 경우

lux = {(1, 2): 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 튜플가 들어간 경우 (OK)

**빈 딕셔너리 만들기**
- 딕셔너리 = {}
- 딕셔너리 = dict()

x = {}
type(x)

x = dict()
type(x)

**dict()로 딕셔너리 만들기**
- dictionary = dict(zip([key1, key2], [value1, value2]))
- dictionary = dic([(key1, value1), (key2, value2)])

zip(['health', 'melee', 'armor'], [490, 500, 18.72])

list(zip(['health', 'melee', 'armor'], [490, 500, 18.72]))

dict(zip(['health', 'melee', 'armor'], [490, 500, 18.72]))

dict([('health', 490), ('melee', 500), ('armor', 18.72)])

**딕셔너리의 키로 값 조회하기**
- dictionary[key]

year_pop[2016]

lux['melee']

**딕셔너리의 값 변경하기**
- dictionary[key] = value

lux

lux['melee'] = 1000
lux

lux['attack_speed'] = 500

lux

lux['power']     # 없는 키로 조회하면 오류

**딕셔너리에 키가 있는지 확인하기**
- 키 in dictionary

a = [1, 2, 3]
1 in a

'melee' in lux

'power' in lux

len(lux)

# Workshop

age = int(input())
balance = 9000
if age >= 7 and age <= 12:
    balance -= 650
elif age >= 13 and age <= 18:
    balance -= 1050
elif age >= 19:
    balance -= 1250
print(balance)

age = int(input())
balance = 9000

if 7 <= age <= 12:  # 어린이
    balance -= 650
elif 13 <= age <= 18:  # 청소년
    balance -= 1050
elif age >= 19:    # 성인
    balance -= 1250
else:
    print("Error")
print(balance)

---

**게임 캐릭터 능력 저장**
- 표준 입력으로 문자열 여러 개와 숫자(실수) 여러 개가 두 줄로 입력됩니다. 입력된 첫 번째 줄은 키, 두 번째 줄은 값으로 하여 딕셔너리를 생성한 뒤 딕셔너리를 출력하는 프로그램을 만드세요. input().split()의 결과를 변수 한개에 저장하면 리스트로 저장됩니다.
```
(입력예)
health health_regen mana mana_regen
575.6 1.7 338.8 1.63
(결과)
{'health':575.6, 'health_regen':1.7, 'mana':338.8, 'mana_regen':1.63}
```

k = input().split()
d = input().split()

dict(zip(k, d))

key_list = input().split()
dict_list = input().split()

dict(zip(key_list, dict_list))


