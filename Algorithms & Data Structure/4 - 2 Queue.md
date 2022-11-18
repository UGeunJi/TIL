큐는 선입선출(First in First out) 구조입니다.

- 인큐(enque): 데이터를 추가하는 작업
- 디큐(deque): 데이터를 꺼내는 작업
- 프런트(front): 데이터를 꺼내는 쪽
- 리어(rear): 데이터를 넣는 쪽

### 우선순위 큐

우선순위 큐(priority queue)는 인큐할 때 데이터에 우선순위를 부여하여 추가하고, 디큐할 때 우선순위가 가장 높은 데이터를 꺼내는 방식입니다. 파이썬에서 우선순위를 부여하는 큐는 heapq 모듈에서 제공합니다. heap에서 data의 인큐는 heapq.heappush(heap, data)로 수행하고, 디큐는 heapq.heappop(head)으로 수행합니다. heapq 모듈을 사용한 프로그램은 6장에서 다룹니다.

## 링 버퍼로 큐 구현하기

디큐할 때 배열 안으로 원소를 옮기지 않는 큐를 구현하겠습니다. 이럴 때 사용하는 자료구조가 링 버퍼(ring buffer)입니다. 링 버퍼는 배열
맨 끝의 원소 뒤에 맨 앞의 원소가 연결되는 자료구조입니다. 어떤 원소가 맨 앞 원소이고, 어떤 원소가 맨 끝 원소인지 식별하는 변수가 각각
front와 rear입니다. 여기에서 front와 rear는 논리적인 데이터 순서일 뿐 배열의 물리적 원소의 순서는 아닙니다.
모든 처리의 시간 복잡도는 O(1)입니다.

```py
# 고정 길이 큐 클래스 FixedQueue 구현하기

from typing import Any

class FixedQueue:
    
    class Empty(Exception):
        """비어 있는 FixedQueue에서 디큐 또는 피크할 때 내보내는 예외 처리"""
        pass
    
    class Full(Exception):
        """가득 차 있는 FixedQueue에서 인큐할 때 내보내는 예외 처리"""
        pass
    
    def __init__(self, capacity: int) -> None:
        """큐 초기화"""
        self.no = 0                     # 현재 데이터 개수
        self.front = 0                  # 맨 앞 원소 커서
        self.rear = 0                   # 맨 뒤 원소 커서
        self.capacity = capacity        # 큐의 크기
        self.que = [None] * capacity    # 큐의 본체
        
    def __len__(self) -> int:
        """큐에 있는 모든 데이터 개수를 반환"""
        return self.no
    
    def is_empty(self) -> bool:
        """큐가 비어 있는지 판단"""
        return self.no <= 0
    
    def is_full(self) -> bool:
        """큐가 가득 차 있는지 판단"""
        return self.no >= self.capacity
    
    def enque(self, x: Any) -> None:
        """데이터 x를 인큐"""
        if self.is_full():
            raise FixedQueue.Full   # 큐가 가득 차 있는 경우 예외 처리 발생
        self.que[self.rear] = x
        self.rear += 1               # rear에 추가하고 + 1
        self.no += 1                 # 전체 개수에도 + 1
        if self.rear == self.capacity:       # rear가 배열의 최대크기인 capacity에 도달했을 때 
            self.rear = 0                                                       # 0으로 설정해줌으로써 링 버퍼로 동작
    
    def deque(self) -> Any:
        """데이터를 디큐"""
        if self.is_empty():
            raise FixedQueue.Empty   # 큐가 비어 있는 경우 예외 처리 발생
        x = self.que[self.front]
        self.front += 1                      # front를 더해줌으로써 하나를 없애버림
        self.no -= 1                         # 전체 개수에서 하나 줆
        if self.front == self.capacity:      # rear와 같이 front가 capacity에 도달하면 
            self.front = 0                                                    # 0으로 설정해줌으로써 링 버퍼로 동작
        return x
    
    def peek(self) -> Any:
        """큐에서 데이터를 피크(맨 앞 데이터를 들여다봄)"""
        if self.is_empty():
            raise FixedQueue.Empty         # 큐가 비어 있는 경우 예외 처리 발생
        return self.que[self.front]        # 안 비어 있다면 제일 앞에 있는 front 값 반환
    
    def find(self, value: Any) -> Any:
        """큐에서 value를 찾아 인덱스를 반환(없으면 -1을 반환)"""
        for i in range(self.no):
            idx = (i + self.front) % self.capacity          # i는 0부터 시작
            if self.que[idx] == value:    # 검색 성공
                return idx
        return -1                        # 검색 실패 
    
    def count(self, value: Any) -> bool:
        """큐에 있는 value의 개수를 반환"""
        c = 0
        for i in range(self.no):          # 큐 데이터를 선형 검색      # 전체 개수까지 반복
            idx = (i + self.front) % self.capacity          # i는 0부터 시작
            if self.que[idx] == value:    # 검색 성공                  # 발견되면 + 1 해주고 동작
                c += 1                    # 들어 있음
        return c
    
    def __contains__(self, value: Any) -> bool:
        """큐에 value가 있는지 판단"""
        return self.count(value)
    
    def clear(self) -> None:
        """큐의 모든 데이터를 비움"""
        self.no = self.front = self.rear = 0                           # 개수, 앞, 뒤 모두 0으로 설정
        
    def dump(self) -> None:
        """모든 데이터를 맨 앞부터 맨 끝 순으로 출력"""
        if self.is_empty():
            print('큐가 비었습니다.')
        else:                                  
            for i in range(self.no):
                print(self.que[(i + self.front) % self.capacity], end = '')# find() 함수에서 쓰는 코드와 동일. 찾는대로 출력
            print()
```

