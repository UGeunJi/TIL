# 해시법

해시법은 '데이터를 저장할 위치 = 인덱스'를 간단한 연산으로 구하는 것을 말합니다. 이 방법은 원소의 검색뿐 아니라 추가, 삭제도 효율적으로
수행할 수 있습니다.

## 해시 충돌

키와 해시값의 대응 관계가 꼭 1:1일 필요는 없습니다. 키와 해시값은 일반적으로 다대 1(n:1)입니다. 이처럼 저장할 버킷이 중복되는 현상을
충돌(collision)이라고 합니다.

이렇게 해시법에서 충돌이 발생하는 경우 다음 2가지 방법으로 대처할 수 있습니다.
- 체인법: 해시값이 같은 원소를 연결 리스트로 관리합니다.
- 오픈 주소법: 빈 버킷을 찾을 때까지 해시를 반복합니다.

### 체인법

체인법이란 해시값이 같은 데이터를 체인 모양의 연결 리스트로 연결하는 방법을 말하며 오픈 해시법(Open Hashing)이라고도 합니다.

# 체인법으로 해시 함수 구현하기
```py
from __future__ import annotations
from typing import Any, Type
import hashlib

class Node:                                             # 해시 충돌 시에도 사용
    """해시를 구성하는 노드"""
    
    
    def __init__(self, key: Any, value: Any, next: Node) -> None:
        """초기화"""
        self.key = key      # 키
        self.value = value  # 값
        self.next = next    # 뒤쪽 노드를 참조
```
#### Node 클래스 만들기

- key: 키(임의의 자료형)
- value: 값(임의의 자료형)
- next: 뒤쪽 노드를 참고(Node형)

Node 클래스는 키와 값이 짝을 이루는 구조입니다. 키에 해시 함수를 적용하여 해시값을 구합니다.
```py
class ChainedHash:
    """체인법으로 해시 클래스 구현"""
    
    
    def __init__(self, capacity: int) -> None:
        """초기화"""
        self.capacity = capacity               # 해시 테이블의 크기를 지정
        self.table = [None] * self.capacity   # 해시 테이블(리스트)을 선언
        
    
    def hash_value(self, key: Any) -> int:
        """해시값을 구함"""
        if isinstance(key, int):                           # isinstance(object, type)  object가 type이면 True, 아니면 False                       
            return key % self.capacity
        return(int(hashlib.sha256(str(key).encode()).hexdigest(), 16) % self.capacity)   
                                                           # False일 경우 이 행의 함수와 알고리즘을 통해 int형으로 변환
    
    def search(self, key: Any) -> Any:
        """키가 key인 원소를 검색하여 값을 반환"""
        hash = self.hash_value(key)             # 검색하는 키의 해시값              # 변환한 해시값
        p = self.table[hash]                    # 노드를 주목                       # 해시 테이블의 인덱스에 해당하는 값
        
        
        while p is not None:
            if p.key == key:
                return p.value                 # 검색 성공
            p = p.next                         # 뒤쪽 노드를 주목
            
        return None                           # 검색 실패
    
    
    def add(self, key: Any, value: Any) -> bool:
        """키가 key이고 value인 원소를 추가"""
        hash = self.hash_value(key)            # 추가하는 key의 해시값
        p = self.table[hash]                   # 노드를 주목                            # 추가하고자하는 자리: p
        
        
        while p is not None:                                                            # p가 비어있지 않으면
            if p.key == key:
                return False                  # 추가 실패
            p = p.next                         # 뒤쪽 노드를 주목                        # class Node에서 추가한 next (다음 노드)
            
        
        temp = Node(key, value, self.table[hash])                                       # 맨 앞에 노드 추가하고 입력 완료
        self.table[hash] = temp                # 노드를 추가
        return True                           # 추가 성공
    
    
    def remove(self, key: Any) -> bool:
        """키가 key인 원소를 삭제"""
        hash - self.hash_value(key)            # 삭제할 key의 해시값
        p = self.table[hash]                   # 노드를 주목
        pp = None                             # 바로 앞의 노드를 주목
        
        
        while p is not None:
            if p.key == key:                   # key를 발견하면 아래를 실행               
                if pp is None:
                    self.table[hash] = p.next                                            # 다음 노드로 연결해서 삭제
                else:
                    pp.next = p.next                                       # else문: 그 다음 노드도 다음 노드로 연결해서 삭제 
                return True                   # key 삭제 성공
            
            pp = p
            p = p.next                         # 뒤쪽 노드를 주목                     
        return False                          # 삭제 실패(key가 존재하지 않음)            # 없어서 뒤쪽 봤는데도 없어서 실패
    
    
    def dump(self) -> None:
        """해시 테이블을 덤프"""
        for i in range(self.capacity):
            p = self.table[i]
            print(i, end = '')
            while p is not None:
                print(f' -> {p.key} ({p.value})', end = '')
                p = p.next
            print()
```
#### ChainedHash 해시 클래스 만들기

