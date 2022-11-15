이진 검색을 알아보겠습니다. 이진 검색 알고리즘을 사용하려면 배열의 데이터가 정렬되어 있어야 합니다. 이진 검색은 선형 검색보다 빠르게 검색할 수 있다는 장점이 있습니다.

# 이진 검색

이진 검색은 원소가 오름차순이나 내림차순으로 정렬된 배열에서 좀 더 효율적으로 검색할 수 있는 알고리즘입니다.

## 이진 검색 알고리즘
```py
from typing import Any, Sequence

def bin_search(a: Sequence, key: Any) -> int:
    """시퀀스 a에서 key와 일치하는 원소를 이진 검색"""
    pl = 0                    # 검색 범위 맨 앞 원소의 인덱스
    pr = len(a) - 1           # 검색 범위 맨 끝 원소의 인덱스
    
    while True:
        pc = (pl + pr) // 2   # 중앙 원소의 인덱스
        if a[pc] == key:
            return pc         # 검색 성공
        elif a[pc] < key:
            pl = pc + 1        # 검색 범위를 뒤쪽 절반으로 좁힙
        else:
            pr = pc - 1        # 검색 범위를 앞쪽 절반으로 좁힘
        if pl > pr:
            break
    return -1                 # 검색 실패                               # 함수 생성  여기까지가 핵심 코드


if __name__ == '__main__':
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                               # 원소 수가 num인 배열을 생성
    
    
    print('배열 데이터를 오름차순으로 입력하세요.')
    
    x[0] = int(input('x[0]: '))                     # 배열 초기화
    
    for i in range(1, num):
        while True:
            x[i] = int(input(f'x[{i}]: '))
            if x[i] >= x[i - 1]:                   # 바로 직전에 입력한 원솟값보다 큰 값을 입력
                break                              # 조건이 성립되면 다음 작업 수행
    
    
    ky = int(input('검색할 값을 입력하세요.: '))    # 검색할 키값 ky를 입력
    
    
    idx = bin_search(x, ky)                         # ky값과 같은 원소를 x에서 검색

    
    if idx == -1:
        print('검색값을 갖는 원소가 존재하지 않습니다.')
    else:
        print(f'검색값은 x[{idx}]에 있습니다.')
```
앞에서 설명했듯이 이진 검색에서는 검색 대상인 배열이 오름차순으로 정렬되어 있어야 합니다. 따라서 28 ~ 34행에서는 바로 앞에 입력한 원소보다 큰 값을 입력받도록 유도합니다. 만약 바로 앞에 입력한 원소보다 작은 값을 입력하면 다시 입력해야 합니다. <br>
이진 검색 알고리즘은 반복할 때마다 검색 범위가 거의 절반으로 줄어드므로 검색하는 데 필요한 비교 횟수는 평균 $\log n$입니다. 검색에
실패할 경우는 [$\log (n + 1)$]번이며, 검색에 성공할 경우는 $\log n - 1$번입니다.

[ x ]는 x의 천장 함수(Ceiling Function)라고 하며, x보다 크거나 정수 가운데 가장 작은 수를 가리킵니다. 예를 들어 [3.5]는 4입니다.

## 복잡도

알고리즘의 성능을 객관적으로 평가하는 기준을 복잡도(Complexity)라고 합니다. 복잡도는 다음과 같이 2가지로 구분합니다.
- **시간 복잡도**(time complexity): 실행하는 데 필요한 시간을 평가합니다.
- **공간 복잡도**(space complexity): 메모리(기억 공간)와 파일 공간이 얼마나 필요한지를 평가합니다.

## 선형 검색의 시간 복잡도

# 선형 검색하는 seq_search()함수를 바탕으로 시간 복잡도를 알아봅시다.
```py
def seq_search(a: Sequence, key: Any) -> int:
    i = 0   # 1 
    
    while i < n:  # 2
        if a[i] == key:   # 3
            return i    # 4   # 검색에 성공하여 인덱스를 반환 
        i += 1  # 5
    
return -1   # 6               # 검색에 실패하여 -1을 반환
```
| 단계 | 실행 횟수 | 복잡도 |
| --- | --- | --- |
| 1 | 1 | O(1) |
| 2 | n / 2 | O(n) |
| 3 | n / 2 | O(n) |
| 4 |  1 | O(1) |
| 5 | n / 2 | O(n) |
| 6 | 1 | O(1) |

n이 점점 커지면 O(n)에 필요한 계산 시간은 n에 비례하여 점점 길어집니다. 하지만 O(1)에 필요한 계산 시간은 변하지 않습니다.
여기서 짐작할 수 있듯이 O(f(n))과 O(g(n))의 동작을 연속으로 하는 경우 복잡도는 일반적으로 다음과 같이 나타냅니다.

O(f(n)) + O(g(n)) = O(max(f(n)), g(n)))

