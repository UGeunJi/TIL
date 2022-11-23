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
```py
if pin.split('-')[1][0] == '1':
    print('male')
else:
    print('female')
```
---
```py
print("phone number 출력 문자열")
y = input()
z = list(y)
z[:-4] = '*******'
print(list(z))
print(str(z))
print(z)
```
```py
def solution(angle):
    answer = (angle // 90) * 2 + (angle % 90 > 0) * 1
    return answer

solution(130)
```
```py
solution(40)
```
```py
solution(90)
```
```py
solution(180)
```
```py
phone_number = input()
```
```py
phone_number
```
```py
phone_number[:-4]
```
```py
len(phone_number[:-4])
```
```py
# s1 = 시퀀스 객체 * 정수
s1 = '*'* len(phone_number[:-4])
```
```py
s2 = phone_number[-4:]
```
```py
ss = s1 + s2
```
```py
ss
```
# 최종 코드
```py
phone_number = input()
s1 = '*'* len(phone_number[:-4])
s2 = phone_number[-4:]
s1 + s2
```
# dictionary

- dictionary = {key1:value1, key2:value2, key3:value3, ...}
```py
year_pop = {2016:9981304, 2017:4072902, 2018:1204857}

type(year_pop)
```
# 딕셔너리에서는 어떤 값을 찾아가기 위한 유일한 수단이 '키가 됨
# (Note.) 리스트, 튜플, 문자열 등에서는 어떤 값을 찾아가기 위해 원소의 위치를 직접 계산을 했었음

# 2016년도의 population을 알고 싶다면
```py
year_pop[2016]
```
# 딕셔너리에서는 어떤 값을 찾아가기 위한 유일한 수단 '키'이므로
# '키'는 중복이 되어서는 안됨

# 아래와 같이 키 값(2016)을 중복해서 사용해도 문법적으로 오류는 안나지만
# 실제로 중복된 키(2016)로 색인했을 때 올바른 값을 얻어낼 수 없음
# 중복된 값 중 뒤에 있는 값이 조회가 됨
```py
year_pop = {2016:9981304, 2016:4072902, 2018:1204857}
```
```py
year_pop[2016]
```
```py
year_pop[2016]
```
# 딕셔너리는 순서가 있는 자료형이 아님 (list나 tuple과는 달리 순서가 없어도 상관없다.)
```py
year_pop = {2016:9981304, 2017:4072902, 2018:1204857}
year_pop
```
# dictionary's key: string, float, bool, tuple, and so on
# dictionary's value: all form including list, dictionary 

# 딕셔너리의 키 값으로는 읽기 가능한 자료형이 와야 함(리스트, 딕셔너리 올 수 없음)
```py
lux = {'health': 490, 'melee': 500, 'armor': 18.72}

lux
```
```py
lux = {[1, 2, 3]: 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 리스트가 들어간 경우
```
```py
lux = {{'k': 'v'}: 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 딕셔너리가 들어간 경우
```
```py
lux = {(1, 2): 490, 'melee': 500, 'armor': 18.72}    # 딕셔너리의 키에 튜플가 들어간 경우 (OK)
```
**빈 딕셔너리 만들기**
- 딕셔너리 = {}
- 딕셔너리 = dict()
```py
x = {}
type(x)
```
```py
x = dict()
type(x)
```
**dict()로 딕셔너리 만들기**
- dictionary = dict(zip([key1, key2], [value1, value2]))
- dictionary = dic([(key1, value1), (key2, value2)])
```py
zip(['health', 'melee', 'armor'], [490, 500, 18.72])
```
```py
list(zip(['health', 'melee', 'armor'], [490, 500, 18.72]))
```
```py
dict(zip(['health', 'melee', 'armor'], [490, 500, 18.72]))
```
```py
dict([('health', 490), ('melee', 500), ('armor', 18.72)])
```
**딕셔너리의 키로 값 조회하기**
- dictionary[key]
```py
year_pop[2016]
```
```py
lux['melee']
```
**딕셔너리의 값 변경하기**
- dictionary[key] = value
```py
lux
```
```py
lux['melee'] = 1000
lux
```
```py
lux['attack_speed'] = 500

lux
```
```py
lux['power']     # 없는 키로 조회하면 오류
```
**딕셔너리에 키가 있는지 확인하기**
- 키 in dictionary
```py
a = [1, 2, 3]
1 in a
```
```py
'melee' in lux
```
```py
'power' in lux
```
```py
len(lux)
```
### Workshop
```py
age = int(input())
balance = 9000
if age >= 7 and age <= 12:
    balance -= 650
elif age >= 13 and age <= 18:
    balance -= 1050
elif age >= 19:
    balance -= 1250
print(balance)
```
```py
age = int(input())
balance = 9000
```
```py
if 7 <= age <= 12:  # 어린이
    balance -= 650
elif 13 <= age <= 18:  # 청소년
    balance -= 1050
elif age >= 19:    # 성인
    balance -= 1250
else:
    print("Error")
print(balance)
```
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
```py
k = input().split()
d = input().split()

dict(zip(k, d))

key_list = input().split()
dict_list = input().split()

dict(zip(key_list, dict_list))
```
# Day 2 review

- sequence object
- index
- sequence object[index]
- range, del, ...
- sequence object[start_index:end_index:interval] (slice), (omit O)
- dictionary = {key:value}      (sequence X, overlap X)

---

# for, range 사용
```
for 변수 in range(횟수):
    반복할 코드
```
```py
for i in range(10):
    print("Hello World!", i)
```
```
for 변수 in range(시작, 끝, 증가폭):
    반복할 코드
```
```py
for i in range(0, 10, 2):
    print("Hello world!", i)
```
```py
for i in range(10, 0, -1):
    print("Hello World!", i)
```
# enumerate는 시퀀스 객체의 값뿐만 아니라 인덱스까지도 반환해줌
```py
for i, v in enumerate(range(0, 10, 2)):
    print("Hello World!", i, v)     # enumearate를 사용하면 index가 따라붙는다. index는 변수1에, valte는 변수2에 저장
```
```
for 변수 in 시퀀스 객체:
    반복할 코드
```
```py
for i in "Hello":       # 문자
    print(i)
```
```py
for i in [1, 2, 3]:       # list
    print(i)
```
```py
for i in (1, 2, 3):     # tuple
    print(i)
```
- for i in enumearate(sequence object):
```py
for i, v in enumerate("Hello"):
    print(i, v)
```
```
for i in reversed(sequence object):
    반복할 코드
```
```py
for i in reversed((1, 2, 3)):
    print(i)
```
```py
for i in reversed("Python"):
    print(i)
```
### Workshop
```py
a = int(input())
for i in range(1, 10):
    print(a, '*', i, '=' , a * i)
```
```py
"Hello".format()
```
# option 1  (format 함수 사용)
```py
x = int(input())
for i in range(1, 10):
    print("{0} * {1} = {2}".format(x, i, x * i))     # format을 사용하여 C언어에서의 #d, #f, ...와 같은 것들을 파이썬으로 표현
```
```py
x = int(input())
for i in range(1, 10):
    print("{2} * {1} = {0}".format(x, i, x * i))         # 입력하는 숫자에 따라서 입력되는 순서가 달라짐
```
# option 2   (서식 지정자 %)
```py
x = int(input())
for i in range(1, 10):
    print("%d * %d = %d" % (x, i, x * i))     # C언어에서의 ,(comma) 대신 파이썬에서는 %를 입력해준다.
```
# option 3 (문자열 포매팅(formatting) f를 붙이는 방법)
```py
x = int(input())
for i in range(1, 10):
    print(f"{x} * {i} = {x * i}")
```
```py
i = 0                         # 초기식
while i < 10:                # while 조건식
    print("Hello World!", i)    # 반복할 코드
    i += 1                  # 변화식 (없으면 무한 실행)
```
# while 반복문 사용하기

