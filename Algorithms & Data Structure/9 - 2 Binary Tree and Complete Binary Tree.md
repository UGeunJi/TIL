## 이진 트리 알아보기

노드가 왼쪽 자식(left child)과 오른쪽 자식(right child)만을 갖는 트리를 이진 트리(binary tree)라고 합니다. 이때 두 자식 가운데 하나 또는 둘 다 존재하지 않는 노드가 있어도 상관없습니다.

이진 트리의 특징은 왼쪽 자식과 오른쪽 자식을 구분한다는 점입니다. 또 왼쪽 자식을 루트로 하는 서브트리를 왼쪽 서브트리라 하고, 오른쪽 자식을 루트로 하는 서브트리를 오른쪽 서브트리라고 합니다.

## 완전 이진 트리 알아보기

루트부터 아래쪽 레벨로 노드가 가득 차 있고, 같은 레벨 안에서 왼쪽부터 오른쪽으로 노드가 채워져 있는 이진 트리를 완전 이진 트리(complete binary tree)라고 합니다.

#### 완전 이진 트리 노드를 채우는 방법

- 마지막 레벨을 제외하고 모든 레벨에 노드가 가득 차 있습니다.
- 마지막 레벨에 한해서 왼쪽부터 오른쪽으로 노드를 채우되 반드시 끝까지 채우지 않아도 됩니다.

## 이진 검색 트리 알아보기

이진 검색 트리는 모든 노드가 다음 조건을 만족해야 합니다.

- 왼쪽 서브트리 노드의 키값은 자신의 노드 키값보다 작아야 합니다.
- 오른쪽 서브트리 노드의 키값은 자신의 노드 키값보다 커야 합니다.

이진 검색 트리는 다음과 같은 특징이 있어서 알고리즘에서 폭 넓게 사용되고 있습니다.

- 구조가 단순합니다.
- 중위 순회의 깊이 우선 검색을 통하여 노드값을 오름차순으로 얻을 수 있습니다.
- 이진 검색과 비슷한 방식으로 아주 빠르게 검색할 수 있습니다.
- 노드를 삽입하기 쉽습니다.

## 이진 검색 트리 만들기

### 노드 클래스 Node

이진 검색 트리의 노드를 나타내는 클래스 Node입니다. 이진 검색 트리는 다음 4개의 필드로 구성됩니다.

- key: 키(임의의 형)를 나타냅니다.
- value: 값(임의의 형)을 나타냅니다.
- left: 왼쪽 자식 노드에 대한 참조(왼쪽 포인터)를 나타냅니다.
- right: 오른쪽 자식 노드에 대한 참조(오른쪽 포인터)를 나타냅니다.

```python
# 이진 검색 트리 구현하기

from __future__ import annotations
from typing import Any, Type

class Node:
    """이진 검색 트리의 노드"""
    def __init__(self, key: Any, value: Any, left: Node = None, right: Node = None):
        """생성자(constructor)"""
        self.key = key       # 키
        self.value = value   # 값
        self.left = left     # 왼쪽 포인터
        self.right = right   # 오른쪽 포인터

class BinarySearchTree:
    """이진 검색 트리"""

    def __init__(self):
        """초기화"""
        self.root = None     # 루트
```

### 이진 탐색 트리 클래스 BinarySearchTree

이진 검색 트리를 나타내는 클래스 BinarySearchTree입니다. 이 클래스의 유일한 필드는 루트에 대한 참조를 유지하는 root입니다. 클래스 BinarySearchTree의 __init__() 함수는 root에 None을 대입하여 노드가 하나도 없는 빈 상태의 이진 검색 트리를 생성합니다.

### 키값으로 노드를 검색하는 search() 함수

````
1. 루트에 주목합니다. 여기서 주목하는 노드를 p라고 하겠습니다.
2. p가 None이면 검색을 실패하고 종료합니다.
3. 검색하는 key와 주목 노드 p의 키를 비교합니다.
- key = p: 검색을 성공하고 종료합니다.
- key < p: 주목 노드를 왼쪽 자식 노드로 옮깁니다.
- key > p: 주목 노드를 오른쪽 자식 노드로 옮깁니다.
4. 2번 과정으로 돌아갑니다.


