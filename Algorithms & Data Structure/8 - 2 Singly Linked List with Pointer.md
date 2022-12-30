## 포인터로 연결 리스트 만들기

연결 리스트에 데이터를 삽입할 때 노드용 인스턴스를 생성하고, 데이터를 삭제할 때 노드용 인스턴스를 없애면 앞에서 제시한 데이터를 옮기는 문제를 해결할 수 있습니다.

Node는 데이터용 필드 data와는 별도로 자신과 같은 형의 인스턴스를 참조하는 필드가 있는 구조를 자기 참고(self-referential)형이라고 합니다.

여기에서 data는 데이터 자체가 아니라 **'데이터에 대한 참조'**이고 next는 **'노드에 대한 참조'**입니다.

```python
# 포인터로 연결 리스트 구현하기

from __future__ import annotations
from typing import Any, Type

class Node:
    """연결 리스트용 노드 클래스"""

    def __init__(self, data: Any = None, next: Node = None):
        """초기화"""
        self.data = data     # 데이터
        self.next = next     # 뒤쪽 포인터
```

- data: 데이터(데이터에 대한 참조: 임의의 형)
- next: 뒤쪽 포인터(뒤쪽 노드에 대한 참조: Node형)

__init__() 함수

__init__() 함수는 전달받은 data와 next를 해당 필드에 대입합니다. 호출할 때 어떤 인수도 생략할 수 있으며, 생략할 경우에는 None으로 간주합니다.

### 파이썬의 리스트는 자료구조가 아닙니다.

연결 리스트는 임의의 위치에 원소를 삽입하거나 삭제할 때 빠르게 수행할 수 있다는 장점이 있습니다. 하지만 기억 영역(메모리)과 속도 면에서는 배열보다 효율이 떨어집니다. <br>
파이썬의 리스트는 이러한 연결 리스트의 자료구조가 아니라 모든 원소를 연속으로 메모리에 배치하는 '배열'로 내부에서 구현하고 있습니다. 그러므로 속도가 급격히 떨어지지는 않습니다. 또 원소를 하나씩 추가, 삽입할 때마다 내부에서 메모리를 확보하거나 해제하지 않습니다. 실제 필요한 메모리보다 여유 있게 미리 마련해 놓기 때문입니다.

```python
class LinkedList:
    """연결 리스트 클래스"""

    def __init__(self) -> None:
        """초기화"""
        self.no = 0               # 노드의 개수
        self.head = None         # 머리 노드
        self.current = None      # 주목 노드

    def __len__(self) -> int:
        """연결 리스트의 노드 개수를 반환"""
        return self.no
```

- no: 리스트에 등록되어 있는 노드의 개수입니다.
  
- head: 머리 노드에 대한 참조입니다.
  
- current: 현재 주목하고 있는 노드에 대한 참조이며, 이 책에서는 주목 포인터라고 하겠습니다. 리스트에서 노드를 검색하여, 그 노드를 주목한 직후에 노드를 삭제하는 등의 용도로 사용합니다.
  
- 빈 연결 리스트 <br>
  

head is None

- 노드가 1개인 연결 리스트

head.next is None

- 노드가 2개인 연결 리스트

head.next.next is None

- 꼬리 노드의 판단

p.next is None

#### 노드를 스캔할 때 다음 조건 가운데 하나만 성립해도 검색이 종료됩니다.

- 종료 조건 1: 검색 조건을 만족하는 노드를 발견하지 못하고 꼬리 노드까지 왔을 경우
- 종료 조건 2: 검색 조건을 만족하는 노드를 발견한 경우

```python
    def search(self, data:Any) -> int:
        """data와 값이 같은 노드를 탐색"""
        cnt = 0
        ptr = self.head
        while ptr.data == data:                             # None이 나온다는 건 리스트가 끝났다는 것
            if ptr.data == data:                            # 발견하면 위치 반환
                self.current = ptr
                return cnt                                  # 발견하면 위치 반환
            cnt += 1
            ptr = ptr.next
        return -1                                           # 검색 실패

    def __contains__(self, data: Any) -> bool:
        """연결 리스트에 data가 포함되어 있는지 확인"""
        return self.search(data) >= 0                       # 검색 실패는 -1을 반환하기 때문에 찾으면 0 이상임

    def add_first(self, data: Any) -> None:
        """맨 앞에 노드를 삽입"""
        ptr = self.head   # 삽입하기 전의 머리 노드
        self.head = self.current = Node(data, ptr)          # 데이터를 미리 저장해둔 포인터에
        self.no += 1
```

#### 꼬리에 노드를 삽입하는 add_last() 함수

- 리스트가 비어있을 때