```
초기식
while 조건식:
    반복할 코드
    변화식
```    
```py
i = 10
while i > 0:
    print("Hello World!")
    i -= 1
```
```py
import random

random.randint(1, 6)

i = 0
while i != 3:
    i = random.randint(1, 6)              
    print(i)
```
---
```py
balance = int(input())
while balance > 1340:
    balance -= 1350
    print(balance)
```
---
```py
for i in range(0, 80):
    if i % 10 == 3:
        print(i, end = " ")
```
```py
for i in range(74):
    if (i % 10) == 3:
        print(i, end = " ")
```
# break문 사용법
```py
i = 0
while True:
    print(i)
    i += 1
    if i == 10:
        break
```
# continue
```py
for i in range(74):
    if (i % 10) != 3:
        continue
    else:
        print(i, end = " ")
```
```py
i = 0
while True:
    if i > 73:
        break
    print(i)
    i += 1
```
```py
i = 0
while True:
    if i % 10 != 3:
        i += 1
        continue
        
    if i > 73:
        break
    print(i, end = " ")
    i += 1
```
---
```py
s = 'life is short, so python is easy.'
punct = ',.'
d = {}

s_list = list(s)
s_list
```
```py
for i in s_list:
    print('%s의 개수 : %d' % (i,s_list.count(i)))
    list(zip(list(i), s_list.count(i)))
```
```py
for i in s_list:
    print('%s의 개수 : %d' % (i,s_list.count(i)))
```
```py
for i in s_list:
    dict(list(zip(s_list, s_list.count(i))))
```
```py
s = 'life is short, so python is easy.'
punct = ',. '
d = {}
```
```py
for c in s:
    # print(c)
    if c in punct:
        continue
    if c not in d:
        d[c] = 0
    if c in d:
        d[c] += 1

d
```
# 중첩 루트 사용하기
```py
for j in range(3):
    for i in range(5):
        print('*', end = " ")
    print()
```
```
**계단식으로 별 출력하기 (1)**
*
**
***
****
*****
```
```py
for j in range(1, 6):
    for i in range(5):
        print(end = " ")
    print(j * '*')
```


```
**계단식으로 별 출력하기 (2)**
*****
****
***
**
*
```
```py
for j in range(5, 0, -1):
    for i in range(5):
        print(end = " ")
    print(j * '*')
```
```py
for i in range(5):      # i: 0 -> 1 -> 2 -> 3 -> 4
    # 1. 공백
    for j in range(i):       # j: 0 -> 1 -> 2 -> 3 -> 4
        print(" ", end = '')
        
    # 2. 별
    
    for k in range(5-i): # k: 5 -> 4 -> 3 -> 2 -> 1
        print("*", end = '')
    print()
```
```
**별로 산 만들기**
    *
   ***
  *****
 *******
*********
```
```py
for i in range(1, 6):      # i: 1 -> 2 -> 3 -> 4 -> 5
    # 1. 공백
    for j in range(5-i):   # j: 4 -> 3 -> 2 -> 1 -> 0
        print(" ", end = "")
        
    # 2. 별
    for k in range(2 * i - 1):   # k: 1 -> 3 -> 5 -> 7 -> 9
        print("*", end = "")
    print()
```
```py
for j in range(1, 10, 2):
    for i in range(5):
        print(end = " ")
    print(j * '*')
```
# FizzBuzz 문제
```py
for i in range(1, 101):
    if i % 15 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```
# list applying

- append: 요소 하나를 추가
- extend: 리스트를 연결하여 확장
- insert: 특정 인덱스에 요소 추가
```py
a = [10, 20, 30]

a.append(500)

a
```
```py
a = []
a.append(10)

a
```
```py
a = [10, 20, 30]
b = [40, 50, 60]

a.extend(b)

a
```
```py
b
```
```py
a   # 기존 리스트가 변경됨
```
# 참고      기존 리스트는 변경되지 않음
```py
a = [10, 20, 30]
b = [40, 50, 60]

a + b
```
```py
a
```
```py
b
```
```
a.insert(location, something to insert)
```
```py
a.insert(1, 500)

a
```
- insert(0, element): add at the first of list
- insert(len(list), element): add at the last of list
```py
a = [10, 20, 30]
a.insert(0, 100)
a
```
```py
a.insert(len(a), 1000)
a
```
```py
a.insert(-1, 2000)
a
```
- pop: delete last element or specular index
- remove: delete someothing value
```py
a = [10, 20, 30]
x = a.pop()
x
```
```py
a
```
```py
a = [10, 20, 30]
x = a.pop(1)       # index
x
```
```py
a
```
```py
a = [10, 20, 30]
a.remove(20)      # value

a
```
- index(value): 리스트에서 특정 값의 인덱스 구함
- count(value): 리스트에서 특정 값의 개수를 구함
```py
a = [10, 20, 30]
a.index(20)
```
```py
a = [10, 10, 20, 30, 30, 30]

a.count(10)
```
```py
a.count(30)
```
- reverse(): 리스트에서 요소의 순서를 반대로 뒤집음.
- sort(): 리스트의 요소를 정렬함(오름차순 기본값)
```py
a = [10, 20, 30]
a.reverse()

a
```
# 참고 슬라이스로 뒤집기
```py
a[-1::-1]
```
```py
a = [10, 50, -1, 0, 4, 10000]
a.sort()     # reverse = False
a
```
```py
a = [10, 50, -1, 0, 4, 10000]
a.sort(reverse = True)
a
```
- =
- copy()
```py
a = [0, 0, 0, 0]
b = a            # 새로운 메모리가 할당되진 않고 a가 쓰는 메모리를 가리키는 것이다.

b
```
```py
a
```
```py
a is b
```
```py
b[1] = 1000

b
```
```py
a is b

a              # 같은 메모리를 공유하기 때문에 b를 바꿔도 a도 바뀜
```
```py
a = [0, 0, 0, 0]
b = a.copy()       # copy()를 사용해 b를 위한 또다른 메모리 할당

a
```
```py
b
```
```py
a[1] = 1000

a          # 변경된 a의 메모리
```
```py
b          # 변경되지 않은 b의 또다른 메모리
```
- copy()와 deepcopy()
```py
a = [[10, 20], [30, 40]]    # 2차원 리스트
b = a

a
```
```py
b
```
```py
b[0]
```
```py
b[0][0] = 3000   # 2차원 리스트를 2번 색인해서 원소값에 접근

b
```
```py
a
```
```py
a = [[10, 20], [30, 40]]
b = a.copy()
```
```py
b[0][0] = 3000
b
```
```py
a          # copy()를 사용했음에도 메모리가 따로 할당되지 않았다.
```
```py
import copy                   # import copy module

a = [[10, 20], [30, 40]]
b = copy.deepcopy(a)          # 2차원 리스트부터는 copy module에 deepcopy를 사용

a
```
```py
b
```
```py
b[0][0] = 3000

b
```
```py
a
```
# print the list elements using repeat string

- for element in list
```py
a = [10, 20, 30]
for v in a:
    print(v)
```
```py
for i in range(len(a)):         # C언어 방식 - 파이썬이 more simple
    print(a[i])
```
- for index, element in enumerate(list):
```py
a = [10, 20, 30]
for i, v in enumerate(a, start = 1):          # start 활용
    print(i, v)        # i: index, v: value
```
**리스트의 가장 작은 수, 가장 큰 수, 합계**
```py
a = [10, 20, 30]
```
```py
min(a)
```
```py
max(a)
```
```py
sum(a)
```
```py
sum(a)/len(a)        # average
```
**리스트 표현식(List comprehension)**

- [식 for 변수 in 리스트]
```py
list(range(10))
```
```py
for i in range(10):
    print(i * 2)
```
# 1. for문 이용, list의 append()함수 이용
```py
l = []
for i in range(10):
    l.append(i * 2)
l
```
# 2. 리스트 표현식
```py
[i * 2 for i in range(10)]
```
```py
word_list = ["Python", "is", "easy"]
```
```py
[6, 2, 4]
```
단어 길이 리스트로 구하기

# 1
```py
word_count = []
word_list = ["Python", "is", "easy"]
for word in word_list:
    word_count.append(len(word))
word_count
```
# 2
```
[len(word) for word in word_list]

- [식 for 변수  in 리스트 if 조건식]

[i for i in range(10) if i % 2 == 0]
```
```py
l = []
for i in range(10):
    if i % 2 == 0:
        l.append(i)
l
```
### Workshop
```py
a = ['awfnawkn', 'awkjfa', 'afawf', 'awff', 'awfaw', 'wrtnn', 'nrtnwr', 'asdasd', 'awdaa']

[i for i in a if len(i) == 5]
```
**리스트에서 map 사용하기**
```py
a = [1.2, 2.5, 3.7, 4.6]
l = []
```
```py
for i in a:
    l.append(int(i))
l
```
# 위의 코드와 동일한 결과. But, for문을 사용하지 않고 map을 사용해서 일괄 적용 
```py
list(map(int, a))
```
# applying tuple

