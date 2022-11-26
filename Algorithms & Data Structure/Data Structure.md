# 시간 복잡도 계산하기

**시간 복잡도 표기법**

- 빅-오(O(n)): 최악일 때의 연산 횟수를 나타낸 표기법

```python
# 1에서 100 사이의 무작위수를 찾아 출력
import random

findNumber = random.randrange(1, 101) # fineNumber

for i in range(1, 101):  # 1 ~ 100
    if i == findNumber:
        print(i)
        break

# 최선일 때 1 회
# 보통일 때 50회
# 최악일 때 100회: O(n)
```

```
98
```

```python
sum = 0
fact = 1

for i in range(10):
    sum += i

for j in range(1, 11):
    fact *= j

print(sum, fact)

# 시간 복잡도: O(2n) --> O(n)으로 간주
```

```
45 3628800
```

```python
array = [3, 5, 1, 2, 4]   # 5개의 데이터

for i in array:    # array에는 5개의 데이터
    for j in array:   # array에는 5개의 데이터
        temp = i * j
        print(temp)

# 시간 복잡도 --> O(n ** 2)
```

```
9
15
3
6
12
15
25
5
10
20
3
5
1
2
4
6
10
2
4
8
12
20
4
8
16
```

```python
# manatee1 = {"name": "cute", "age": 2, ....}       # 총 m개의 키
# manatee2 = {"name": "handsome", "age": 1, ....}   # 총 m개의 키
# manatee3 = {"name": "pretty", "age": 3, ....}     # 총 m개의 키
# manatees = [manatee1, manatee2, manatee3, ...]   # 총 n마리의 manatee를 저장하는 리스트
```

```python
def example1(manatees):
    for manatee in manatees: # n iterations
        print(manatee['name'])

# 시간 복잡도 --> O(n)

def example2(manatees):
    print(manatees[0]['name'])
    print(manatees[0]['age'])

# 시간 복잡도 --> O(2) --> O(1)

def example3(manatees):
    for manatee in manatees: # n iterations
        for manatee_property in manatee: # m iterations
            print(manatee_property, ": ", manatee[manatee_property])

# 시간 복잡도 --> O(n * m)

def example4(manatees):
    oldest_manatee = "No manatees here!"
    for manatee1 in manatees: # n iterations
        for manatee2 in manatees:# n iterations
            if manatee1['age'] < manatee2['age']:  
                oldest_manatee = manatee2['name']  # 1회 
            else:
                oldest_manatee = manatee1['name']  # 1회   중에 하나
    print(oldest_manatee)

# 시간 복잡도 --> 2 * n ** 2 --> O(n ** 2) or O(n ^ 2)
```
# 배열 응용문제

#### 숫자의 합 구하기

- 시간 제한 1초 | 난이도 브론즈 Ⅳ | 백준 온라인 저지 11720번
- N개의 숫자가 공백 없이 써 있다. 이 숫자를 모두 합해 출력하는 프로그램을 작성하시오.
  **입력**
- 1번째 줄에 숫자의 개수 N(1<=N<=100), 2번째 줄에 숫자 N개가 공백 없이 주어진다.
  **출력**
- 입력으로 주어진 숫자 N개가 합을 출력한다.

**이미지 다운로드 코드**

```
from IPython.display import Image
Image("그림이름.형식자", width = 600)
```

```python
sum = 0
l = []

a = input()
l = list(a)

for i in range(len(l)):
    sum += i

print(sum)
```

```
12512612
28
```

```python
n = int(input())
numbers = list(input())  # numbers = ['1', '0', '6', '7', '2', ...]

s = 0  # 합을 담을 그릇

for i in numbers:
    s = s + int(i)  # i: 1 -> 0 -> 6 -> 7 -> 2 ...
print(s)
```

```
12
124152562167
42
```

# 단순 연결 리스트