- que: 큐의 배열로써 밀어 넣는 데이터를 저장하는 list형 배열입니다.
- capacity: 큐의 최대 크기를 나타내는 int형 정수입니다. 이 값은 배열 que의 원소 수와 일치합니다.
- front, rear: 맨 앞의 원소, 맨 끝의 원소를 나타내는 인덱스입니다. 큐에 넣은 데이터 중에 가장 처음에 넣은 맨 앞 원소의 인덱스가
front이고, 가장 마지막에 넣은 맨 끝 원소의 바로 다음 인덱스가 rear입니다. rear는 다음에 인큐할 때 데이터를 저장하는 원소의 인덱스입니다.
- no: 큐에 쌓여 있는 데이터 개수를 나타내는 int형 정수입니다. 변수 front와 rear의 값이 같은 경우 큐가 비어 있는지 또는 가득 차 있는지
구별하기 위해 필요합니다. 큐가 비어 있는 경우에는 no가 0이 되고, 가득 차 있는 경우에는 capacity와 같은 값이 됩니다.

#### 양방향 대기열 덱의 구조

양방향 대기열인 덱은 맨 앞과 맨 끝 양쪽에서 데이터를 넣고 꺼낼 수 있는 자료구조입니다. 파이썬에서는 collections.deque 컨테이너로 제공됩니다.

![image](https://user-images.githubusercontent.com/84713532/202594289-b039fd9a-9021-41a2-96e0-d0c089b2c5a0.png)

#### 덱이란?

덱(deque: double-ended queue)은 맨 앞과 맨 끝 양쪽에서 데이터를 모두 삽입, 삭제할 수 있는 자료 구조입니다. 2개의 포인터를 사용하여
양쪽에서 삭제, 삽입을 할 수 있으며, 큐와 스택을 합친 형태라고 생각하면 됩니다.

```py
# 고정 길이 큐 클래스(FixedQueue)를 사용하기

from enum import Enum
from fixed_queue import FixedQueue

Menu = Enum('Menu', ['인큐', '디큐', '피크', '검색', '덤프', '종료'])

def select_menu() -> Menu:
    """메뉴 선택"""
    s = [f'({m.value}){m.name}' for m in Menu]
    while True:
        n = int(input(': '))
        if 1 <= n <= len(Menu):
            return Menu(n)

q = FixedQueue(64)  # 최대 64개를 인큐할 수 있는 큐 생성(고정 길이)

while True:
    menu = select_menu()   # 메뉴 선택

    if menu == Menu.인큐:  # 인큐
        x = int(input())
        try:
            q.enque(x)
        except FixedQueue.Full:
            

    elif menu == Menu.디큐:  # 디큐
        try:
            x = q.deque()
            print()
        except FixedQueue.Empty:
            print()

    elif menu == Menu.피크:  # 피크
        try:
            x = q.peek()
            print()
        except FixedQueue.Empty:
            print()

    elif menu == Menu.검색:  # 검색
        x = int(input())
        if x in q:
            print()
        else:
            print()

    elif menu == Menu.덤프:  # 덤프
        q.dump()
    else:
        break
```

---

```py
# 원하는 개수(n)만큼 값을 입력받아 마지막 n개를 저장

n = int(input('정수를 몇 개 저장할까요?: '))    # 크기 지정
a = [None] * n                # 입력받은 값을 저장하는 배열

cnt = 0                       # 정수를 입력받은 개수
while True:
    a[cnt % n] = int(input((f'{cnt + 1}번째 정수를 입력하세요.: ')))   # cnt + 1 -> 다음 큐에 값 입력
    cnt += 1
    
    retry = input(f'계속 할까요?(Y ... Yes / N ... No): ')
    if retry in {'N', 'n'}:
        break
        
i = cnt - n                     # cnt, 즉, 입력된 횟수가 배열값을 초과했을 때 i가 양수
if i < 0: i = 0                 # i가 음수면 0으로 처리
    
while i < cnt:
    print(f'{i + 1}번째 = {a[i % n]}') i가 cnt - 1까지 반복. a배열에 반복적으로 입력
    i += 1
```
