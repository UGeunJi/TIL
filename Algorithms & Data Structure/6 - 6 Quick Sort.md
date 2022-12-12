**퀵 정렬**은 가장 빠른 정렬 알고리즘으로 알려져 있으며 널리 사용됩니다.

## 퀵 정렬 알아보기

퀵 정렬은 배열을 중앙 인덱스인 피벗을 기준으로 두 그룹으로 나누어 정렬을 진행합니다.
그룹을 나누려면 피벗 이하인 원소를 배열 왼쪽(맨 앞쪽)으로, 피벗 이상인 원소를 배열 오른쪽(맨 뒤쪽)으로 이동시켜야 합니다.

- a[pl] >= x가 성립하는 원소를 찾을 때까지 pl을 오른쪽 방향으로 스캔합니다.
- a[pr] <= x가 성립하는 원소를 찾을 때까지 pr를 왼쪽 방향으로 스캔합니다.

### 배열을 두 그룹으로 나누기

```python
from typing import MutableSequence

def partition(a: MutableSequence) -> None:
    """배열을 나누어 출력"""
    n = len(a)
    pl = 0           # 왼쪽 커서
    pr = n - 1      # 오른쪽 커서
    x = a[n // 2]   # 피벗(가운데 원소)

    while pl <= pr:
        while a[pl] < x: pl += 1              # 피벗보다 작은 거 찾을 때까지
        while a[pr] > x: pr -= 1              # 피벗보다 큰 거 찾을 
        if pl <= pr:
            a[pl], a[pr] = a[pr], a[pl]
            pl += 1
            pr -= 1

    print(f'피벗은 {x}입니다.')

    print('피벗 이하인 그룹입니다.')
    print(*a[0 : pl])           # a[0] ~ a[pl - 1]

    if pl > pr + 1:
        print('피벗과 일치하는 그룹입니다.')
        print(*a[pr + 1 : pl])  # a[pr + 1] ~ a[pl - 1]

    print('피벗 이상인 그룹입니다.')
    print(*a[pr + 1 : n])       # a[pr + 1] ~ a[n - 1]

if __name__ == '__main__':
    print('배열을 나눕니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num           # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]'))

    partition(x)                # 배열 x를 나누어서 출력
```

```
배열을 나눕니다.
원소 수를 입력하세요.: 7
x[0]2
x[1]5
x[2]6
x[3]1
x[4]7
x[5]9
x[6]10
피벗은 1입니다.
피벗 이하인 그룹입니다.
1
피벗 이상인 그룹입니다.
5 6 2 7 9 10
```

### 이 방식을 반복함으로써 퀵 정렬을 구현합니다.

```python
# 퀵 정렬 알고리즘 구현하기

from typing import MutableSequence

def qsort(a: MutableSequence, left: int, right: int) -> None:
    """a[left] ~ a[right]를 퀵 정렬"""
    pl = left                        # 왼쪽 커서
    pr = right                       # 오른쪽 커서
    x = a[(left + right) // 2]      # 피벗(가운데 원소) 

    while pl <= pr:                         # 배열 나누는 코드
        while a[pl] < x: pl += 1
        while a[pr] > x: pr -= 1
        if pl <= pr:
            a[pl], a[pr] = a[pr], a[pl]
            pl += 1
            pr -= 1

    if left < pr: qsort(a, left, pr)        # 재귀호출을 통해 또 그룹을 
    if pl < right: qsort(a, pl, right)

def quick_sort(a: MutableSequence) -> None:
    """퀵 정렬"""
    qsort(a, 0, len(a) - 1)

if __name__ == '__main__':
    print('퀵 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    quick_sort(x)        # 배열 x를 퀵 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
퀵 정렬을 수행합니다.
원소 수를 입력하세요.: 7
x[0]: 29
x[1]: 10
x[2]: 5
x[3]: 6
x[4]: 7
x[5]: 1
x[6]: 5
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 5
x[2] = 5
x[3] = 6
x[4] = 7
x[5] = 10
x[6] = 29
```

- 재귀호출을 사용
- 서로 이웃하지 않는 원소를 교환하므로 안정적이지 않은 알고리즘

### 배열을 나누는 과정 출력