- index(value): 특정값의 인덱스 구하기
```py
a = (10, 20, 30)
a.index(30)
```
- count(value): 특정값의 개수 구하기
```py
a = (10, 10, 10, 20, 30, 30)
a.count(10)
```
### Workshop

**자동 로또 번호 생성기**
- 1~45 숫자 중에서 6개를 고르는 로또 번호를 자동으로 만들어 주는 프로그램 작성하기
- 사용자가 입력한 개수만큼 번호 쌍을 생성하기(예: 5를 입력하면 5 세트의 번호가 생성되도록 하기)
- 한번 뽑히것은 뽑히지 않도록 하고, 최종 출력은 오름차순 정렬해서 보여주기
```py
import random

a = []
c = []
b = int(input())

for i in range(6):
    a.append(random.randint(1, 45))
    a.sort()
    
    if i not in a:
        for j in range(b):
            c.append(a)
print(c)
```
```py
count = int(input("로또 몇 회 뽑으시겠습니까? "))

total = []
for i in range(count):
    lotto = []
    while True:       # 무한 루프는 break문 필수
        pick = random.randint(1, 45)
        if pick not in lotto:
            lotto.append(pick)

        if len(lotto) >= 6:
            break
    lotto.sort()
    total.append(lotto)
total     
```
```py
count = int(input("로또 몇 회 뽑으시겠습니까? "))

total = []
for i in range(count):
    lotto = random.sample(range(1, 46), 6)
    lotto.sort()
    total.append(lotto)
total
```
# 문자열 응용하기

- replace('바꿀문자열', '새문자열'): 문자열 바꾸기
```py
s = "Hello, World!"
result = s.replace('World!', 'Python!')
result

s
```
- split('기준문자열'): 문자열 분리하기
```py
s = 'apple pear grape pineapple orange'
result = s.split()
result

s
```
```py
s = 'apple.pear.grape.pineapple.orange'
result = s.split('.')
result
```
- '구분자'.join(list)

'-'.join(result)

- upper(): 대문자로 바꿈
- lower(): 소문자로 바꿈
- strip(): 문자열 양쪽에 있는 연속된 모든 공백을 삭제
- lstrip(): 문자열 왼쪽에 있는 연속된 모든 공백을 삭제
- rstrip(): 문자열 오른쪽에 있는 연속된 모든 공백을 삭제
```py
'python'.upper()
```
```py
'PYTHON'.lower()
```
```py
'          python        '.strip()
```
```py
'            python          '.lstrip()
```
```py
'            python          '.rstrip()
```
```py
' .,.    .,     python   .,.,.,.       '.strip(',. ')
```
```py
'python'.center(20)    # 20(길이)만큼의 전체 사이즈를 확보하고 문자열을 중간에 배치
```
- index('찾을문자열'): 문자열에서 특정문자열을 찾아서 인덱스를 반환하고, 없으면 에러
- find('찾을문자열'): 문자열에서 특정문자열을 찾아서 인덱스를 반환하고, 없으면 -1 반환
```py
s = 'apple pear grape pineapple orange'
s.index('pl')
```
```py
s.rindex('pl')    # 오른쪽부터 탐색
```
```py
s.index('oooo')
```
```py
s.find('okkk')
```
```py
s.find('pl')
```
```py
s.rfind('pl')        # index()와 같이 기본적으로 왼쪽부터 찾는다.
```

- count('문자열'): 현재 문자열에서 특정 문자열이 몇 번이나 나오는지 알아냄
```py
s.count('pl')
```
**서식 지정자**
```py
"나는 지우근입니다."
```
```py
name = input()
"나는 %s입니다." % name
```
```py
age = int(input())
"나이는 %d세 입니다." % age
```
```py
score = float(input())
"제 학점은 %.1f입니다." % score
```
```py
name = input()
age = int(input())
score = float(input())
```
```py
"제 이름은 %s이며 나이는 %d세 학점은 %.1f입니다." % (name, age, score)
```
**format함수**
```py
name = '지우근'
"나는 {}입니다.".format(name)
```
```py
name = '지우근'
f"나는 {name}입니다."
```
# Applying dictionary

- setdefault: key:value twin add
- update: 키의 값 수정, 키가 없으면 키-값 쌍 추가

shift + tab: 해당 단어에 대한 정보 열람
```py
x = {'a': 10, 'b': 20, 'c': 30, 'd': 40}
type(x)
```
```py
x.setdefault('e', 50)        # setdefault는 ,(comma)로 연결

x
```
```py
x.setdefault('f')          # value를 추가하지 않으면 None으로 출력
x
```
```py
x.update({'a': 100, 'b': 200})           # update는 :(colon)으로 연결

x
```
```py
x.update({'a': 1000, 'b': 2000, 'g': 1234})

x
```
- pop(key): 특정 키-값 쌍을 삭제한 뒤, 삭제한 값을 반환
- pop(key, default): 키가 없을 때 기본값을 반환
- clear(): 딕셔너리의 모든 키-값 쌍을 삭제
```py
x

result = x.pop('a')
result
```
```py
x
```
```py
result = x.pop('a', 0)
result
```
```py
result = x.pop('b', 0)
result
```
```py
x
```
- get(key): 특정 키의 값을 가져옴
- get(key, default): 키가 없을 때 기본값을 반환
```py
x
```
```py
result = x.get('c')
result
```
```py
x             # pop()과는 다르게 딕셔너리에서 사라지지 않는다.
```
```py
result = x.get('z', 0)
result
```
```py
x
```
- item(): 키-값 쌍을 모두 가져옴
- keys(): 키를 모두 가져옴
- values(): 값을 모두 가져옴
```py
x
```
```py
x.items()
```
```py
x.keys()
```
```py
x.values()
```
- for key, value in dictionary.items():
```py
for k, v in x.items():
    print(k, v)
```
```py
for k in x.keys():
    print(k)
```
```py
for v in x.values():
    print(v)
```
# set

- set = {value1, value2, value3, ...}
```py
fruits = {'strawberry', ' grape', 'orange', 'pineapple', 'cherry'}
type(fruits)
```
```py
fruits
```
```py
fruits = {'strawberry', 'strawberry', ' grape', 'orange', 'pineapple', 'cherry'}
```
```py
fruits     # 세트는 중복이 없고(유일한 값만 사용), 순서도 없다.
```
```py
x = {'a', 'a', 'b'}
y = {'a', 'b', 'a'}
z = {'b', 'a'}
```
```py
x == y
```
```py
x == z
```
```py
y == z            # 순서, 중복이 없기에 모두 같은 set이다.
```
```py
d = {}
type(d)
```
```py
s = set()     # 빈 set 만드는 방법
```
### Workshop

**리스트와 반복문**
- 아래에 주어진 리스트 l1의 요소 중에서 l2의 요소와 값이 같은 경우 삭제하는 파이썬 코드 작성하기

```
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']
결과 l1
['c', 'd']
```
```py
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']
```
```py
s1 = set(l1)
```
```py
s1
```
```py
s2 = set(l2)

s2
```
```py
s3 = s1 - s2

s3
```
```py
l3 = list(s3)

l3
```
```py
l1 = ['a', 'b', 'c', 'd', 'a', 'b', 'a', 'b']
l2 = ['b', 'a']
```
```py
for c2 in l2:    # b -> a
    while c2 in l1:
        print(c2, 'will be removed')
        l1.remove(c2)
l1
```
---