$ ~~~ $ 맨 앞에 노드를 삽입하는 것과 같은 처리를 수행하므로 add_first() 함수를 호출합니다.

- 리스트가 비어 있지 않을 때

$ ~~~ $ 리스트의 맨 끝에 노드 G를 삽입합니다.

```python
    def add_last(self, data: Any):
        """맨 끝에 노드를 삽입"""
        if self.head is None:            # 리스트가 비어 있으면
            self.add_first(data)          # 맨 앞에 노드를 삽입
        else:
            ptr = self.head
            while ptr.next is not None:
                ptr = ptr.next                               # 다음 자리를 찾아 이동 -> None에 도달했다는 건 꼬리에 왔다는 것
            ptr.next = self.current = Node(data, None)       # ptr.next: next가 다음으로 들어갈 데이터의 자리가 되도록
            self.no += 1

    def remove_first(self) -> None:
        """머리 노드를 삭제"""
        if self.head is not None:        # 리스트가 비어 있지 않다면
            self.head = self.current = self.head.next
        self.no -= 1                                         # 수만 감소시키면 된다.
```

#### 꼬리 노드를 삭제하는 remove_last() 함수

- 리스트에 노드가 하나만 존재할 때

$ ~~~ $ 머리 노드가 삭제하는 것이므로 remove_first() 함수를 호출합니다.

- 리스트에 노드가 2개 이상 존재할 때

$ ~~~ $ 리스트의 맨 끝에서 노드 F를 삭제합니다.

```python
    def remove_last(self):
        """꼬리 노드를 삭제"""
        if self.head is not None:               # 노드가 존재
            if self.head.next is None:          # 노드가 1개 뿐이라면
                self.remove_first()             # 머리 노드를 삭제
            else:
                ptr = self.head                 # 스캔 중인 노드
                pre = self.head                 # 스캔 중인 노드의 앞쪽 노드
 
                while ptr.next is not None:     # 꼬리에 도달할 때까지
                    pre = ptr              
                    ptr = ptr.next
                pre.next = None                 # pre는 삭제 뒤 꼬리 노드   # 데이터 삭제
                self.current = pre              # 주목시키고
                self.no -= 1                    # 삭제
```

#### 임의의 노드를 삭제하는 remove() 함수

- p가 머리 노드일 때

$ ~~~ $ 머리 노드를 삭제하는 것이므로 remove_first() 함수를 호출합니다.

- p가 머리 노드가 아닐 때

$ ~~~ $ 리스트에서 p가 참조하는 노드 D를 삭제합니다.

```python
    def remove(self, p: Node) -> None:
        """노드 p를 삭제"""
        if self.head is not None:                  # 머리 노드인지 아닌지
            if p is self.head:                     # p가 머리 노드이면
                self.remove_first()                # 머리 노드를 삭제
            else:
                ptr = self.head

                while ptr.next is not p:
                    ptr = ptr.next
                    if ptr is None:
                        return                     # ptr은 리스트에 존재하지 않음
                ptr.next = p.next                  # p의 노드를 ptr의 다음 참조 노드로 바꾸고
                self.current = ptr                 # 주목시키고
                self.no -= 1                       # 삭제

    def remove_current_node(self) -> None:
        """주목 노드를 삭제"""
        self.remove(self.current)

    def clear(self) -> None:
        """전체 노드를 삭제"""
        while self.head is not None:              # 전체가 비어 있을 때까지  # head가 None이라는 건 전체가 비어있다는 것
            self.remove_first()                   # 머리 노드를 삭제  # 머리 노드를 계속 삭제해서 clear 시켜버림
        self.current = None
        self.no = 0

    def next(self) -> bool:
        """주목 노드를 한 칸 뒤로 이동"""
        if self.current is None or self.current.next is None:        # 현재나 이동할 노드가 없다면 False
            return False                          # 이동할 수 없음
        self.current = self.current.next          # next로 옮겨줘서 update
        return True

    def print_current_node(self) -> None:
        """주목 노드를 출력"""
        if self.current is None:
            print('주목 노드가 존재하지 않습니다.')
        else:
            print(self.current.data)

    def print(self) -> None:
        """모든 노드를 출력"""
        ptr = self.head

        while ptr is not None:
            print(ptr.data)                       # 출력
            ptr = ptr.next                        # 계속 다음 노드로 update
```

| 실행한 함수 | current의 값 |
| --- | --- |
| __init__() | None |
| search() | 검색에 성공하면 발견할 수 있는 노드 |
| add_first() | 삽입한 머리 노드 |
| add_last() | 삽입한 꼬리 노드 |
| remove_first() | 삭제한 뒤 머리 노드(리스트가 비어 있으면 None) |
| remove_last() | 삭제한 뒤 꼬리 노드(리스트가 비어 있으면 None) |
| remove() | 삭제한 노드의 앞쪽 노드 |
| remove_current_node() | 삭제한 노드의 앞쪽 노드 |
| clear() | None |
| next() | 이동한 뒤 주목 노드 |
| print_current_node() | 업데이트하지 않음 |
| print() | 업데이트하지 않음 |