```python
# 퀵 정렬 알고리즘 구현

from typing import MutableSequence

def qsort(a: MutableSequence, left: int, right: int) -> None:
    """a[left] ~ a[right]를 퀵 정렬(배열을 나누는 과정 출력)"""
    pl = left                   # 왼쪽 커서
    pr = right                  # 오른쪽 커서
    x = a[(left + right) // 2]  # 피벗(가운데 원소)

    print(f'a[{left}] ~ a[{right}]: ', *a[left : right + 1])  # 새로 추가된 부분

    while pl <= pr:                     
        while a[pl] < x: pl += 1
        while a[pr] > x: pr -= 1
        if pl <= pr:                    
            a[pl], a[pr] = a[pr], a[pl]
            pl += 1
            pr -= 1

    if left < pr: qsort(a, left, pr)   
    if pl < right: qsort(a, pl, right)

def quick_sort(a: MutableSequence) -> None:
    """퀵 정렬"""
    qsort(a, 0, len(a) - 1)

if __name__ == '__main__':
    print('퀵 정렬을 수행합니다(배열을 나누는 과정 출력).')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    quick_sort(x)       # 배열 x를 퀵 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
퀵 정렬을 수행합니다(배열을 나누는 과정 출력).
원소 수를 입력하세요.: 7
x[0]: 1
x[1]: 5
x[2]: 7
x[3]: 8
x[4]: 0
x[5]: 10
x[6]: 58
a[0] ~ a[6]:  1 5 7 8 0 10 58
a[0] ~ a[3]:  1 5 7 0
a[0] ~ a[1]:  1 0
a[2] ~ a[3]:  7 5
a[4] ~ a[6]:  8 10 58
오름차순으로 정렬했습니다.
x[0] = 0
x[1] = 1
x[2] = 5
x[3] = 7
x[4] = 8
x[5] = 10
x[6] = 58
```

### 비재귀적인 퀵 정렬 만들기

```python
# 비재귀적인 퀵 정렬 구현하기

from stack import Stack
from typing import MutableSequence

def qsort(a: MutableSequence, left: int, right: int) -> None:
    """a[left] ~ a[right]를 퀵 정렬(비재귀적인 퀵 정렬)"""
    range = Stack(right - left + 1)                # 스택 생성

    range.push((left, right))

    while not range.is_empty():                    # 모두 push될 때까지 반복
        pl, pr = left, right = range.pop()         # 왼쪽, 오른쪽 커서를 꺼냄
        x = a[(left + right) // 2]                 # 피벗(가운데 원소)

        while pl <= pr:
            while a[pl] < x: pl += 1
            while a[pr] > x: pr -= 1
            if pl <= pr:
                a[pl], a[pr] = a[pr], a[pl]
                pl += 1
                pr -= 1

        if left < pr: range.push((left, pr))       # 왼쪽 그룹의 커서를 저장
        if pr < right: range.push((pl, right))     # 오른쪽 그룹의 커서를 저장

if __name__ == '__main__':
    print('퀵 정렬을 수행합니다(배열을 나누는 과정 출력).')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    qsort(x)       # 배열 x를 퀵 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

## 퀵 정렬의 시간 복잡도

시간 복잡도는 $ O(n~log~n) $ 입니다. 그런데 정렬하는 배열의 초깃값이나 피벗을 선택하는 방법에 따라 실행 시간 복잡도가 증가하는 경우도 있습니다. 예를 들어 매번 1개의 원소와 나머지 원소로 나누어진다면 n번의 분할이 필요합니다. 이러한 경우 시간 복잡도는 $ O(n^2) $ 이 됩니다.

- 원소 수가 9개 미만인 경우 단순 삽입 정렬로 전환합니다.
- 피벗 선택은 방법 2를 채택합니다.

```python
# 퀵 정렬 알고리즘 구현하기(원소 수가 9개 미만인 경우 단순 삽입 정렬)

from typing import MutableSequence