**'the'의 개수 출력하기**
- 아래 문자열에서 'the'의 개수를 출력하는 프로그램을 만드세요. 
- 단 , 모든 문자가 소문자인 'the'만 찾으면 되며 'them', 'there', 'their' 등은 포함되지 않아야 합니다.
```py
s = "the grown-ups' response, this time, was to advise me to lay aside my drawings of boa constrictors, whether from the inside or the outside, and devote myself instead to geography, history, arithmetic, and grammar. That is why, at the, age of six, I gave up what might have been a magnificent career as a painter. I had been disheartened by the failure of my Drawing Number One and my Drawing Number Two. Grown-ups never understand anything by themselves, and it is tiresome for children to be always and forever explaining things to the."

a = s.count(' the')

a
```
```py
word_list = s.split()

for word in word_list:
    if word == 'the':
        print(word)
```
```py
word_list = s.split()

for word in word_list:
    if word.strip(',.') == 'the':
        print(word)
```
---

**평균 점수 구하기**
- 다음 소스 코드를 완성하여 평균 점수가 출력되게 만드세요
```py
maria = {'korean' : 94, 'english': 91, 'mathmatics': 89, 'science': 83 }

scores = maria.values()

scores
```
```py
average = sum(scores) / len(scores)

average
```
```py
total_v = 0
for v in maria.values():
    total_v = total_v + v
total_v/len(maria)
```
---

**딕셔너리에서 특정값 삭제하기**
- 표준 입력으로 문자열 여러개와 숫자 여러개가 두 줄로 입력되고, 첫 번째 줄은 키, 두번째 줄은 값으로 하여 딕셔너리를 생성합니다.
- 다음 코드를 완성하여 딕셔너리에서 키가 'delta'인 키-값 쌍과 값이 30인 키-값 쌍을 삭제하도록 만드세요.

```
입력
alpha bravo charlie delta
10 20 30 40
결과
{'alpha':10, 'bravo':20}
```
```py
k = ['alpha', 'bravo', 'charlie', 'delta']
v = [10, 20, 30, 40]
```
```py
d = dict(zip(k, v))

d
```
```py
d.pop('delta')

d
```
```py
d.pop('charlie', 30)

d
```
```py
keys = input("key:: ").split()
values = map(int, input("value: ").split())

keys
```
```py
values
```
```py
d = dict(zip(keys, values))
d
```
```py
d.pop('delta')
d
```
### option 1
```py
n = {}

for k, v in d.items():
    if v != 30:
        n.setdefault(k, v)
n
```
```
# list comprehension
[식 for 변수 in 리스트 if 조건식]
```
```
# dictionary comprehension
{키:값 for 변수 in 리스트 if 조건식}
```
### option 2
```py
{k : v for k, v in d.items() if v != 30}
```
# 최종
```py
{k : v for k, v in d.items() if k != 'delta' and v != 30}       # 하나의 식으로 'delta'와 30에 해당되는 키와 값을 모두 제거
```
# 파일 사용하기

- 파일객체 = open("파일이름", "파일모드")
- 파일객체.write("문자열")
- 파일객체.close()
```py
fd = open("hello.txt", "w")
fd.write("hello world!")
fd.close()
```
```py
!dir
```
- 파일객체 = open("파일이름", "파일모드")
- 변수 = 파일객체.read()
- 파일객체.close()
```py
fd = open("hello.txt", "r")
s = fd.read()     # 파일 안에 있는 모든 데이터를 가져옴
print(s)
fd.close()
```
```
if xxxxx:
    ----
    ----
```
```
with open("파일이름", "파일모드") as fd:
    코드
```
```py
with open('hello.txt', 'r') as fd:
    s = fd.read()
    
print(s)
```
```py
fd = open("hello.txt", "r")
s = fd.read()
print(s)
fd.close()
```
```py
with open('hello.txt', 'w') as fd:
    for i in range(3):
        fd.write("Hello World!!! \n")
```
```py
with open('hello.txt', 'w') as fd:
    for i in range(3):
        fd.write("Hello World!!! {} \n".format(i))
```
```py
line_list = ["여기는 \n", "플레이데이터입니다. \n", "오늘도 \n", "화이팅 \n"]
with open('play.txt', 'w') as fd:
    fd.writelines(line_list)   #writelines는 여러 라인을 출력할 수 있음
```
```py
with open('play.txt', 'r') as fd:
    lines = fd.readlines()

lines
```
```
# fd.read(): 파일에 있는 모든 데이터를 읽음
# fd.readline(): 한 줄로 읽은 문자열을 반환
# fd.readlines(): 라인별로 읽은 문자열들을 리스트 형태로 반환

# fd.write(문자열): 파일에 문자열을 씀
# fd.writelines(문자열): 리스트에 있는 여러 문자열을 한 라인씩 씀
```
```py
with open('play.txt', 'r') as fd:
    line = fd.readline()
line
```
```py
with open('play.txt', 'r') as fd:
    line = None
    while line != '':
        line = fd.readline()
        print(line)
```
```py
with open('play.txt', 'r') as fd:
    line = None
    while line != '':
        line = fd.readline()
        print(line.strip('\n'))
```
```py
import pickle
```
```py
name = "james"  # 파이썬 문자열 객체
age = 17        # 파이썬 정수 객체
scores = {'korean': 90, 'english': 80}       # 파이썬 딕셔너리 객체
```
```py
with open("student.pkl", "wb") as fd:          # wb: write binary mode
    pickle.dump(name, fd)
    pickle.dump(age, fd)
    pickle.dump(scores, fd)
```
....
```py
with open("student.pkl", "rb") as fd:
    loaded_name = pickle.load(fd)
    loaded_age = pickle.load(fd)
    loaded_scores = pickle.load(fd)
```
```py
loaded_name
```
```py
loaded_age
```
```py
loaded_scores
```
### Workshop

**파일에서 10자 이하인 단어 개수 세기**
- 단어가 줄 단위로 저장된 words.txt 파일이 주어집니다. 10자 이하인 단어의 개수가 출력되게 만드세요.
```py
with open('words.txt', 'r') as fd:
    word_list = fd.readlines()
    for word in word_list:
        if len(word.rstrip('\n')) <= 10:
            count += 1
count
```

---

**특정 문자가 들어 있는 단어 찾기**
- 문자열이 저장된 words2.txt 파일이 주어집니다(문자열은 한 줄로 저장되어 있습니다). 
words2.txt 파일에서 문자 c가 포함된 단어를 각 줄에 출력하는 프로그램을 만드세요.
단어를 출력할 때는 등장한 순서대로 출력해야 하며 ,(콤마)와 .(점)은 출력하지 않아야 합니다.
```py
with open('words2.txt', 'r') as fd:
    paragraph = fd.read()
    word_list = paragragh.split()
    for word in word_list:
        if 'c' in word:
            print(word.strip = ',.')
```
# 함수

- 코드의 용도 구분
- 코드를 재사용
- 실수를 줄일 수 있음
```py
def hello():
    print("Hello World!")
```
```
def 함수이름():
    코드
```
```py
hello()
```
```py
def add(num1, num2):
    return num1 + num2

add(1, 2)
```
```py
def add1(a, b):
    c = a + b
    print(c)
```
```py
add(1, 2)
```
```py
add(5, 7)
```
```py
add(124, 5129590129501)
```
```py
add(1028508125, 102959012905)
```
```
def 함수이름(매개변수1, 매개변수2):
    코드
    return 반환값
```
```py
def add2(a, b):
    c = a + b
    return c          # return이 없으면 결과값을 변수에 할당하고 출력할 수가 없게 된다.
```
```py
add2(8129, 1590)
```
```
def 함수이름(매개변수1, 매개변수2):
    코드
    return 반환값1, 반환값2
```
```py
def add_sub(a, b):
    return a + b, a - b

add_sub(10, 5)
```
```py
a
```
**I have a dream 연설문 단어 빈도수 계산**
- WordCount 함수에서 ihaveadream.txt 파일을 열어 전체 내용 중 단어를 키로, 빈도를 값으로 매핑한 사전형 자료를 반환하세요.
- 단 stopwords.txt에 있는 단어는 제외시킵니다.
- WordCount 함수의 결과를 result.txt로 저장하세요.
- majorityCnt 함수에서 사전형 자료를 인수로 받아 값을 기준으로 내림차순으로 정렬하여 값이 가장 큰 키를 반환하세요.
```py
with open("ihaveadream.txt", "r") as fd:
    word = None
    while word != '':
        word = fd.readline()
        print(word.split())
```
```py
with open("stopwords.txt", "r") as fd:
    stop = None
    while stop != '':
        stop = fd.read()
        a = list(stop.split())
        
        print(a)
```
```py
with open ('ihaveadream.txt', 'r') as fd1:
    speech = fd1.read()
with open('stopwords.txt', 'r') as fd2:
    stopwords = fd2.read()
```
```py
word_list = speech.lower().split()
stop_list = stopwords.lower().split()
```
```py
len(word_list), len(stop_list)
```
### option 1
```py
d = {}
for word in word_list:    # word: i -> am -> happy -> ....
    if word in stop_list:
        continue
    if word not in d:
        d[word] = 1       # 이 단어가 처음 등장해서 최초로 카운트
    else:
        d[word] += 1      # 이미 단어가 등록된 경우에는 카운트 누적

d
```
### option 2
```py
d = {}
for word in word_list:    # word: i -> am -> happy -> ....
    if word in stop_list:
        continue
    d[word] = d.get(word, 0) + 1      # 이미 단어가 사전에 있으면 pass, 없으면 value로 0을 가져온다.

d
``
### option 3
```py
def WordCount():
    d = {}
    for word in word_list:    # word: i -> am -> happy -> ....
        if word in stop_list:
            continue
        d[word] = d.get(word, 0) + 1      # 이미 단어가 사전에 있으면 pass, 없으면 value로 0을 가져온다.
    return d
