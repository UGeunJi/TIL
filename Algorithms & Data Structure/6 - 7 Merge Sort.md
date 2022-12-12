**병합 정렬**은 배열을 앞부분과 뒷부분의 두 그룹으로 나누어 각각 정렬한 후 병합하는 작업을 반복하는 알고리즘입니다.

## 정렬을 마친 배열의 병합

각 배열에서 주목하는 원소의 값을 비교하여 작은 쪽의 원소를 꺼내 새로운 배열에 저장합니다. 이 작업을 반복하며 정렬을 마친 배열을 만듭니다.

병합하는데 필요한 시간 복잡도는 $ O(n) $ 입니다.

```python
# 정렬을 마친 두 배열을 병합히가

from typing import Sequence, MutableSequence

def merge_sorted_list(a: Sequence, b: Sequence, c: MutableSequence) -> None:
    """정렬을 마친 배열 a와 b를 병합하여 c에 저장"""
    pa, pb, pc = 0, 0, 0                     # 각 배열의 커서
    na, nb, nc = len(a), len(b), len(c)      # 각 배열의 원소 수

    while pa < na and pb < nb:              # pa와 pb를 비교하여 작은 값을 pc에 저장
        if a[pa] <= b[pb]:                  # pa가 더 작으면
            c[pc] = a[pa]                   # pa가 pc로 입력
            pa += 1 
        else:                               # pb가 더 작으면
            c[pc] = b[pb]                   # pb가 pc로 입력
            pb += 1
        pc += 1

    while pa < na:                          # a에 남은 원소를 c에 복사
        c[pc] = a[pa]
        pa += 1
        pc += 1

    while pb < nb:                          # b에 남은 원소를 c에 
        c[pc] = b[pb]
        pb += 1
        pc += 1

if __name__ == '__main__':
    a = [2, 4, 6, 8, 11, 13]
    b = [1, 2, 3, 4, 9, 16, 21]
    c = [None] * (len(a) + len(b))
    print('정렬을 마친 두 배열의 병합을 수행합니다.')

    merge_sorted_list(a, b, c)                # 배열 a와 b를 병합하여 c에 저장

    print('배열 a와 b를 병합하여 배열 c에 저장했습니다.')
    print(f'배열 a: {a}')
    print(f'배열 b: {b}')
    print(f'배열 c: {c}')
```

```
정렬을 마친 두 배열의 병합을 수행합니다.
배열 a와 b를 병합하여 배열 c에 저장했습니다.
배열 a: [2, 4, 6, 8, 11, 13]
배열 b: [1, 2, 3, 4, 9, 16, 21]
배열 c: [1, 2, 2, 3, 4, 4, 6, 8, 9, 11, 13, 16, 21]
```

### sorted() 함수로 병합 정렬하기

```python
c = list(sorted(a + b))   # a와 b를 연결하여 오름차순으로 정렬한 것을 list로 변환하여 c에 저장
```

이 방법은 a와 b가 정렬을 마친 상태가 아니어도 적용할 수 있다는 장점이 있지만, 속도가 빠르지 않다는 단점이 있습니다. 빠르게 병합하려면 다음과 같이 heapq 모듈의 merge() 함수를 사용하면 됩니다.

```python
# 병합 정렬 알고리즘 구현하기(heapq.merge를 사용)

from typing import MutableSequence
import heapq

def merge_sort(a: MutableSequence) -> None:
    """병합 정렬(heapq.merge를 사용)"""
    atype = type(a)

    def _merge_sort(a: MutableSequence, left: int, right: int) -> None:
        """a[left]～a[right]를 재귀적으로 병합 정렬"""
        if left < right:
            center = (left + right) // 2

            _merge_sort(a, left, center)            # 앞부분 배열의 병합 정렬
            _merge_sort(a, center + 1, right)       # 뒷부분 배열의 병합 정렬

            buff = atype(heapq.merge(a[left: center+1], a[center + 1: right+1]))
            for i in range(len(buff)):
                a[left + i] = buff[i]

    _merge_sort(a, 0, len(a))       # 배열 전체를 병합 정렬

if __name__ == '__main__':
    print('병합 정렬을 수행합니다(heapq.merge를 사용).')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}] : '))

    merge_sort(x)       # 배열 x를 병합 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

## 병합 정렬 만들기

### 병합 정렬 알고리즘

**배열의 원소 수가 2개 이상인 경우**

1. 배열의 앞부분을 병합 정렬로 정렬합니다.
2. 배열의 뒷부분을 병합 정렬로 정렬합니다.
3. 배열의 앞부분과 뒷부분을 병합합니다.

```python
# 병합 정렬 알고리즘 구현하기

from typing import MutableSequence

def merge_sort(a: MutableSequence) -> None:
    """병합 정렬"""

    def _merge_sort(a: MutableSequence, left: int, right: int) -> None:
        """a[left] ~ a[right]를 재귀적으로 병합 정렬"""
        if left < right:
            center = (left + right) // 2

            _merge_sort(a, left, center)           # 배열 앞부분을 병합 정렬
            _merge_sort(a, center + 1, right)      # 배열 뒷부분을 병합 정렬

            p = j = 0
            i = k = left

            while i <= center:
                buff[p] = a[i]                     # 왼쪽 buff에 저장
                p += 1
                i += 1

            while i <= right and j < p:
                if buff[j] <= a[i]:                # 오른쪽이랑 a에 병합
                    a[k] = buff[j]
                    j += 1
                else:
                    a[k] = a[i]
                    i += 1
                k += 1

            while j < p:                           # 남아있는 원소 병합
                a[k] = buff[j]
                k += 1
                j += 1

    n = len(a)
    buff = [None] * n                          # 작업용 배열을 생성
    _merge_sort(a, 0, n - 1)                   # 배열 전체를 병합 정렬

    del buff                                       # 작업용 배열을 소멸

if __name__ == '__main__':
    print('병합 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                               # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    merge_sort(x)                                   # 배열 x를 병합 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
병합 정렬을 수행합니다.
원소 수를 입력하세요.: 7
x[0]: 1
x[1]: 9
x[2]: 5
x[3]: 0
x[4]: 2
x[5]: 4
x[6]: 3
오름차순으로 정렬했습니다.
x[0] = 0
x[1] = 1
x[2] = 2
x[3] = 3
x[4] = 4
x[5] = 5
x[6] = 9
```