def sort3(a: MutableSequence, idx1: int, idx2: int, idx3: int):
    """a[idx1], a[idx2], a[idx3]을 오름차순으로 정렬하고 가운데 값의 인덱스를 반환"""
    if a[idx2] < a[idx1]: a[idx2], a[idx1] = a[idx1], a[idx2]
    if a[idx3] < a[idx2]: a[idx3], a[idx2] = a[idx2], a[idx3]
    if a[idx2] < a[idx1]: a[idx2], a[idx1] = a[idx1], a[idx2]
    return idx2

def insertion_sort(a: MutableSequence, left: int, right: int) -> None:
    """a[left] ~ a[right]를 단순 삽입 정렬"""
    for i in range(left + 1, right + 1):
        j = i
        tmp = a[i]
        while j > 0 and a[j - 1] > tmp:
            a[j] = a[j - 1]
            j -= 1
        a[j] = tmp

def qsort(a: MutableSequence, left: int, right: int) -> None:
    """a[left] ~ a[right]를 퀵 정렬"""
    if right - left < 9:            # 원소 수가 9개 미만이면 단순 삽입 정렬을 호출
        insertion_sort(a, left, right)
    else:                           # 원소 수가 9개 이상이면 퀵 정렬을 수행
        pl = left                   # 왼쪽 커서
        pr = right                  # 오른쪽 커서
        m = sort3(a, pl, (pl + pr) // 2, pr)
        x = a[m]

        a[m], a[pr - 1] = a[pr - 1], a[m]
        pl += 1
        pr -= 2
        while pl <= pr:
            while a[pl] < x: pl += 1
            while a[pr] > x: pr -= 1
            if pl <= pr:
                a[pl], a[pr] = a[pr], a[pl]
                pl += 1
                pr -= 1

        if left < pr: qsort(a, left, pr)
        if pl < right: qsort(a, pl, right)

def quick_sort(a: MutableSequence) -> None:
    """퀵 정렬"""
    qsort(a, 0, len(a) - 1)

if __name__ == '__main__':
    print('퀵 정렬을 합니다(원소 수가 9개 미만이면 단순 삽입 정렬).')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num    # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    quick_sort(x)       # 배열 x를 퀵 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
퀵 정렬을 합니다(원소 수가 9개 미만이면 단순 삽입 정렬).
원소 수를 입력하세요.: 12
x[0]: 6
x[1]: 1
x[2]: 2
x[3]: 7
x[4]: 9
x[5]: 3
x[6]: 5
x[7]: 6
x[8]: 3
x[9]: 6
x[10]: 7
x[11]: 9
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 2
x[2] = 3
x[3] = 3
x[4] = 5
x[5] = 6
x[6] = 6
x[7] = 6
x[8] = 7
x[9] = 7
x[10] = 9
x[11] = 9
```

## sorted() 함수로 정렬하기

- a, b =sorted([a, b]) # a, b를 오름차순으로 정렬
- a, b, c = sorted([a, b, c]) # a, b, c를 오름차순으로 정렬
- a, b, c, d = sorted([a, b, c, d]) # a, b, c, d를 오름차순으로 정렬

```python
# sorted() 함수를 사용하여 정렬하기

print('sorted() 함수를 사용하여 정렬합니다.')
num = int(input('원소 수를 입력하세요.: '))
x = [None] * num   # 원소 수가 num인 배열을 생성

for i in range(num):
    x[i] = int(input(f'x[{i}]: '))

# 배열 x를 오름차순으로 정렬
x = sorted(x)
print('오름차순으로 정렬했습니다.')
for i in range(num):
    print(f'x[{i}] = {x[i]}')

# 배열 x를 내림차순으로 정렬
x = sorted(x, reverse = True)
print('내림차순으로 정렬했습니다.')
for i in range(num):
    print(f'x[{i}] = {x[i]}')
```

```
sorted() 함수를 사용하여 정렬합니다.
원소 수를 입력하세요.: 7
x[0]: 1
x[1]: 2
x[2]: 5
x[3]: 6
x[4]: 72
x[5]: 2
x[6]: 1
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 1
x[2] = 2
x[3] = 2
x[4] = 5
x[5] = 6
x[6] = 72
내림차순으로 정렬했습니다.
x[0] = 72
x[1] = 6
x[2] = 5
x[3] = 2
x[4] = 2
x[5] = 1
x[6] = 1
```