```    
```py
d = WordCount()
with open('result.txt', 'w') as fd3:
    fd3.write(str(d))
```
**(참고) 정렬**
```py
l = [1, 4, 5, 6, -1, -10]
l.sort()      # 리스트에서 제공하는 sort() 메서드를 사용
l          # 오름차순으로 정렬된 것이 l에 반영
```
```py
l = [1, 4, 5, 6, -1, -10]
result = sorted(l)     # sorted() 함수는 다른 시퀀스 객체에서도 사용할 수 있음
result       # 정렬의 결과물이 반환되고, l은 원본 그래로
```
```py
l
```
### 단어의 리스트가 준비
```py
words = ["abc", "defgh", "i", "jklm", "nm"]
```
```py
list(map(len, words)) # 각 단어의 길이 값이 나옴
```
```py
sorted(words, key = len)      # key 매개변수에 적당한 함수를 제공해주면, 그에 맞게 정렬
```
```py
# 딕셔너리 정렬  (높은 점수 순으로 정렬)
scores = {"James": 90, "Selly": 80, "Jun": 100}
```
### option 1
```py
def return_score(x):
    # print(x)
    return x[1]
```
```py
sorted(scores.items(), key = return_score, reverse = True)      # key에 함수만 주어도 자동으로 순서대로 정렬해준다.
```
### option 2
```py
sorted(scores.items(), key = lambda x : x[1], reverse = True)
```
---
```py
d
```
```py
sorted(d.items(), key = return_score, reverse = True)
```
```py
def majorityCnt(d):
    result  = sorted(d.items(), key = return_score, reverse = True)
    return result[0]
```
```py
most_freq_word = majorityCnt(d)
print(most_freq_word)
```
```py
def majorityCnt(d):
    result = sorted(d.items(), key = lambda x : x[1], reverse = True)
    return result[0]
```
```py
most_freq_word = majorityCnt(d)
print(most_freq_word)
```
**참고** 
- 단어 리스트에서 개별 단어들 strip 하려면
```py
a = ["abc", "def,"]
```
```py
[word.strip(',.') for word in a]
```
```py
list(map(lambda x : x.strip(',.'), a))
```
# Day 4 review

- set
- dictionary method
- file
- def function
- strip 문자열에 사용 가능

# 위치 인수와 키워드 인수

# 위치 인수
```py
def print_numbers(a, b, c):
    print(a)
    print(b)
    print(c)
```
```py
print_numbers(10, 20, 30)
```
```py
x = [10, 20, 30]
print_numbers(*x)       # *는 언패킹한다는 의미
```
# 가변 인수
```py
def print_numbers(*args):      # args(arguments)는 집합체로 원소의 개수가 가변적인 원소
    for arg in args:
        print(arg)
```
```py
print_numbers(200)
```
```py
print_numbers(200, 300)
```
```py
print_numbers(200, 300, 400)
```
```py
print_numbers(200, 300, 400, 500)
```
# 키워드 인수
```py
def personal_information(name, age, address):
    print(name)
    print(age)
    print(address)
```
```py
personal_information("장경희", 25, "경기 파주")
```
```py
personal_information(name = "지우근", age = 25, address = "경기 파주")
```
```py
personal_information(name = "지우근", address = "경기 파주", age = 25)   # 순서 바뀌어도 함수에 입력되어 있는 순서대로 출력함
```
# 초기값 설정
```py
def personal_information(name, age, address = "경기 파주"):
    print(name)
    print(age)
    print(address)
```
```py
personal_information(name = "지우근", age = 25)          # 초기값 설정 상태기 때문에 따로 입력해주지 않아도 출력됨
```
```py
personal_information(name = "지우근", age = 25, address = "서울 강남")    # 초기값 변환 가능
```
# 딕셔너리를 사용하여 호출하는 경우
```py
d = {'name': "지우근", 'age': 25, 'address': "경기 파주"}
personal_information(*d)
personal_information(**d)                # 언패킹 1회: key 출력, 언패킹 2회: value 출력
```
# 키워드 인수를 가변적으로 처리
```py
def personal_info(**kwargs):        # kwargs에는 가변적인 개수의 키와 값의 쌍으로 이루어짐
    for k, v in kwargs.items():
        print(k, v)
```
```py
personal_info(name = "지우근", age = 25, adderss = "파주", sex = 'male', blood = 'AB')
```
# 함수에서 재귀 호출 사용하기
```py
def hello():
    print("Hello")
    hello()
hello()
```
```py
def hello(count):
    if count == 0:        # 재귀 호출 할 경우에는 종료 조건이 반드시 있어야 함
        return
    print('hello world', count)
    count -= 1
    hello(count)
```
```py
hello(5)
```
# 재귀 함수는 반복문을 통해서도 동일하게 구현 가능
```py
def hello(count):
    for i in range(count):
        print('hello world')
```
```py
hello(7)
```
```py
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1
```
```py
a = 0
for i in range(10, 0, -1):
    a += i
a
```
```py
def add_sum(i):
    if i == 1:
        return 1
    
    sum = i + add_sum(i - 1)
    
    return sum
```
```py
add_sum(10)
```
---

# 재귀함수 연습

### 코딩 테스트를 위한 연습
```
# 팩토리얼 (반복)
# n! = n * (n - 1) * (n - 2) * (n - 3) * ... * 1
```
```py
fact_val = 1
for i in range(5, 0, -1):
    fact_val = fact_val * i
    
print(fact_val)
```
# 팩토리얼 (재귀함수)
```py
def fact(n):
    if n == 1:
        return 1
    fact_val = n * fact(n - 1)
    
    return fact_val
```
```py
fact(6)
```
# 구구단 출력
```py
def gugu(n):
    if n == 9:
        return 9
    gugudan = n + gugu(n + 1)
    
    return gugudan
```
```py
gugu(0)
```
```py
def gugu(x, y):       # x: 단위, y: 1, 2, ...
    print(x, '*', y, '=', x * y)
    if y < 9:
        gugu(x, y + 1)
gugu(2, 1)
```
```py
for dan in range(2, 10):
    print('------ \n')
    gugu(dan, 1)
```
# lambda 표현식
```py
def plus_ten(x):
    return x +10
```
```py
plus_ten(2)
```
- lambda 매개변수: 식
```py
plus_ten = lambda x : x + 10
```
```py
plus_ten(1)
```
```py
(lambda x : x + 10) (1)
```
- lambda 매개변수: 식1 if 조건식 else 식2
```py
a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```
```
# 3의 배수이면 문자열로 만들고, 그렇지 않으면 있는 그대로 출력하기
# lambda 식 이용
```
```py
myformat = lambda x : str(x) if x % 3 == 0 else x
```
```py
list(map(myformat, a))
```
```py
list(map(lambda x : str(x) if x % 3 == 0 else x, a))
```
```py
a = [1, 2, 3, 4, 5]
b = [2, 4, 6, 8, 10]
```
```py
mul = lambda x, y : x * y
```
# 두 리스트를 요소별로 곱셈한 결과를 리스트로 출력
```py
list(map(mul, a, b))
```
- map(함수, 반복 가능한 객체): 반복 가능한 객체에 함수를 일괄 적용
- filter(함수, 반복 가능한 객체): 반복 가능한 객체에 함수에서 출력하는 조건에 맞는 것만 가져옴
```py
def f(x):
    return x > 5 and x < 10    # True or False