```python
    def search(self, key: Any) -> Any:
        """키가 key인 노드를 검색"""
        p = self.root                    # 루트에 주목
        while True:
            if p is None:                # 더 이상 진행할 수 없으면
                return None              # 검색 실패
            if key == p.key:             # key와 노드 p의 키가 같으면
                return p.value           # 검색 성공
            elif key < p.key:            # key 쪽이 작으면
                p = p.left               # 왼쪽 서브트리에서 검색
            else:                        # key 쪽이 크면
                p = p.right              # 오른쪽 서브트리에서 검색 
````

### 노드를 삽입하는 add() 함수

1. 루트에 주목합니다. 여기서 주목하는 노드를 node라고 하겠습니다.
2. 삽입하는 key와 주목 노드 node의 키를 비교합니다.

- key = node인 경우: 삽입을 실패하고 종료합니다.
- key < node인 경우:
  - 왼쪽 자식 노드가 없으면 그 자리에 노드를 삽입하고 종료합니다.
  - 왼쪽 자식 노드가 있으면, 주목 노드를 왼쪽 자식 노드로 옮깁니다.
- key > node:
  - 오른쪽 자식 노드가 없으면, 그 자리에 노드를 삽입하고 종료합니다.
  - 오른쪽 자식 노드가 있으면, 주목 노드를 오른쪽 자식 노드로 옮깁니다.

3. 2번 과정으로 되돌아갑니다.

```python
    def add(self, key: Any, value: Any) -> bool:
        """키가 key이고 값이 value인 노드를 삽입"""

        def add_node(node: Node, key: Any, value: Any) -> None:
            """node를 루트로 하는 서브트리에 키가 key이고 값이 value인 노드를 삽입"""
            if key == node.key:     # 중복 X
                return False   # key가 이진 검색 트리에 이미 존재
            elif key < node.key:
                if node.left is None:
                    node.left = Node(key, value, None, None)
                else:
                    add_node(node.left, key, value)  # 재귀
            else:
                if node.right is None:
                    node.right = Node(key, value, None, None)
                else:
                    add_node(node.right, key, value)   # 재귀
            return True

            if self.root is None:     # root가 비어있으면 root로
                self.root = Node(key, value, None, None)
                return True
            else:
                return add_node(self.root, key, value)
```

### 노드를 삭제하는 remove() 함수

A: 자식 노드가 없는 노드를 삭제하는 경우

- 삭제할 노드가 부모 노드의 왼쪽 자식이면, 부모의 왼쪽 포인터를 None으로 합니다.
- 삭제할 노드가 부모 노드의 오른쪽 자식이면, 부모의 오른쪽 포인터를 None으로 합니다.

B: 자식 노드가 1개인 노드를 삭제하는 경우

- 삭제할 노드가 부모 노드의 왼쪽 자식인 경우: 부모의 왼쪽 포인터가 삭제할 노드의 자식을 가리키도록 업데이트합니다.
- 삭제할 노드가 부모 노드의 오른쪽 자식인 경우: 부모의 오른쪽 포인터가 삭제할 노드의 자식을 가리키도록 업데이트합니다.

C: 자식 노드가 2개인 노드를 삭제하는 경우

1. 삭제할 노드의 왼쪽 서브트리에서 키값이 가장 큰 노드를 검색합니다.
2. 검색한 노드를 삭제 위치로 옮깁니다. 즉, 검색한 노드의 데이터를 삭제할 노드 위치에 복사합니다.
3. 옮긴 노드를 삭제합니다. 이때 자식 노드의 개수에 따라 다음을 수행합니다.
  - 옮긴 노드에 자식이 없으면 A: '자식 노드가 없는 노드의 삭제'에 따라 노드를 삭제합니다.
  - 옮긴 노드에 자식이 1개만 있으면 B: '자식 노드가 1개인 노드의 삭제'에 따라 노드를 삭제합니다.

```python
    def remove(self, key: Any) -> bool:
        """키가 key인 노드를 삭제"""
        p = self.root                          # 스캔 중인 노드
        parent = None                          # 스캔 중인 노드의 부모 노드
        is_left_child = True                   # p는 parent의 왼쪽 자식 노드인지 확인

        while True:
            if p is None:                      # 더 이상 진행할 수 없으면
                return False                   # 그 키는 존재하지 않음

            if key == p.key:                   # key와 노드 p의 키가 같으면
                break                          # 검색 성공
            else:
                parent = p                     # 가지를 내려가기 전에 부모를 설정
                if key < p.key:                # key 쪽이 작으면   # left
                    is_left_child = True       # 여기서 내려가는 것은 왼쪽 자식
                    p = p.left                 # 왼쪽 서브트리에서 검색
                else:                          # key 쪽이 크면     # right
                    is_left_child = False      # 여기서 내려가는 것은 오른쪽 자식
                    p = p. right               # 오른쪽 서브트리에서 검색

        if p.left is None:                     # p에 왼쪽 자식이 없으면        # 자식 노드가 없는 경우와 1개인 노드
            if p is self.root:
                self. root = p.right           # p가 root이면
            elif is_left_child:                # is_left_child = True
                parent.left = p.right          # 부모의 왼쪽 포인터가 오른쪽 자식을 가리킴
            else:
                parent.right = p.right         # 부모의 오른쪽 포인터가 오른쪽 자식을 가리킴
        elif p.right is None:                  # p에 오른쪽 자식이 없으면
            if p is self.root:
                self.root = p.left
            elif is_left_child:
                parent.left = p.left           # 부모의 왼쪽 포인터가 왼쪽 자식을 가리킴
            else:
                parent.right = p.left          # 부모의 오른쪽 포인터가 왼쪽 자식을 가리킴
        else:                                                                 # 자식 노드가 2개인 경우
            parent = p
            left = p.left                      # 서브트리 안에서 가장 큰 노드
            is_left_child = True
            while left.right is not None:      # 가장 큰 노드 left를 검색
                parent = left
                left = left.right              # 양쪽 탐색
                is_left_child = False

            p.key = left.key                   # left의 키를 p로 이동
            p.value = left.value               # left의 데이터를 p로 이동
            if is_left_child:
                parent.left = left.left        # left를 삭제
            else:
                parent.right = left.left       # left를 삭제
        return True