```python
class Node() :
    def __init__ (self) :
        self.data = None
        self.link = None

def printNodes(start) :
    current = start

    if current == None :
        return
    print(current.data, end = ' ')

    while current.link != None:
        current = current.link
        print(current.data, end = ' ')
    print()

def makeSimpleLinkedList(namePhone) :
    global memory, head, current, pre
    printNodes(head)
    node = Node()
    node.data = namePhone
    memory.append(node)

    if head == None : # 첫 번째 노드일 때
        head = node
        return

    if head.data[0] > namePhone[0] : # 첫 번째 노드보다 작을 때
        node.link = head
        head = node
        return

    # 중간 노드로 삽입하는 경우
    current = head
    while current.link != None :
        pre = current
        current = current.link
        if current.data[0] > namePhone[0]:
            pre.link = node
            node.link = current
            return

    # 삽입하는 노드가 가장 큰 경우
    current.link = node

## 전역 변수 선언 부분 ##
memory = []
head, current, pre = None, None, None
dataArray = [["지민", "010-1111-1111"], ["정국", "010-2222-2222"], ["뷔", "010-3333-3333"], ["슈가", "010-4444-4444"], ["진", "010-5555-5555"]]

## 메인 코드 부분 ##
if __name__ == "__main__" :
    for data in dataArray :   # 5 iterations: 지민 -> 정국 -> 뷔 -> 슈가 -> 진
        makeSimpleLinkedList(data)
    printNodes(head)
```

```
['지민', '010-1111-1111'] 
['정국', '010-2222-2222'] ['지민', '010-1111-1111'] 
['뷔', '010-3333-3333'] ['정국', '010-2222-2222'] ['지민', '010-1111-1111'] 
['뷔', '010-3333-3333'] ['슈가', '010-4444-4444'] ['정국', '010-2222-2222'] ['지민', '010-1111-1111'] 
['뷔', '010-3333-3333'] ['슈가', '010-4444-4444'] ['정국', '010-2222-2222'] ['지민', '010-1111-1111'] ['진', '010-5555-5555'] 
```

```python
# %load "(실습 4) 스택 일반.py"
## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False

def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False

def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        print("스택이 꽉 찼습니다.")
        return

    top += 1           # push 했으니 한층 더 쌓음
    stack[top]= data   # 그 탑에 데이터를 입력한 넣어줌    

def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None

    data = stack[top]     # 제일 위에 있는 데이터를 pop
    stack[top] = None     # 데이터를 꺼낸 자리엔 None이 입력되도록 함
    top -= 1              # 빼냈으니 top을 낮춤

    return data

def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    return stack[top]

## 전역 변수 선언 부분 ##
SIZE = int(input("스택의 크기를 입력하세요 ==> "))
stack = [ None for _ in range(SIZE) ]        # _ 는 None으로 채울 부분을 나타낸 것
top = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :        # 시작점이기 때문에 __main__
    select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")

    while (select != 'X' and select != 'x') :
        if select=='I' or select =='i' :
            data = input("입력할 데이터 ==> ")
            push(data)
            print("스택 상태 : ", stack)
        elif select=='E' or select =='e' :
            data = pop()
            print("추출된 데이터 ==> ", data)
            print("스택 상태 : ", stack)
        elif select=='V' or select =='v' :
            data = peek()
            print("확인된 데이터 ==> ", data)
            print("스택 상태 : ", stack)
        else :
            print("입력이 잘못됨")
        select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    print("프로그램 종료!")
```

```
스택의 크기를 입력하세요 ==> 2
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> i
입력할 데이터 ==> awdn
스택 상태 :  ['awdn', None]
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> i
입력할 데이터 ==> ajwdn
스택 상태 :  ['awdn', 'ajwdn']
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> e
추출된 데이터 ==>  ajwdn
스택 상태 :  ['awdn', 'ajwdn']
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> e
추출된 데이터 ==>  ajwdn
스택 상태 :  ['awdn', 'ajwdn']
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> x
프로그램 종료!
```

# 스택 응용

- 웹 서핑에서 이전 페이지 돌아가기

```python
import webbrowser
```

```python
webbrowser.open("http://naver.com")
```

```
True
```