```
```py
a = [3, 2, 8, 10, 1, 16, 21, 0]
```
```py
list(filter(f, a))
```
### Workshop

**거리계산**
- 리스트를 이용하여 점 사이의 거리를 계산 해 보자.
- 직교 좌표 위에서 A는 (1, 1), B는 (3, 2), C는 (5,7)일 때 X(2, 3)와  A/B/C와의 거리를 각각 구하여라.
- 위 코드블럭을 이용하여 distMeasure 함수를 정의하라.
```py
import math
```
```py
points = [(1, 1), (3, 2), (5, 7)]     # A B C
x = (2, 3)
```
```py
dis = lambda x, y : ((x[0] - y[0]) ** 2 + (x[1] - y[1]) ** 2) ** (1 / 2)     # 리스트 간의 크기가 다르기 때문에 함수를 통해 해결
```
```py
distance = list(map(dis, points[i], x))       # map 자체가 일괄적용이 되기 때문에 for문을 사용할 필요는 없다
print(distance)
```
### option 1
```py
points = [(1, 1), (3, 2), (5, 7)]     # A B C
x = (2, 3)
```
```py
def distMeasure():
    result = []
    for point in points:   # A, B, C
        dist = ((point[0] - x[0]) ** 2 + (point[1] - x[1] ** 2)) ** (1 / 2)
        print(dist)
    return result
```
```py
result = distMeasure()
result
```
### option 2
```py
points = [(1, 1), (3, 2), (5, 7)]     # A B C
x = (2, 3)
```
```py
def distMeasure_1p(point):   # A or B or C
    dist = ((point[0] - x[0]) ** 2 + (point[1] - x[1]) ** 2) ** (1 / 2)
    return dist
```
```py
list(map(distMeasure_1p, points))
```
### option 3
```py
distMeasure_2p = lambda point: ((point[0] - x[0]) ** 2 + (point[1] - x[1]) ** 2) ** (1 / 2)
```
```py
list(map(distMeasure_2p, points))
```
### option 4
```py
list(map(lambda point: ((point[0] - x[0]) ** 2 + (point[1] - x[1]) ** 2) ** (1 / 2), points))
```
**이미지 파일만 가져오기**
- 다음 소스 코드를 완성하여 확장자가 .jpg, .png인 이미지 파일만 출력되게 만드세요. 여기서는 람다 표현식을 사용해야 하며 출력 결과는 리스트 형태라야 합니다. 람다 표현식에서 확장자를 검사할 때는 문자열 메서드를 활용하세요.
```
files = ['font', '1.png', '10.jpg', '11.gif', '2.jpg', '3.png', 'table.xslx', 'spec.docx']
실행결과
['1.png', '10.jpg', '2.jpg', '3.png']
```
```py
files = ['font', '1.png', '10.jpg', '11.gif', '2.jpg', '3.png', 'table.xslx', 'spec.docx']
a = []
for word in files:
    if '.png' in word:
        a.append(word)
    elif '.jpg' in word:
        a.append(word)
a
```
```py
def filter_img(file):
    if ('jpg' in file) or ('png' in file):
        return True
list(filter(filter_img, files))
```
```py
'10.jpg'.find('.jpg')
```
```py
def filter_img(file):
    if file.find('.jpg') != -1 or file.find('png') != -1:
        return True
list(filter(filter_img, files))
```
```py
filter_img = lambda file: file.find('.jpg') != -1 or file.find('png') != -1
```
```py
list(filter(filter_img, files))
```
```py
list(filter(lambda file: file.find('.jpg') != -1 or file.find('png') != -1, files))
```
**파일 이름을 한꺼번에 바꾸기**
```
표준 입력으로 숫자.확장자 형식으로 된 파일 이름 여러 개가 입력됩니다.
파일 이름이 숫자 3개이면서 앞에 0이 들어가는 형식으로 출력되게 만드세요. 
예를 들어 1.png는 001.png, 99.docx는 099.docx, 100.xlsx는 100.xlsx처럼 출력되어야 합니다. 
그리고 람다 표현식을 사용해야 하며 출력 결과는 리스트 형태라야 합니다.
람다 표현식에서 파일명을 처리할 때는 문자열 포매팅과 문자열 메서드를 활용하세요.
```
```py
files = input().split()
```
```py
files
```
```py
names = []
exts = []
for file in files:
    name = file.split('.')[0]
    names.append(int(name))
    
    ext = file.split('.')[1]
    exts.append(ext)
```
```py
names = []
for file in files:
    name = file.split('.')
    names.append(name)

names
```
```py
names, exts
```
```py
names
```
```py
name = 1
ext = 'jpg'
# 001.jpg
"{:03d}.{}".format(name, ext) 
```
```py
def fmt(name, ext):
    return "{:03d}.{}".format(name, ext)
```
```py
list(map(fmt, names, exts))
```
```py
list(map(lambda name, ext : "{:03d}.{}".format(name, ext), names, exts))
```
# 변수의 사용범위
```py
x = 10
```
```py
def foo():
    print("foo()", x)
```
```py
foo()
print("main()", x)
```
```py
x = 10     # 전역 변수
```
```py
def foo():      # 지역 변수
    x = 20
    print("foo()", x)
    
foo()
print("main()", x)
```
```py
x = 10     # 전역 변수

def foo():      # 지역 변수
    global x      # 전역변수화
    x = 20
    print("foo()", x)
    
foo()
print("main()", x)    # 함수 내부에서 수정된 x가 바깥에서도 유효 (x가 global로 선언)
```
# 클래스

```
class 클래스이름:        # 붕어빵 틀
    def method(self):
        code
```

class Person:
    def greeting(self):
        print("Hello")

```
인스턴스 = 클래스() # 붕어빵
```
```py
james = Person()
mary = Person()
```
```py
james.greeting()
```
```py
mary.greeting()
```
```
인스턴스.메서드()
```
```py
# 파이썬에서 흔히 볼 수 있는 클래스
a = int(10)
print(type(a))
```
```py
b = list(range(10))
print(type(b))
```
```py
b.append(3) # 인스턴스 메서드를 사용한 예
```
```
class 클래스 이름:
    def __init__(self):
        self.속성 = 값    # 붕어빵 앙꼬
```
```py
class Person:
    def __init__(self):
        self.hello = "안녕하세요"
    
    def greeting(self):
        print(self.hello)

james = Person()
james.greeting()

selly = Person()
selly.greeting()
```
```
class 클래스 이름:
    def __init__(self, 매개변수1, 매개변수2, ....):
        self.속성 = 매개변수1
        self.속성 = 매개변수2
        
```
```py
class Person:
    def __init__(self, hello_msg):
        self.hello = hello_msg
    
    def greeting(self):
        print(self.hello)
    

james = Person("안녕하십니까")
james.greeting()

selly = Person("하이")
selly.greeting()
```
```py
class Person:
    def __init__(self, hello_msg, name, age, address):
        self.hello = hello_msg
        self.name = name
        self.age = age
        self.address = address
    
    def greeting(self):
        print(self.hello)
        print("저는 {}입니다.".format(self.name))
        print("나이는 {}살입니다. ".format(self.age))
        print("사는 곳은 {}입니다.".format(self.address))
    
```
```py
UGeun = Person("하이", "우근", 25, "집")
```
```py
UGeun.greeting()
```
```py
maria = Person("Hi", "마리아~", 21, "지이이입")
maria.greeting()      # method 호출
```
```py
maria.name
```
```py
maria.age
```
```py
maria.address
```
```py
maria.hello
```
```py
class 클래스이름:
    def __init__(self, 매개변수):
        self.__속성 = 값     # 비공개 속성