2가지 계산으로 구성된 알고리즘의 복잡도는 차원이 더 높은 쪽의 복잡도를 우선으로 합니다. 3가지 이상의 계산으로 구성된 알고리즘도 마찬가지입니다.
다시 말해 전체 복잡도는 차원이 가장 높은 복잡도를 선택하는 격입니다. 그러므로 선형 검색 알고리즘의 복잡도는 다음과 같이 O(n)이 됩니다.

O(1) + O(n) + O(n) + O(1) + O(n) + O(1) = O(max(1, n, n, 1, n, 1)) = O(n)

### index() 함수로 검색하기

리스트 또는 튜플에서 검색은 각 클래스의 index() 함수로 수행할 수 있습니다. index() 함수는 다음과 같은 형식으로 호출합니다. 호출할 때 인수는 j 또는 i, j를 생략할 수 있습니다.

obj.index(x, i, j)

### 이진 검색의 시간 복잡도
```py
def bin_search(a: Sequence, key: Any) -> int:
    
    pl = 0         # 1                       # 검색 범위 맨 앞 원소의 인덱스
    pr = len(a) - 1      # 2                 # 검색 범위 맨 뒤 원소의 인덱스
    
    while True:
        pc = (pl + pr) // 2     # 3          # 중앙 원소의 인덱스
        if a[pc] == key:        # 4
            return pc           # 5          # 검색 성공
        elif a[pc] < key:       # 6
            pl = pc + 1         # 7          # 검색 범위를 뒤쪽 절반으로 좁힘
        else:
            pr = pc - 1                      # 검색 범위를 앞쪽 절반으로 좁힘
        if pl > pr:
            break
    return -1                               # 검색 실패
```
| 단계 | 실행 횟수 | 복잡도 |
| --- | --- | --- |
| 1 | 1 | O(1) |
| 2 | 1 | O(1) |
| 3 | $\log n$ | O($\log n$) |
| 4 | $\log n$ | O($\log n$) |
| 5 | 1 | O(1) |
| 6 | $\log n$ | O($\log n$) |
| 7 | $\log n$ | O($\log n$) |
| 8 | $\log n$ | O($\log n$) |
| 9 | $\log n$ | O($\log n$) |
| 10 | 1 | O(1) |

이진 검색 알고리즘의 복잡도는 다음과 같이 O($\log n$)으로 얻을 수 있습니다.

O(1) + O(1) + O($\log n$) + O($\log n$) + O(1) + O($\log n$) + $\cdots$ + O(1) = O($\log n$)

## 이진 검색 알고리즘의 실행 과정 출력
```py
from typing import Any, Sequence

def bin_search(a: Sequence, key: Any) -> int:
    """시퀀스 a에서 key와 일치하는 원소를 이진 검색(실행 과정을 출력)"""
    pl = 0                  # 검색 범위 맨 앞 원소의 인덱스
    pr = len(a) - 1         # 검색 범위 맨 뒤 원소의 인덱스
    
    print('   |', end = '')
    for i in range(len(a)):
        print(f'{i : 4}', end = '')
    print()
    print('---+' + (4 * len(a) + 2) * '-')
              
    while True:
        pc = (pl + pr) // 2  # 중앙 원소의 인덱스
              
        print('   |', end = '')
        if pl != pc:
            print((pl * 4 + 1) * ' ' + '<-' + ((pc - pl) * 4) * ' ' + '+', end = '')
        else:
            print((pc * 4 + 1) * ' ' + '<+', end = '')
        if pc != pr:
            print(((pr - pc) * 4 - 2) * ' ' + '->')
        else:
            print('->')
        print(f'{pc:3}|', end = '')
        for i in range(len(a)):
            print(f'{a[i]:4}', end = '')
        print('\n   |')
        
        if a[pc] == key:
            return pc         # 검색 성공
        elif a[pc] < key:
            pl = pc + 1        # 검색 범위를 뒤쪽 절반으로 좁힙
        else:
            pr = pc - 1        # 검색 범위를 앞쪽 절반으로 좁힘
        if pl > pr:
            break
    return -1                 # 검색 실패                                 # 함수 생성 - 여기까지가 핵심 
              
if __name__ == '__main__':
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num                               # 원소 수가 num인 배열을 생성
    
    
    print('배열 데이터를 오름차순으로 입력하세요.')
    
    x[0] = int(input('x[0]: '))                     # 배열 초기화
    
    for i in range(1, num):
        while True:
            x[i] = int(input(f'x[{i}]: '))
            if x[i] >= x[i - 1]:                   # 바로 직전에 입력한 원솟값보다 큰 값을 입력
                break                              # 조건이 성립되면 다음 작업 수행
    
    
    ky = int(input('검색할 값을 입력하세요.: '))    # 검색할 키값 ky를 입력
    
    
    idx = bin_search(x, ky)                         # ky값과 같은 원소를 x에서 검색

    
    if idx == -1:
        print('검색값을 갖는 원소가 존재하지 않습니다.')
    else:
        print(f'검색값은 x[{idx}]에 있습니다.')
```