- capacity: 해시 테이블의 크기(배열 table의 원소 수)를 나타냅니다.
- table: 해시 테이블을 저장하는 list형 배열을 나타냅니다.

---
- key가 int형인 경우 <br>
key를 해시의 크기 capacity로 나눈 나머지를 해시값으로 합니다.
<br>
<br>
- key가 int형이 아닌 경우 <br>
key가 정수가 아닌 경우 그 값으로는 바로 나눌 수 없습니다. 그래서 다음과 같은 표준 라이브러리로 형 변환을 해야 해시값을 얻을 수 있습니다.
다음은 앞에 코드에서 사용한 표준 라이브러리입니다.

---
- sha256 알고리즘: hashlib 모듈에서 제공하는 sha256은 RSA의 FIPS 알고리즘을 바탕으로 하며, 주어진 바이트(byte) 문자열의 해시값을 구하는 해시
알고리즘의 생성자(constructor)입니다. hashlib 모듈은 sha256 외에도 MD5 알고리즘인 md5 등 다양한 해시 알고리즘을 제공합니다.
<br>
<br>
- enconde() 함수: hashlib.sha256에는 바이트 문자열의 인수를 전달해야 합니다. 그래서 key를 str형 문자열로 변환한 뒤 그 문자열을
encode() 함수에 전달하여 바이트 문자열을 생성합니다.
<br>
<br>
- hexdigest() 함수: sha256 알고리즘에서 해시값을 16진수 문자열로 꺼냅니다.
<br>
<br>
- int() 함수: hexdigest() 함수로 꺼낸 문자열을 16진수 문자열로 하는 int형으로 변환합니다.

**return(int(hashlib.sha256(str(key).encode()).hexdigest(), 16) % self.capacity) 줄까지의 설명**

---

#### add() 함수가 원소를 추가하는 과정은 다음과 같이 정리할 수 있습니다.

1. 해시 함수를 사용하여 키를 해시값으로 변환합니다.
2. 해시값을 인덱스로 하는 버킷에 주목합니다.
3. 버킷이 참조하는 연결 리스트를 맨 앞부터 차례로 선형 검색을 합니다. 키와 같은 값이 발견되면 키가 이미 등록된 경우이므로 추가에
실패합니다. 원소의 맨 끝까지 발견되지 않으면 해시값인 리스트의 맨 앞에 노드를 추가합니다.

#### remove() 함수가 원소를 삭제하는 과정은 다음과 같이 정리할 수 있습니다.

1. 해시 함수를 사용하여 키를 해시값으로 변환합니다.
2. 해시값을 인덱스로 하는 버킷에 주목합니다.
3. 버킷이 참조하는 연결 리스트를 맨 앞부터 차례로 선형 검색합니다. 키와 같은 값이 발견되면 그 노드를 리스트에서 삭제합니다.
그렇지 않으면 삭제에 실패합니다.

#### 원소를 출력하는 dump() 함수

dump() 함수는 모든 원소를 덤프하는 것, 즉 해시 테이블의 내용을 한꺼번에 통째로 출력합니다.