```
```py
class Person:
    def __init__(self, hello_msg, name, age, address, wallet):
        self.hello = hello_msg
        self.name = name
        self.age = age
        self.address = address
        self.__wallet = wallet   # 비공개 속성
    
    def greeting(self):
        print(self.hello)
        print("저는 {}입니다.".format(self.name))
        print("나이는 {}살입니다. ".format(self.age))
        print("사는 곳은 {}입니다.".format(self.address))
        
    def pay(self, amount):
        self.__wallet = self.__wallet - amount
        print("지갑에 {}원 남았습니다.".format(self.__wallet))
```
```py
selly = Person("안뇽", "selly", 22, "강남역", 100000000000)
```
```py
selly.greeting()
```
```py
selly.name
```
```py
selly.wallet    # 비공개 속성은 외부에서 접근하면 에러가 생김
```
```py
selly.pay(2124214000)
```
 # 클래스 속성과 인스턴스 속성

```
class 클래스 이름:
    속성 = 값
```

- 클래스 속성; 모든 인스턴스들이 공유. 인스턴스 전체가 사용해야 하는 값을 저장할 때 사용
- 신스턴스 속성: 인스턴스 별로 독립되어 있음. 각 인스턴스 값을 따로 저장할 때 나옴

# 클래스 속성 bag을 사용하여 인스턴스 모두가 공용으로 사용
```py
class Person:
    bag = []
    
    def put_bag(self, stuff):
        Person.bag.append(stuff)
```
```py
james = Person()
```
```py
james.put_bag("책")
```
```py
maria = Person()
maria.put_bag("열쇠")
```
```py
james.bag
```
```py
maria.bag
```
```py
class Person:          # 인스턴스마다 bag 속성을 따로 관리
    def __init__(self):
        self.bag = []
    
    def put_bag(self, stuff):
        self.bag.append(stuff)
```
```py
james = Person()
james.put_bag("책")
```
```py
maria = Person()
maria.put_bag("열쇠")
```
```py
james.bag
```
```py
maria.bag
```
# 클래스 상속 사용하기
```
class 기반클래스이름:
    코드

class 파생클래스이름(기반클래스)
```
```py
class Person:
    def greeting(self):
        print("안녕하세요")
```
```py
class student(Person):
    def study(self):
        print("공부중입니다")
```
```py
james = student()    # 상속을 받았다
```
```py
james.study()
```
```py
james.greeting()    # 상속받은 부모 클래스(Person)의 기능까지도 사용 가능
```
```py
class Person:
    def __init__(self):
        print("Person Initialized")
        
    def greeting(self):
        print("안녕하세요")
```
```py
class Student(Person):
    def __init__(self):
        print("student Initialized")
        
    def study(self):
        print("공부중입니다")
```
```py
james = Student()   # 자식 클래스에 __init__가 정의되어 있다면 이것이 우선
```
```py
class Person:
    def __init__(self):
        print("Person Initialized")
        
    def greeting(self):
        print("안녕하세요")
```
```py
class Student(Person):
    # def __init__(self):
    #     print("student Initialized")
        
    def study(self):
        print("공부중입니다")
```
```py
james = Student() # 자식 클래스에 __init__가 정의되어 있지 않다면 부모 클래스 __init__
```
```py
class Person:
    def __init__(self):
        print("Person Initialized")
        self.hello = "안녕하세요"
        
    def greeting(self):
        print(self.hello)
```       
```py
class Student(Person):
    def __init__(self):
        print("student Initialized")
        
    def study(self):
        print("공부중입니다")
```
```py
james = Student()
james.study()
```
```py
james.greeting()
```
```py
class Person:
    def __init__(self):
        print("Person Initialized")
        self.hello = "안녕하세요"
        
    def greeting(self):
        print(self.hello)
```
```py
class Student(Person):
    def __init__(self):
        super().__init__()  # 부모 클래스의 __init__()를 강제로 호출
        print("student Initialized")
        
    def study(self):
        print("공부중입니다")
```
```py
james = Student()
james.greeting()
```
**메서드 오버라이딩**
```py
class Person:
    def greeting(self):
        print("안녕하세요")
```
```py
class Student(Person):
    def greeting(self):
        print("안녕하세요. 저는 인공지능 과정 25기 학생입니다.")
```
```py
kai = Student()
kai.greeting()
```
```py
class Person:
    def greeting(self):
        print("안녕하세요")
```
```py
class Student(Person):
    def greeting(self):
        super().greeting()
        print("저는 인공지능 과정 25기 학생입니다.")
```
```py
james = Student()
james.greeting()
```
**다중 상속 사용하기**

```
class 기반클래스1:
    코드

class 기반클래스2:
    코드
    
class 파생크래스(기반클래스1, 기반클래스2):
    코드
```
```py
class Person:
    def greeting(self):
        print("안녕하세요")
```
```py
class University:
    def manage_credit(self):
        print("학점 관리")
```
```py
class Undergraduate(Person, University):
    def study(self):
        print("공부하기")
```
```py
james = Undergraduate()
james.study()
```
```py
james.manage_credit()
```
```py
james.greeting()
```
**추상클래스**

```
from abc import *

class 추상클래스(metaclass = ABCmeta):
    @abstractmethod
    def 메서드이름(self):
        코드
```
```py
from abc import *
```
```py
class StudentBase(metaclass = ABCMeta):
    @abstractmethod
    def study(self):
        pass
    
    @abstractmethod
    def gotoschool(self):
        pass
```
```py
class Student(StudentBase):
    def study(self):
        print("공부하기")
    
    def gotoschool(self):
        print("학교가기")
```
```py
james = Student()
james.study()
```
### Workshop

**리스트에 기능 추가하기**
- 아래 예시와 같이 리스트(list)에 replace 메서드를 추가한 AdvancedList 클래스를 작성하세요. AdvancedList는 list를 상속받아서 만들고, replace 메서드는 리스트에서 특정 값으로 된 요소를 찾아서 다른 값으로 바꾸도록 만드세요.
```
x = AdvancedList([1, 2, 3, 1, 2, 3, 1, 2, 3])
x.replace(1, 100)
print(x)
결과
[100, 2, 3, 100, 2, 3, 100, 2, 3]
```

### option 1
```py
class AdvancedList(list):
    def replace(self, old, new):        # self: list 형의 데이터 (예: [1, 2, 3, ...])
        for idx, v in enumerate(self):    # idx: 0, 1, 2, 3, ....  v: 1, 2, 3, 1, 2, 3
            if v == old:
                self[idx] = new   # x[0] = 100, x[3] = 100, x[6] = 100
```                

### option 2
```py
class AdvancedList(list):
    def replace(self, old, new):        # self: list 형의 데이터 (예: [1, 2, 3, ...])
        while old in self:
            idx = self.index(old)
            self[idx] = new

x = AdvancedList([1, 2, 3, 1, 2, 3, 1, 2, 3])
x.replace(1, 100)
print(x)
```
# 예외 처리하기
- 예외처리는 에러가 발생하더라도 스크립트 실행을 중단하지 않고 계속 실행하고자 할 때 사용함
```py
x = int(input("나눌 숫자를 입력하세요: "))
```
```py
y = 10 / x
print(y)
```
```
try:
    실행할 코드
except:
    예외가 발생했을 때 처리할 코드
```
```py
try:
    x = int(input("나눌 숫자를 입력하세요: "))
    y = 10 / x
    print(y)
except:
    print("예외가 발생했습니다.")
```
```py
try:
    x = int(input("나눌 숫자를 입력하세요: "))
    y = 10 / x
    print(y)
except:
    print("예외가 발생했습니다.")
    x = int(input("0이 아닌 숫자를 다시 입력해주세요: "))
    y = 10 / x
    print(y)
```
```
특정 예외만 처리하기

try:
    실행할 코드
except 예외이름1:
    예외가 발생했을 때 처리할 코드
except 예외이름2:
    예외가 발생했을 때 처리할 코드
```
```py
try:
    x = int(input("나눌 숫자를 입력하세요: "))
    y = 10 / x
    print(y)
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
```
```py
y = [10, 20, 30]
index = int(input("인덱스를 입력하세요"))
print(y[index])
```
```py
y = [10, 20, 30]
```
```py
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index] / x
    print(y)
    
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
    