```python
import webbrowser
import time

## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False

def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False

def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        print("스택이 꽉 찼습니다.")
        return

    top += 1
    stack[top] = data

def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None

    data = stack[top]
    stack[top] = None
    top -= 1
    return data

def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        print("스택이 비었습니다.")
        return None
    return stack[top]

## 전역 변수 선언 부분 ##
SIZE = 100
stack = [ None for _ in range(SIZE) ]
top = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :
    urls = [ 'naver.com', 'daum.net', 'nate.com']
    for url in urls :
        push(url)                             
        webbrowser.open('http://' + url)                                                    
        print(url, end = '-->')
        time.sleep(1)
    print("방문 종료")
    time.sleep(5)

    while True :
        url = pop()
        if url == None:
            break
        webbrowser.open('http://' + url)      
        print(url, end = '-->')    
        time.sleep(1)
    print("방문 종료")
```

```
naver.com-->daum.net-->nate.com-->방문 종료
nate.com-->daum.net-->naver.com-->스택이 비었습니다.
방문 종료
```

**헨젤과 그레텔**

- 헨젤과 그레텔이 돌을 떨어뜨리면서 숲으로 들어간다. 과자집에서 집으로 돌아갈 때는 떨어뜨린 순서와 반대로 돌을 주워야 한다. 스택을 이용해서 집으로 무사히 돌아가도록 하자

```python
import random

## 함수 선언 부분 ##
def isStackFull() :
    global SIZE, stack, top
    if (top >= SIZE-1) :
        return True
    else :
        return False

def isStackEmpty() :
    global SIZE, stack, top
    if (top == -1) :
        return True
    else :
        return False

def push(data) :
    global SIZE, stack, top
    if (isStackFull()) :
        return
    top += 1
    stack[top] = data

def pop() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        return None
    data = stack[top]
    stack[top] = None
    top -= 1
    return data

def peek() :
    global SIZE, stack, top
    if (isStackEmpty()) :
        return None
    return stack[top]

## 전역 변수 선언 부분 ##
SIZE = 10
stack = [ None for _ in range(SIZE) ]
top = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :
    stoneAry = ["빨강", "파랑", "초록", "노랑", "보라", "주황"]
    random.shuffle(stoneAry)
    print("과자집에 가는길 : ", end = ' ')

    for stone in stoneAry :
        push(stone)
        #TODO
        print(stone, "-->", end = ' ')
    print("과자집")
    print("우리집에 오는길 : ", end = ' ')

    while True :
        stone = pop()
        if stone == None:
            break
        #TODO
        print(stone, "-->", end = ' ')
    print("우리집")
```

```
과자집에 가는길 :  보라 --> 노랑 --> 파랑 --> 초록 --> 빨강 --> 주황 --> 과자집
우리집에 오는길 :  주황 --> 빨강 --> 초록 --> 파랑 --> 노랑 --> 보라 --> 우리집
```

# 큐

```python
## 함수 선언 부분 ##
def isQueueFull() :
    global SIZE, queue, front, rear
    if (rear == SIZE-1) :
        return True
    else :
        return False

def isQueueEmpty() :
    global SIZE, queue, front, rear
    if (front == rear) :
        return True
    else :
        return False

def enQueue(data) :
    global SIZE, queue, front, rear
    if (isQueueFull()) :
        print("큐가 꽉 찼습니다.")
        return

    # todo
    rear += 1
    queue[rear] = data

def deQueue() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None

    # todo
    front += 1
    data = queue[front]
    queue[front] = None
    return data

def peek() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    return queue[front+1]

## 전역 변수 선언 부분 ##
SIZE = int(input("큐의 크기를 입력하세요 ==> "))
queue = [ None for _ in range(SIZE) ]
front = rear = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :
    select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    while (select != 'X' and select != 'x') :
        if select=='I' or select =='i' :
            data = input("입력할 데이터 ==> ")
            enQueue(data)
            print("큐 상태 : ", queue)
        elif select=='E' or select =='e' :
            data = deQueue()
            print("추출된 데이터 ==> ", data)
            print("큐 상태 : ", queue)
        elif select=='V' or select =='v' :
            data = peek()
            print("확인된 데이터 ==> ", data)
            print("큐 상태 : ", queue)
        else :
            print("입력이 잘못됨")
        select = input("삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> ")
    print("프로그램 종료!")
```

