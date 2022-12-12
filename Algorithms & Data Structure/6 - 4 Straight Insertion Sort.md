**단순 삽입 정렬**은 주목한 원소보다 더 앞쪽에서 알맞은 위치로 삽입하며 정렬하는 알고리즘입니다. 단순 선택 정렬과 비슷해 보이지만
값이 가장 작은 원소를 선택하지 않는다는 점이 다릅니다.

## 단순 삽입 정렬 알아보기

```
j = i
tmp = a[i]
while j > 0 and a[j - 1] > tmp:
    a[j] = a[j - 1]
    j -= 1
a[j] = tmp
```

a[i]보다 작은 수를 찾을 때까지 값을 하나씩 오른쪽으로 이동시킵니다.

작은 수를 찾으면 한칸 오른쪽에 a[i]값을 넣습니다.

- 종료 조건 1: 정렬된 배열의 왼쪽 끝에 도달한 경우
  
- 종료 조건 2: tmp보다 작거나 키값이 같은 원소 a[j - 1]을 발견할 경우
  
- 계속 조건 1: j가 0보다 큰 경우
  
- 계속 조건 2: a[j - 1]의 값이 tmp보다 큰 경우
  

```python
# 단순 삽입 정렬 알고리즘 구현하기

from typing import MutableSequence

def insertion_sort(a: MutableSequence) -> None:
    """단순 삽입 정렬"""
    n = len(a)
    for i in range(1, n):
        j = i
        tmp = a[i]
        while j > 0 and a[j - 1] > tmp:
            a[j] = a[j - 1]
            j -= 1
        a[j] = tmp

if __name__ == '__main__':
    print('단순 삽입 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num  # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    insertion_sort(x)  # 배열 x를 단순 삽입 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
단순 삽입 정렬을 수행합니다.
원소 수를 입력하세요.: 7
x[0]: 1
x[1]: 6
x[2]: 8
x[3]: 3
x[4]: 42
x[5]: 5
x[6]: 1
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 1
x[2] = 3
x[3] = 5
x[4] = 6
x[5] = 8
x[6] = 42
```

이 알고리즘은 서로 떨어져 있는 원소를 교환하지 않으므로 안정적이라고 할 수 있습니다.

원소의 비교 횟수와 교환 횟수는 모두 $ n^2 ~ / ~ 2 $ 번입니다.

### 단순 정렬 알고리즘의 시간 복잡도

지금까지 다룬 3가지 단순 정렬(버블, 선택, 삽입) 알고리즘의 시간 복잡도는 모두 $ O(n^2) $으로 프로그램의 효율이 좋지 않습니다.
아래는 이러한 단순 정렬 알고리즘의 개선 방법을 적용한 정렬 알고리즘을 알아보겠습니다.

## 이진 삽입 정렬(binary insertion sort)

```python
# 이진 삽입 정렬 알고리즘 구현하기

from typing import MutableSequence

def binary_insertion_sort(a: MutableSequence) -> None:
    """이진 삽입 정렬"""
    n = len(a)
    for i in range(1, n):
        key = a[i]
        pl = 0                                   # 검색 범위의 맨 앞 원소 인덱스
        pr = i - 1                               # 검색 범위의 맨 끝 원소 인덱스

        while True:
            pc = (pl + pr) // 2                  # 검색 범위의 가운데 원소 인덱스
            if a[pc] == key:                     # 검색 성공     # 중앙값이면 검색 끝
                break
            elif a[pc] < key:                    # 오른쪽
                pl = pc + 1                      # 검색 범위를 뒤쪽 절반으로 좁힘
            else:     
                pr = pc - 1                      # 검색 범위를 앞쪽 절반으로 좁힘   # 왼쪽
            if pl > pr:                          # 오류 
                break

        pd = pc + 1 if pl <= pr else pr + 1     # 삽입해야 할 위치의 인덱스

        for j in range(i, pd, -1):
            a[j] = a[j - 1]
        a[pd] = key

if __name__ == '__main__':
    print('이진 삽입 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                             # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    binary_insertion_sort(x)                      # 배열 x를 이진 삽입 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
이진 삽입 정렬을 수행합니다.
원소 수를 입력하세요.: 8
x[0]: 2
x[1]: 58
x[2]: 692
x[3]: 10
x[4]: 59
x[5]: 57
x[6]: 20
x[7]: 4
오름차순으로 정렬했습니다.
x[0] = 2
x[1] = 4
x[2] = 10
x[3] = 20
x[4] = 57
x[5] = 58
x[6] = 59
x[7] = 692
```

```python
# 이진 삽입 정렬 알고리즘 구현(bisect.insort 사용)

from typing import MutableSequence
import bisect

def binary_insertion_sort(a: MutableSequence) -> None:
    """이진 삽입 정렬(bisect.insort 사용)"""
    for i in range(1, len(a)):
        bisect.insort(a, a.pop(i), 0, i)

if __name__ == '__main__':
    print('이진 삽입 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                             # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    binary_insertion_sort(x)                      # 배열 x를 이진 삽입 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
이진 삽입 정렬을 수행합니다.
원소 수를 입력하세요.: 5
x[0]: 1
x[1]: 6
x[2]: 8
x[3]: 3
x[4]: 2
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 2
x[2] = 3
x[3] = 6
x[4] = 8
```