```

### 모든 노드를 오름차순으로 출력하는 dump() 함수

모든 노드를 키의 오름차순으로 출력하는 함수입니다. 스캔은 중위 순회의 깊이 우선 검색으로 합니다.

```python
    def dump(self) -> None:
        """덤프(모든 노드를 키의 오름차순으로 출력)"""

        def print_subtree(node: Node):
            """node를 루트로 하는 서브트리의 노드를 키의 오름차순으로 출력"""
            if node is not None:
                print_subtree(node.left)              # 왼쪽 서브트리를 오름차순으로 출력
                print(f'{node.key} {node.value}')     # node를 출력 
                print_subtree(node.right)             # 오른쪽 서브트리를 오름차순으로 출력

        print_subtree(self.node)
```

### 최소 키와 최대 키를 반환하는 min_key() 함수와 max_key() 함수

```python
    def min_key(self) -> Any:
        """가장 작은 키"""
        if self.root is None:
            return None
        p = self.root
        while p.left is not None:
            p = p.left
            return p.key

        def max_key(self) -> Any:
            """가장 큰 키"""
            if self.root is None:
                return None
            p = self.root
            while p.right is not None:
                p = p.right
            return p.key
```

### 보충수업 키의 내림차순으로 덤프

```python
# 이진 검색 트리의 구현(키를 내림차순으로 덤프)

from __future__ import annotations
from typing import Any, Type

class Node:
    """이진검색트리의 노드"""
    def __init__(self, key: Any, value: Any, left: Node = None,
                 right: Node = None):
        """생성자"""
        self.key = key          # 키
        self.value = value      # 값
        self.left = left        # 왼쪽 포인터(왼쪽 자식에 대한 참조)
        self.right = right      # 오른쪽 포인터(오른쪽 자식에 대한 참조)

