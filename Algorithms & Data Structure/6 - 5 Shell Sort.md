**셸 정렬**은 단순 삽입 정렬의 장점은 살리고 단점은 보완하여 더 빠르게 정렬하는 알고리즘입니다.

- 장점: 이미 정렬을 마쳤거나 정렬이 거의 끝나가는 상태에서는 속도가 아주 빠릅니다.
- 단점: 삽입할 위치가 멀리 떨어져 있으면 이동 횟수가 많아집니다.

### 셸 정렬 알아보기

셸 정렬은 먼저 정렬할 배열의 원소를 그룹으로 나눠 각 그룹별로 정렬을 수행합니다. 그 후 정렬된 그룹을 합치는 작업을 반복하여 원소의
이동 횟수를 줄이는 방법입니다.

```python
# 셸 정렬 알고리즘 구현하기

from typing import MutableSequence

def shell_sort(a: MutableSequence) -> None:
    """셸 정렬"""
    n = len(a)        # 8
    h = n // 2        # 4
    while h > 0:
        for i in range(h, n):
            j = i - h
            tmp = a[i]
            while j >= 0 and a[j] > tmp:        # 자리 교체 조건
                a[j + h] = a[j]
                j -= h
            a[j + h] = tmp
        h //= 2                                 # 4정렬 - 2정렬 - 1정렬

if __name__ == '__main__':
    print('셸 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    shell_sort(x)

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{[i]} = {x[i]}')
```

```
셸 정렬을 수행합니다.
원소 수를 입력하세요.: 6
x[0]: 1
x[1]: 5
x[2]: 7
x[3]: 2
x[4]: 1
x[5]: 9
오름차순으로 정렬했습니다.
x[[0] = 1
x[[1] = 1
x[[2] = 2
x[[3] = 5
x[[4] = 7
x[[5] = 9
```

```python
# 셸 정렬 알고리즘 구현하기(h * 3 + 1의 수열 사용)

from typing import MutableSequence

def shell_sort(a: MutableSequence) -> None:
    """셸 정렬(h * 3 + 1의 수열 사용)"""
    n = len(a)
    h = 1

    while h < n // 9:
        h = h * 3 + 1

    while h > 0:
        for i in range(h, n):
            j = i - h
            tmp = a[i]
            while j >= 0 and a[j] > tmp:
                a[j + h] = a[j]
                j -= h
            a[j + h] = tmp
        h //= 3                                     # 차이 2단위 -> 3단위 정렬

if __name__ == '__main__':
    print('셸 정렬을 수행합니다(h * 3 + 1의 수열 사용).')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num   # 원소 수가 num인 배열을 생성

    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))

    shell_sort(x)       # 배열 x를 셸 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
셸 정렬을 수행합니다(h * 3 + 1의 수열 사용).
원소 수를 입력하세요.: 6
x[0]: 1
x[1]: 6
x[2]: 7
x[3]: 2
x[4]: 1
x[5]: 8
오름차순으로 정렬했습니다.
x[0] = 1
x[1] = 1
x[2] = 2
x[3] = 6
x[4] = 7
x[5] = 8
```