except IndexError:
    print("잘못된 인덱스입니다.")
```
```
예외 메시지 출력하기

try:
    실행할 코드
except 예외이름1 as 변수:
    예외가 발생했을 때 처리할 코드
```
```py
y = [10, 20, 30]
```
```py
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index] / x
    print(y)
    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)
    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)
```
```py
y = [10, 20, 30]
```
```py
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index] / x
    print(y)
    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)
    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)
```
```
예외 발생 여부에 따라 분기

try:
    실행할 코드
except 예외이름1 as 변수:
    예외가 발생했을 때 처리할 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
```
```py
y = [10, 20, 30]
```
```py
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index] / x    # <-- 문제가 생겼을 때 예외가 발생하는 위치
    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)
    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)

else:
    print(y)
```
```
예외 발생 여부 상관없이 처리(finally)

try:
    실행할 코드
except 예외이름1 as 변수:
    예외가 발생했을 때 처리할 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
finally:
    예외 발생 여부와 상관없이 항상 실행할 코드
```
```py
y = [10, 20, 30]
```
```py
try:
    index, x = map(int, input("인덱스와 나눌 숫자를 입력하세요: ").split())
    y = y[index] / x    # <-- 문제가 생겼을 때 예외가 발생하는 위치
    
except ZeroDivisionError as e:
    print("0으로 나눌 수 없습니다.", e)
    
except IndexError as e:
    print("잘못된 인덱스입니다.", e)

else:
    print(y)
    
finally:
    print("프로그램이 종료되었습니다.")
```
```
예외 발생시키기

raisse exeeption("에러메시지")
```
```py
x = int(input("3의 배수를 입력하세요: "))
if x % 3 != 0:    # 3으로 나눴을 때 나머지가 0이 아닌 때
    raise Exception("3의 배수가 아닙니다.")

try:
    x = int(input("3의 배수를 입력하세요: "))
    if x % 3 != 0:    # 3으로 나눴을 때 나머지가 0이 아닌 때
        raise Exception("3의 배수가 아닙니다.")
except Exception as e:     # e는 에러메시지를 받는 공간
    print("예외가 발생했습니다.", e) 
```
# 이터레이터

- **이터레이터(iterator)**는 값을 차례대로 꺼낼 수 있는 객체(object)
- 파이썬에서는 이터레이터만 생성하고 값이 "필요한 시점" 되었을 때 값을 만드는 방식을 사용
- 데이터 생성을 뒤로 미루는 방식을 지연평가(lazy evaluation)라고 함


- **반복 가능한 객체** 는 말 그대로 반복할 수 있는 객체인데 문자열, 리스트, 딕셔너리, 세트가 그 예임
- 객체 안에 요소가 여러 개 들어있고, 한 번에 하나씩 꺼낼 수 있는 객체


- 객체가 반복 가능한 객체인지 알아보는 방법은 객체의 iter 메서드가 들어 있는지 확인해 보면 됨
```py
l = [1, 2, 3]
l    # 반복 가능한 객체
```
```py
dir(l)
```
```py
iter = l.__iter__()    # l = [1, 2, 3]
iter                   # 이터레이터
```
```py
iter.__next__()    # 실체가 없는 것의 데이터를 가져온 것임
```
```py
iter.__next__()
```
```py
iter.__next__()
```
```py
iter.__next__()
```
```py
for i in range(10):
    print(i)

s = "Hello World"
s # 반복 가능한 객체
```
```py
dir(s)
```
```py
s.__iter__()
```
```py
d = {"a": 1, "b": 2}
```
```py
d.__iter__()
```
# 이터레이터 만들기

```
class 이터레이터 이름:
    def __iter__(self):
        코드
    def __next__(self):
        코드
```

# range()와 유사한 이터레이터
```py
class myrange:
    def __init__(self, stop):
        self.current = 0
        self.stop = stop
        
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current < self.stop:
            r = self.current
            self.current += 1
            return r
        
        else:
            raise StopIteration
```
```py
for i in myrange(3):
    print(i)
```
```py
it = myrange(3).__iter__()
it
```
```py
it.__next__()
```
```py
it.__next__()
```
```py
it.__next__()
```
```py
it.__next__()
```
```py
range(10)[4]
```
```py
myrange(10)[0]      # 색인은 되지 않음. range()와 완전히 같진 않음.
```
**인덱스로 접근할 수 있는 이터레이터 만들기**
- **getitem()** 함수 작성
- 딥러닝 프레임워크에 데이터셋을 준비할 때 이런 방식이 사용됨

```
class 이터레이터이름:
    def __getitem__(self, 인덱스):
        코드
```
```py
class myrange:
    def __init__(self, stop):
        self.stop = stop
        
    def __getitem__(self, index):
        if index < self.stop:
            return index
        else:
            raise IndexError

myrange(10)[6]
```
# 제너레이터

- 이터레이터를 만들어 주는 또다른 방식(함수를 사용)
- 제너레이터는 이터레이터를 생성해 주는 함수
- 이터레이터에서는 클래스 안에 iter(), next(), getitem()메서드들을 구현해야 하지만 제너레이터는 함수 안에서 yield라는 키워드만 사용하면 간단히 작성할 수 있음.
```py
def myrange2(): # 함수로써 이터레이터를 만들 수 있음
    yield 0
    yield 1
    yield 2
    yield 5
```
```py
for i in myrange2():
    print(i)
```
# 모듈과 패키지

#### 모듈을 가져오는 방법

- import module
- import module1, module2

#### 모듈을 사용하는 방법

- 모듈.variable
- 모듈.function()
- 모듈.class()
```py
import math
```
```py
math.sqrt(2)      # module.function
```
```py
math.pi      # module.variable
```
- import module as nickname
```py
import math as m
```
```py
m.sqrt(4.0)
```
```py
m.pi
```
# 참고 (데이터 분석을 위해 파이썬 생태계에서 사용하는 모듈들)
```py
import numpy as np  # 관례적으로 사용
import pandas as pd
```
- from 모듈 import 변수
- from 모듈 import 함수
- from 모듈 import 클래스
```py
from math import sqrt
```
```py
import math
```
```py
math.sqrt(2)
math.pi
```
```py
from math import pi
```
```py
pi
```
- from module import variable, function, class, ...
```py
from math import sqrt, pi
```
```py
sqrt(4)
```
```py
from math import *
```
- from module import variable as nickname
```py
from math import pi as p

p
```
**패키지 안의 모듈 가져오는 방법**
- import package.module
- import package.module1, package.module2

**패키지 안의 모듈 사용하는 방법**
- package.module.variable
- package.module.function()
- package.module.class()
```py
import urllib.request
```
```py
reponse = urllib.request.urlopen("http://www.google.co.kr")  # package.module.function()
```
```py
reponse.status
```
- import package.module as name
```py
import urllib.request as r
```
```py
response = r.urlopen("http://www.google.co.kr")
response.status
```
- from package.module import variable
- from package.module import class
- from package.module import function
- from package.module import function, class, variable
```py
from urllib.request import urlopen

response = r.urlopen("http://www.google.co.kr")
response.status
```
- from package.module import *
```py
from urllib.request import *

response = r.urlopen("http://www.google.co.kr")
response.status
```
**나만의 모듈 만들어서 사용하기**
```py
import square2
```
```py
square2.base
```
```py
square2.square2(5)  # 2 ** 5를 계산
```
```py
from square2 import square2
```
```py
square2(10)
```
```py
import Person
```
```py
me = Person.Person("지우근", 25, "경기 파주")
me.greeting()
```
```py
%run hello2.py   # anaconda prompt에서 python hello2.py
```
```py
%run main.py
```
```py
%run test.py
```
```py
%run calc.py
```
```py
import calc
```
```py
calc.add(10, 20)
```
```py
calc.mul(500, 200)
```
```py
import calcpkg.operation
calcpkg.operation.add(10, 20)
```
```py
import calcpkg.geometry
calcpkg.geometry.triangle_area(10, 10)
```
```py
from calcpkg.operation import add, mul
```
```py
add(10, 20)
```
```py
mul(10, 20)
```
```py
from calcpkg.geometry import *
```
```py
triangle_area(10, 10)
```
```py
rectangle_area(10, 10)
```