```
큐의 크기를 입력하세요 ==> 2
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> i
입력할 데이터 ==> qwe
큐 상태 :  ['qwe', None]
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> i
입력할 데이터 ==> asd
큐 상태 :  ['qwe', 'asd']
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> e
추출된 데이터 ==>  qwe
큐 상태 :  [None, 'asd']
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> e
추출된 데이터 ==>  asd
큐 상태 :  [None, None]
삽입(I)/추출(E)/확인(V)/종료(X) 중 하나를 선택 ==> x
프로그램 종료!
```

```python
def isQueueFull() :
    global SIZE, queue, front, rear

    if (rear != SIZE-1) :
        return False
    elif (rear == SIZE -1) and (front == -1) :
        return True
    else :
        for i in range(front + 1, SIZE) :

            queue[i - 1] = queue[i]
            queue[i] = None

        front -= 1
        rear -= 1
        return False             #TODO


SIZE = 5
queue = [None, None, "문별", "휘인", "선미"]
front = 1
rear = 4
print("큐가 꽉 찼는지 여부 ==>", isQueueFull())
print("큐 상태 ==> ", queue)
# 흰색_확인_표시
# 두_눈
# 두_손을_들고_있는_사람
# 반응
# 댓글
```

```
큐가 꽉 찼는지 여부 ==> False
큐 상태 ==>  [None, '문별', '휘인', '선미', None]
```

# 큐 응용

**유명 맛집의 대기줄**

- 유명 맛집의 대기줄에는 손님들이 들어온 순서대로 줄을 선다.
  그리고 대기줄이 꽉 차면 더 이상 손님을 받지 않는다.
  이제 대기줄 손님들은 자리가 생기면 1명씩 식당으로 들어간다.
  맨 앞쪽 손님이 대기줄에서 식당으로 들어갈 때마다 대기줄 뒤쪽 손님들은 한 칸씩 이동해서 줄을 다시 서도록 한다.

```python
## 함수 선언 부분 ##
def isQueueFull() :
    global SIZE, queue, front, rear
    if (rear == SIZE-1) :
        return True
    else :
        return False

def isQueueEmpty() :
    global SIZE, queue, front, rear
    if (front == rear) :
        return True
    else :
        return False

def enQueue(data) :
    global SIZE, queue, front, rear
    if (isQueueFull()) :
        print("큐가 꽉 찼습니다.")
        return
    rear += 1
    queue[rear] = data

def deQueue() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    front += 1
    data = queue[front]
    queue[front] = None

    # 모든 사람을 한칸씩 앞으로 당기기
    # todo
    for i in range(front + 1, SIZE) :    # SiZE 대신 rear + 1로 해줘도 된다.
            queue[i - 1] = queue[i]
            queue[i] = None
    front -= 1
    rear -= 1

    return data

def peek() :
    global SIZE, queue, front, rear
    if (isQueueEmpty()) :
        print("큐가 비었습니다.")
        return None
    return queue[front+1]

## 전역 변수 선언 부분 ##
SIZE = 5
queue = [ None for _ in range(SIZE) ]
front = rear = -1

## 메인 코드 부분 ##
if __name__ == "__main__" :
    enQueue('정국')
    enQueue('뷔')
    enQueue('지민')
    enQueue('진')
    enQueue('슈가')
    print("대기 줄 상태 : ", queue)

    for _ in range(rear+1) :
        print(deQueue(), '님 식당에 들어감')
        print("대기 줄 상태 : ", queue)

    print("식당 영업 종료!")
```

```
대기 줄 상태 :  ['정국', '뷔', '지민', '진', '슈가']
정국 님 식당에 들어감
대기 줄 상태 :  ['뷔', '지민', '진', '슈가', None]
뷔 님 식당에 들어감
대기 줄 상태 :  ['지민', '진', '슈가', None, None]
지민 님 식당에 들어감
대기 줄 상태 :  ['진', '슈가', None, None, None]
진 님 식당에 들어감
대기 줄 상태 :  ['슈가', None, None, None, None]
슈가 님 식당에 들어감
대기 줄 상태 :  [None, None, None, None, None]
식당 영업 종료!
```