class BinarySearchTree:
    """이진검색트리"""

    def __init__(self):
        """초기화"""
        self.root = None        # 루트

    def search(self, key: Any) -> Any:
        """키 key를 갖는 노드를 검색"""
        p = self.root # 루트에 주목
        while True:
            if p is None:                       # 더 이상 진행할 수 없으면
                return None                     # ... 검색 실패
            if key == p.key:                    # key와 노드 p의 키가 같으면
                return p.value                  # ... 검색 성공
            elif key < p.key:                   # key 쪽이 작으면
                p = p.left                      # ... 왼쪽 서브 트리에서 검색
            else:                               # key 쪽이 크면
                p = p.right                     # ... 오른쪽 서브 트리에서 검색

    def add(self, key: Any, value: Any) -> bool:
        """키가 key이고, 값이 value인 노드를 삽입"""

        def add_node(node: Node, key: Any, value: Any) -> None:
            """node를 루트로 하는 서브 트리에 키가 key이고, 값이 value인 노드를 삽입"""
            if key == node.key:
                return False # key가 이진검색트리에 이미 존재
            elif key < node.key:
                if node.left is None:
                    node.left = Node(key, value, None, None)
                else:
                    add_node(node.left, key, value)
            else:
                if node.right is None:
                    node.right = Node(key, value, None, None)
                else:
                    add_node(node.right, key, value)
            return True

        if self.root is None:
            self.root = Node(key, value, None, None)
            return True

        else:
            return add_node(self.root, key, value)

    def remove(self, key: Any) -> bool:
        """키가 key인 노드를 삭제"""
        p = self.root           # 스캔 중인 노드
        parent = None           # 스캔 중인 노드의 부모 노드
        is_left_child = True    # p는 parent의 왼쪽 자식 노드입니까?

        while True:
            if p is None:                       # 더 이상 진행할 수 없으면
                return False                    # ... 그 키는 존재하지 않음

            if key == p.key:                    # key와 노드 p의 키가 같으면
                break                           # ... 검색 성공
            else:
                parent = p                      # 가지를 내려가기 전에 부모를 설정
                if key < p.key:                 # key 쪽이 작으면
                    is_left_child = True        # ... 여기서 내려가는 것은 왼쪽 자식
                    p = p.left                  #... 왼쪽 서브 트리에서 검색
                else:                           # key 쪽이 크면
                    is_left_child = False       # ... 여기서 내려가는 것은 오른쪽 자식
                    p = p.right                 # ... 오른쪽 서브 트리에서 검색

        if p.left is None:                      # p에 왼쪽 자식이 없으면 ...
            if p is self.root:
                self.root = p.right
            elif is_left_child:
                parent.left = p.right           # 부모의 왼쪽 포인터가 오른쪽 자식을 가리킵니다.
            else:
                parent.right = p.right          # 부모의 오른쪽 포인터가 오른쪽 자식을 가리킵니다.
        elif p.right is None:                   # p에 오른쪽 자식이 없으면 ...
            if p is self.root:
                self.root = p.left
            elif is_left_child:
                parent.left = p.left            # 부모의 왼쪽 포인터가 왼쪽 자식을 가리킵니다.
            else:
                parent.right = p.left           # 부모의 오른쪽 포인터가 왼쪽 자식을 가리킵니다.
        else:
            parent = p
            left = p.left                       # 서브 트리 안에서 가장 큰 노드
            is_left_child = True
            while left.right is not None:       # 가장 큰 노드 left를 검색
                parent = left
                left = left.right
                is_left_child = False

            p.key = left.key                    # left의 키를 p로 이동
            p.value = left.value                # left의 데이터를 p로 이동
            if is_left_child:
                parent.left = left.left         # left를 삭제
            else:
                parent.right = left.left        # left를 삭제
        return True

    def dump(self, reverse = False) -> None:
        """덤프(모든 노드를 키의 오름차순/내림차순으로 출력)"""

        def print_subtree(node: Node):
            """node를 루트로 하는 서브 트리의 노드를 키의 오름차순으로 출력"""
            if node is not None:
                print_subtree(node.left)                # 왼쪽 서브 트리를 오름차순으로 출력
                print(f'{node.key}  {node.value}')      # node를 출력
                print_subtree(node.right)               # 오른쪽 서브 트리를 오름차순으로 출력

        def print_subtree_rev(node: Node):
            """node를 루트로 하는 서브 트리의 노드를 키의 내림차순으로 출력"""
            if node is not None:
                print_subtree_rev(node.right)           # 오른쪽 서브 트리를 내림차순으로 출력
                print(f'{node.key}  {node.value}')      # node를 출력
                print_subtree_rev(node.left)            # 왼쪽 서브 트리를 내림차순으로 출력

        print_subtree_rev(self.root) if reverse else print_subtree(self.root)

    def min_key(self) -> Any:
        """가장 작은 키"""
        if self.root is None:
            return None
        p = self.root
        while p.left is not None:
            p = p.left
        return p.key

    def max_key(self) -> Any:
        """가장 큰 키"""
        if self.root is None:
            return None
        p = self.root
        while p.right is not None:
            p = p.right
        return p.key
```

## 이진 검색 트리 프로그램 만들기

```python
# 이진 검색 트리 클래스 BinarySearchTree 사용하기

from enum import Enum
from bst import BinarySearchTree

Menu = Enum('Menu', ['삽입', '삭제', '검색', '덤프', '키의범위', '종료'])

def select_Menu() -> Menu:
    """메뉴 선택"""
    s = [f'({m.value}){m.name}' for m in Menu]
    while True:
        print(*s, sep = '  ', end='')
        n = int(input(': '))
        if 1 <= n <= len(Menu):
            return Menu(n)

tree = BinarySearchTree()  # 이진 검색 트리를 생성

while True:
    menu = select_Menu()  # 메뉴 선택

    if menu == Menu.삽입:  # 삽입
        key = int(input('삽입할 키를 입력하세요.: '))
        val = input('삽입할 값을 입력하세요.: ')
        if not tree.add(key, val):
            print('삽입에 실패했습니다!')

    elif menu == Menu.삭제:  # 삭제
        key = int(input('삭제할 키를 입력하세요.: '))
        tree.remove(key)

    elif menu == Menu.검색:  # 검색
        key = int(input('검색할 키를 입력하세요.: '))
        t = tree.search(key)
        if t is not None:
            print(f'이 키를 갖는 값은 {t}입니다.')
        else:
            print('해당 데이터가 없습니다.')

    elif menu == Menu.덤프:  # 덤프(모두 출력)
        tree.dump()

    elif menu == Menu.키의범위 :  # 키의 범위(최솟값과 최댓값)
        print(f'키의 최솟값은 {tree.min_key()}입니다.')
        print(f'키의 최댓값은 {tree.max_key()}입니다.')

    else:  # 종료
        break
```
