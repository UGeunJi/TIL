**도수 정렬**은 원소의 대소 관계를 판단하지 않고 빠르게 정렬하는 알고리즘으로, 분포수 세기(distribution counting) 정렬이라고도 합니다.

## 도수 정렬 알아보기

- 1단계: 도수 분포표 만들기
- 2단계: 누적 도수 분포표 만들기
- 3단계: 작업용 배열 만들기
- 4단계: 배열 복사하기

### 도수 분포표는 무엇인가요?

확률과 통계에서 자주 등장하는 용어인 도수 분포표는 자료를 몇 개의 등급으로 나누고 각 등급에 속하는 도수를 조사하여 나타낸 표를 의미합니다. 여기에서 도수는 각 등급에 속하는 자료의 개수입니다.

### 도수 정렬은 if문을 사용하지 않고 for문만 반복해서 정렬할 수 있는 알고리즘입니다.

```python
# 도수 정렬 알고리즘 구현하기

from typing import MutableSequence

def fsort(a: MutableSequence, max: int) -> None:
    """도수 정렬(배열 원솟값은 0 이상 max 이하)"""
    n = len(a)
    f = [0] * (max + 1)
    b = [0] * n

    for i in range(n):                      f[a[i]] += 1                        # [1단계]     # one-hot-encoding
    for i in range(1, max + 1):             f[i] += f[i - 1]                    # [2단계]     # 누적 도수분포표
    for i in range(n - 1, -1, -1):          f[a[i]] -= 1; b[f[a[i]]] = a[i]     # [3단계]     # 작업용 배열 생성
    for i in range(n):                       a[i] = b[i]                        # [4단계]     # 배열 복사 = 저장

def counting_sort(a: MutableSequence) -> None:
    """도수 정렬"""
    fsort(a, max(a))

if __name__ == '__main__':
    print('도수 정렬을 수행합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                                 # 원소 수가 num인 배열을 생성

    for i in range(num):                             # 양수만 입력받도록 제한
        while True:
            x[i] = int(input(f'x[{i}]: '))
            if x[i] >= 0: break

    counting_sort(x)                                  # 배열 x를 도수 정렬

    print('오름차순으로 정렬했습니다.')
    for i in range(num):
        print(f'x[{i}] = {x[i]}')
```

```
도수 정렬을 수행합니다.
원소 수를 입력하세요.: 7
x[0]: 51
x[1]: 2
x[2]: 57
x[3]: 12
x[4]: 73
x[5]: 83
x[6]: 53
오름차순으로 정렬했습니다.
x[0] = 2
x[1] = 12
x[2] = 51
x[3] = 53
x[4] = 57
x[5] = 73
x[6] = 83
```

#### 최솟값과 최댓값을 미리 알고 있는 경우에만 적용할 수 있습니다.

#### 3단계에서 배열 a를 스캔할 때 맨 앞부터 스캔하면 안정적이지 않다는 점을 주의해야 합니다.