```python
    def __iter__(self) -> LinkedListIterator:
        """이터레이터를 반환"""
        return LinkedListIterator(self.head)

class LinkedListIterator:
    """클래스 LinkedList의 이터레이터용 클래스"""

    def __init__(self, head: Node):
        self.current = head

    def __iter__(self) -> LinkedListIterator:
        return self

    def __next__(self) -> Any:
        if self.current is None:
            raise StopIteration
        else:
            data = self.current.data
            self.current = self.current.next
            return data
```

### 이터러블 객체와 이터레이터의 구현

str형 문자열, list형 리스트, tuple형 튜플 등은 이터러블(반복 가능)하다는 공통점이 있습니다. <br>
이터러블 객체는 원소를 1개씩 꺼내는 구조의 객체입니다. 이터러블 객체를 내장 함수인 iter() 함수에 인수로 전달하면 그 객체에 대한 이터레이터(반복자)를 반환합니다. <br>
이터레이터는 데이터가 줄지어 늘어선 것을 표현하는 객체입니다. 이터레이터의 __next__() 함수를 호출하거나, 내장 함수인 next() 함수에 반복자를 전달하면 줄지어 늘어선 원소를 순차적으로 꺼냅니다. 꺼낼 원소가 없으면 StopIteration 예외 처리를 내보냅니다.

- __next__() 함수를 갖는 이터레이터를 반환하는 __iter__() 함수를 구현합니다.
- __next__() 함수는 다음 우너소를 꺼내 반환합니다. 반환하는 원소가 없으면 StopIteration 예외 처리를 내보냅니다.

## 포인터로 연결 리스트 프로그램 만들기

```python
# 포인터로 이용한 연결 리스트 클래스 LinkedList 사용하기

from enum import Enum
from linked_list import LinkedList

Menu = Enum('Menu', ['머리에노드삽입', '꼬리에노드삽입', '머리노드삭제',
                     '꼬리노드삭제', '주목노드출력', '주목노드이동',
                     '주목노드삭제', '모든노드삭제', '검색', '멤버십판단',
                     '모든노드출력', '스캔', '종료',])

def select_Menu() -> Menu:
    """메뉴 선택"""
    s = [f'({m.value}){m.name}' for m in Menu]
    while True:
        print(*s, sep='  ', end='')
        n = int(input(': '))
        if 1 <= n <= len(Menu):
            return Menu(n)


lst = LinkedList()  # 연결 리스트를 생성

while True:
    menu = select_Menu()  # 메뉴 선택

    if menu == Menu.머리에노드삽입:  # 맨 앞에 노드 삽입
        lst.add_first(int(input('머리에 넣을 값을 입력하세요.: ')))

    elif menu == Menu.꼬리에노드삽입:  # 맨 끝에 노드 삽입
        lst.add_last(int(input('꼬리에 넣을 값을 입력하세요.: ')))

    elif menu == Menu.머리노드삭제:  # 맨 앞 노드 삭제
        lst.remove_first()

    elif menu == Menu.꼬리노드삭제:  # 맨 끝 노드 삭제
        lst.remove_last()

    elif menu == Menu.주목노드출력:  # 주목 노드 출력
        lst.print_current_node()

    elif menu == Menu.주목노드이동:  # 주목 노드를 한 칸 뒤로 이동
        lst.next()

    elif menu == Menu.주목노드삭제:  # 주목 노드 삭제
        lst.remove_current_node()

    elif menu == Menu.모든노드삭제:  # 모든 노드를 삭제
        lst.clear()

    elif menu == Menu.검색:  # 노드를 검색
        pos = lst.search(int(input('검색할 값을 입력하세요.: ')))
        if pos >= 0:
            print(f'그 값의 데이터는 {pos + 1}번째에 있습니다.')
        else:
            print('해당 데이터가 없습니다.')

    elif menu == Menu.멤버십판단:  # 멤버십 판단
        print('그 값의 데이터는 포함되어' + (' 있습니다.' if int(input('멤버십 판단할 값을 입력하세요.: ')) in lst else ' 있지 않습니다.'))

    elif menu == Menu.모든노드출력:  # 모든 노드 출력
        lst.print()

    elif menu == Menu.스캔:  # 모든 노드 스캔
        for e in lst:
            print(e)

    else:  # 종료
        break
```