# 체인법을 구현하는 해시 클래스 ChainedHash의 사용
```py
from enum import Enum                                                    # 출력을 위한 
from chained_hash import ChainedHash

Menu = Enum('Menu', ['추가', '삭제', '검색', '덤프', '종료'])    # 메뉴를 선언

def select_menu() -> Menu:
    """메뉴 선택"""
    s = [f'({m.value}){m.name}' for m in Menu]
    while True:
        print(*s, sep = '   ', end = '')
        n = int(input(': '))
        if 1 <= n <= len(Menu):
            return Menu(n)
        
        
hash = ChainedHash(13)         # 크기가 13인 해시 테이블을 생성

while True:
    menu = select_menu()       # 메뉴 선택
    
    
    if menu == Menu.추가:      # 추가
        key = int(input('추가할 키를 입력하세요.: '))
        val = input('추가할 값을 입력하세요.: ')
        if not hash.add(key, val):
            print('추가를 실패했습니다!')
            
            
    elif menu == Menu.삭제:    # 삭제
        key = int(input('삭제할 키를 입력하세요.: '))
        val = input('삭제할 값을 입력하세요.: ')
        if not hash.remove(key, val):
            print('삭제를 실패했습니다!')
            
    
    elif menu == Menu.삭제:    # 삭제
        key = int(input('삭제할 키를 입력하세요.: '))
        if not hash.remove(key):
            print('삭제를 실패했습니다!')
            
    
    elif menu == Menu.검색:    # 검색
        key = int(input('검색할 키를 입력하세요.: '))
        t = hash.search(key)
        if t is not None:
            print('검색한 키를 갖는 값은 {t}입니다.')
        else:               # t is None
            print('검색할 데이터가 없습니다.')
            
            
    elif menu == Menu.덤프:   # 덤프
        hash.dump()
        
        
    else:                     # 종료
        break
```
# 오픈 주소법

