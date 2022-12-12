선택 정렬을 응용한 알고리즘인 힙 정렬을 알아보겠습니다.

## 힙 정렬 알아보기

**힙 정렬**은 힙의 특성을 이용하여 정렬하는 알고리즘입니다. 힙은 '부모의 값이 자식의 값보다 항상 크다'는 조건을 만족하는 완전 이진 트리입니다. 이때 부모의 값이 자식의 값보다 항상 작아도 힙이라고 합니다. 즉, 이러한 두 값의 대소 관계가 일정하면 됩니다.

### 트리를 알고 싶어요!

9장에서 트리를 설명하겠지만 힙을 이해하기 쉽도록 트리의 개념을 간단히 살펴보겠습니다. 트리는 각 원소를 의미하는 노드(node)들이 연결된 계층 구조합니다. 트리의 가장 윗부분에 위치한 루트(root)는 부모가 없는 노드입니다. 노드의 상하 관계에는 부모 노드(parent node)와 자식 노드(child node)가 있습니다. 그리고 부모가 같은 자식 간의 관계를 형제 노드(sibling node)라고 합니다. <br>
완전 이진 트리란 트리의 한 종류로 완전 이진 상태라는 특징이 있습니다. 여기에서 '완전'은 부모는 왼쪽 자식부터 추가하여 모양을 유지하라는 뜻입니다. 그리고 '이진'은 부모가 가질 수 있는 자식의 최대 개수는 2개라는 의미입니다.

부모 인덱스와 자식 인덱스 사이의 관계
**원소 a[i]에서**

- 부모: a[(i - 1) // 2]
- 왼쪽 자식: a[i * 2 + 1]
- 오른쪽 자식: a[i * 2 + 2]

## 힙 정렬의 특징

힙 정렬은 '힙에서 최댓값은 루트에 위치한다'는 특징을 이용하여 정렬하는 알고리즘입니다.

- 힙에서 최댓값인 루트를 꺼냅니다.
- 루트 이외의 부분을 힙으로 만듭니다.

## 루트를 삭제한 힙의 재구성

1. 루트를 꺼냅니다.
2. 마지막 원소(가장 하단의 오른쪽에 위치한 원소)를 루트로 이동합니다.
3. 루트에서 시작하여 자신보다 값이 큰 자식과 자리를 바꾸고 아래쪽으로 내려가는 작업을 반복합니다. 자식의 값이 작거나 리프의 위치에 도달하면 종료합니다.

## 힙 정렬 알고리즘 알아보기

1. i값을 n - 1로 초기화합니다.
2. a[0]과 a[i]를 교환합니다.
3. a[0], a[1], $ \cdots $, a[i - 1]을 힙으로 만듭니다.
4. i값을 1씩 감소시켜 0이 되면 종료합니다. 그렇지 않으면 2로 돌아갑니다.

```python
# 힙 정렬 알고리즘 구현하기

from typing import MutableSequence

def heap_sort(a: MutableSequence) -> None:
    """힙 정렬"""

    def down_heap(a: MutableSequence, left: int, right: int) -> None:
        """a[left] ~ a[right]를 힙으로 만들기"""
        temp = a[left]              # 루트

        parent = left
        while parent < (right + 1) // 2:       # a[(i + 1) // 2]
            cl = parent * 2 + 1                # 왼쪽 자식
            cr = cl + 1                        # 오른쪽 자식   # = parent * 2 + 2
            child = cr if cr <= right and a[cr] > a[cl] else cl   # 큰 값을 선택
            if temp >= a[child]:
                break
            a[parent] = a[child]
            parent = child
        a[parent] = temp

    n = len(a)

    for i in range((n - 1) // 2, -1, -1):    # a[i] ~ a[n - 1]을 힙으로 만들기
        down_heap(a, i, n - 1)

    for i in range(n - 1, 0, -1):
        a[0], a[i] = a[i], a[0]               #  최댓값인 a[0]와 마지막 원소를 교환
        down_heap(a, 0, i - 1)                # a[0] ~ a[i - 1]을 힙으로 만들기

if __name__ == '__main__':
    print('힙 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                         # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    heap_sort(x)                              # 배열 x를 힙 정렬

    print('오름차순으로 정렬했습니다')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
힙 정렬을 수행합니다.
원소 수를 입력하세요.: 7
x[0]: 4
x[1]: 1
x[2]: 6
x[3]: 2
x[4]: 7
x[5]: 8
x[6]: 3
오름차순으로 정렬했습니다
x[0] = 1
x[1] = 2
x[2] = 3
x[3] = 4
x[4] = 6
x[5] = 7
x[6] = 8
```

## 힙 정렬의 시간 복잡도

단순 선택 정렬에서 최댓값인 원소를 선택하는 시간 복잡도는 O(n)이지만, 힙 정렬에서 다시 힙으로 만드는 작업의 시간 복잡도는 $ O(log~n) $입니다.

### heapq 모듈을 사용하는 힙 정렬

파이썬 의 heapq 모듈은 힙에 원소를 추가하는 heappush() 함수와 힙에서 원소를 제거하는 heappop() 함수를 제공합니다. 이때 푸시와 팝은 힙의 조건을 유지하며 수행됩니다.

```python
# 힙 정렬 알고리즘 구현하기(heapq.push와 heapq.pop를 사용）

import heapq
from typing import MutableSequence

def heap_sort(a: MutableSequence) -> None:
    """힙 정렬(heapq.push와 heapq.pop를 사용)"""

    heap = []
    for i in a:
        heapq.heappush(heap, i)
    for i in range(len(a)):
        a[i] = heapq.heappop(heap)

if __name__ == '__main__':
    print('힙 정렬을 수행합니다(heapq.push와 heapq.pop를 사용).')
    num = int(input('원소 수를 입력하세요. : '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}] : '))

    heap_sort(x)        # 배열 x를 힙 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
힙 정렬을 수행합니다(heapq.push와 heapq.pop를 사용).
원소 수를 입력하세요. : 7
x[0] : 1
x[1] : 5
x[2] : 8
x[3] : 2
x[4] : 4
x[5] : 3
x[6] : 6
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 2
x[2] = 3
x[3] = 4
x[4] = 5
x[5] = 6
x[6] = 8
```