해시 충돌이 발생할 때 해결하는 또 다른 방법으로 오픈 주소법이 있습니다.
오픈 주소법은 충돌이 발생했을 때 재해시(rehashing)를 수행하여 빈 버킷을 찾는 방법을 말하며 닫힌 해시법(closedhashing)이라고도 합니다.
```py
# Do it! 실습 3-7 오픈 주소법으로 해시함수 구현하기

from __future__ import annotations
from typing import Any, Type
from enum import Enum
import hashlib

# 버킷의 속성
class Status(Enum):                                        # 상태에 따라 재해시를 해야 하므로 상태 class 설정
    OCCUPIED = 0  # 데이터를 저장
    EMPTY = 1     # 비어 있음
    DELETED = 2   # 삭제 완료

class Bucket:
    """해시를 구성하는 버킷"""

    def __init__(self, key: Any = None, value: Any = None,
                       stat: Status = Status.EMPTY) -> None:
        """초기화"""
        self.key = key      # 키
        self.value = value  # 값
        self.stat = stat    # 속성

    def set(self, key: Any, value: Any, stat: Status) -> None:
        """모든 필드에 값을 설정"""
        self.key = key      # 키
        self.value = value  # 값
        self.stat = stat    # 속성

    def set_status(self, stat: Status) -> None:
        """속성을 설정"""
        self.stat = stat

class OpenHash:
    """오픈 주소법을 구현하는 해시 클래스"""

    def __init__(self, capacity: int) -> None:
        """초기화"""
        self.capacity = capacity                 # 해시 테이블의 크기를 지정
        self.table = [Bucket()] * self.capacity  # 해시 테이블

    def hash_value(self, key: Any) -> int:
        """해시값을 구함"""
        if isinstance(key, int):
            return key % self.capacity
        return(int(hashlib.md5(str(key).encode()).hexdigest(), 16)
                % self.capacity)

    def rehash_value(self, key: Any) -> int:
        """재해시값을 구함"""
        return(self.hash_value(key) + 1) % self.capacity                    # 재해시니까 원래 +1 한 값의 나머지

    def search_node(self, key: Any) -> Any:
        """키가 key인 버킷을 검색"""
        hash = self.hash_value(key)  # 검색하는 키의 해시값
        p = self.table[hash]         # 버킷을 주목

        for i in range(self.capacity):
            if p.stat == Status.EMPTY:                                      # 비어있으면 멈추고
                break
            elif p.stat == Status.OCCUPIED and p.key == key:                # 상태가 차있고 찾는 키였다면 채우기
                return p
            hash = self.rehash_value(hash)  # 재해시
            p = self.table[hash]
        return None

    def search(self, key: Any) -> Any:
        """키가 key인 갖는 원소를 검색하여 값을 반환"""
        p = self.search_node(key)
        if p is not None:
            return p.value  # 검색 성공
        else:
            return None     # 검색 실패

    def add(self, key: Any, value: Any) -> bool:
        """키가 key이고 값이 value인 요소를 추가"""
        if self.search(key) is not None:
            return False             # 이미 등록된 키                         # 먼저 키 검색해서 상태 확인 (없는 키라면 진행)

        hash = self.hash_value(key)  # 추가하는 키의 해시값
        p = self.table[hash]         # 버킷을 주목
        for i in range(self.capacity):
            if p.stat == Status.EMPTY or p.stat == Status.DELETED:            # 비어있거나 삭제되어 있으면
                self.table[hash] = Bucket(key, value, Status.OCCUPIED)
                return True
            hash = self.rehash_value(hash)  # 재해시                          # 차있으면 재해시
            p = self.table[hash]
        return False                        # 해시 테이블이 가득 참           # 끝까지 가득 차있으면 False return

    def remove(self, key: Any) -> int:
        """키가 key인 갖는 요소를 삭제"""
        p = self.search_node(key)  # 버킷을 주목
        if p is None:
            return False           # 이 키는 등록되어 있지 않음                # 찾아야 삭제하는데 None 값임
        p.set_status(Status.DELETED)                                          # None이 아니라면 삭제로 상태 변경
        return True

    def dump(self) -> None:
        """해시 테이블을 덤프"""
        for i in range(self.capacity):
            print(f'{i:2} ', end='')
            if self.table[i].stat == Status.OCCUPIED:
                print(f'{self.table[i].key} ({self.table[i].value})')
            elif self.table[i].stat == Status.EMPTY:
                print('-- 미등록 --')
            elif self.table[i] .stat == Status.DELETED:
                print('-- 삭제 완료 --')
```
# [Do it! 실습 3-8] 오픈 주소법을 구현하는 해시 클래스 OpenHash 사용
```py
from enum import Enum                                                   # 출력을 위한 코드
from open_hash import OpenHash

Menu = Enum('Menu', ['추가', '삭제', '검색', '덤프', '종료'])

def select_menu() -> Menu:
    """메뉴 선택"""
    s = [f'({m.value}){m.name}' for m in Menu]
    while True:
        print(*s, sep = '  ', end='')
        n = int(input(': '))
        if 1 <=  n <= len(Menu):
            return Menu(n)

hash = OpenHash(13)  # 크기가 13인 해시 테이블 생성

while True:
    menu = select_menu()  # 메뉴 선택

    if menu == Menu.추가:  # 추가
        key = int(input('추가할 키를 입력하세요.: '))
        val = input('추가할 값을 입력하세요.: ')
        if not hash.add(key, val):
            print('추가를 실패했습니다!')

    elif menu == Menu.삭제:  # 삭제
        key = int(input('삭제할 키를 입력하세요.: '))
        if not hash.remove(key):
            print('삭제를 실패했습니다!')

    elif menu == Menu.검색:  # 검색
        key = int(input('검색할 키를 입력하세요.: '))
        t = hash.search(key)
        if t is not None:
            print(f'검색한 키를 갖는 값은 {t}입니다.')
        else:
            print('검색할 데이터가 없습니다.')

    elif menu == Menu.덤프:  # 덤프
        hash.dump()

    else:  # 종료
        break
```
- 체인법: 해시값이 같은 (1 수연)과 (14, 민서)를 연결하는 연결 리스트가 버킷 1에 연결되어 있습니다.
- 오픈 주소법: 나중에 추가한 (14, 민서)는 재해시 결과 버킷 2에는 등록되어 있습니다. 또 데이터를 삭제한 뒤 버킷 2는 삭제 완료 속성이 들어 있습니다.
