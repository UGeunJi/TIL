배열에서 검색하는 방법 중 가장 기본적인 알고리즘은 선형 검색입니다. 이 알고리즘은 4장에서도 사용하므로 확실하게 알아 둡시다.

# 선형 탐색 

선형 검색이란 직선 모양(선형)으로 늘어선 배열에서 검색하는 경우에 원하는 키값을 가진 원소를 찾을 때까지 맨 앞부터 스캔하여 순서대로 검색하는 알고리즘입니다.

## while 문으로 작성한 선형 검색 알고리즘
```py
from typing import Any, Sequence

def seq_search(a: Sequence, key: Any) -> int:
    """시퀀스 a에서 key와 값이 같은 원소를 선형 검색(while문)"""
    i = 0
    
    while True:
        if i == len(a):
            return -1     # 검색에 실패하여 -1을 반환
        if a[i] == key:
            return i      # 검색에 성공하여 현재 검사한 배열의 인덱스를 반환
        i += 1                                                                            # 선형 검색의 핵심 코드
        
if __name__ == '__main__':
    num = int(input('원소 수를 입력하세요.: '))  # num값을 입력받음
    x = [None] * num                            # 원소 수가 num인 배열을 생성
    
    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))
        
    
    ky = int(input('검색할 값을 입력하세요.: '))  # 검색할 키 ky를 입력받음
    
    idx = seq_search(x, ky)
    
    if idx == -1:
        print('검색값을 갖는 원소가 존재하지 않습니다.')
    else:
        print(f'검색값은 x[{idx}]에 있습니다.')                                         
```
## for 문으로 작성한 선형 검색 알고리즘
```py
from typing import Any, Sequence

def seq_search(a: Sequence, key: Any) -> int:
    """시퀀스 a에서 key와 값이 같은 원소를 선형 탐색(for 문)"""
    for i in range(len(a)):
        if a[i] == key:
            return i   # 검색 성공(인덱스를 반환)
    return -1          # 검색 실패(-1을 반환)            # 나머지 코드 생략 (출력 결과를 알기 위한 코드일 뿐이다)
```

---

# 보초법

앞에서 설명했듯이 선형 검색은 반복할 때마다 2가지 종료 조건을 체크합니다. 단순한 판단이지만 이 과정을 계속 반복하면 종료 조건을 검사하는
비용을 무시할 수 없습니다. 이 비용을 반으로 줄이는 방법이 앞으로 배울 보초법(Sentinel method)입니다.

배열 원소 a[0] ~ a[6]은 원래 데이터입니다. 그리고 검색하고자 하는 키값을 배열의 맨 끝 a[7]에 저장합니다. 이때 저장하는 값을 보초(Sentinel)
라고 합니다. 보초는 다음과 같이 검색하는 키와 같은 값으로 추가합니다.

- 2를 추가: 2를 검색하려고 준비, a[7]에 보초 2를 추가합니다.
- 5를 추가: 2를 검색하려고 준비, a[7]에 보초 5를 추가합니다.    

## 선형 검색 알고리즘을 보초법으로 수정
```py
from typing import Any, Sequence
import copy

def seq_search(seq: Sequence, key: Any) -> int:
    """시퀀스 sseq에서 key와 일치하는 원소를 선형 검색(보초법)"""
    a = copy.deepcopy(seq)  # seq를 복사
    a.append(key)           # 보초 key를 추가
    
    i = 0
    while True:
        if a[i] == key:
            break
        i += 1
    return -1 if i ==len(seq) else i                                     # 핵심 코드

if __name__ == '__main__':
    num = int(input('원소 수를 입력하세요.: '))    # num값을 입력
    x = [None] * num                              # 원소 수가 num인 배열을 생성
    
    
    for i in range(num):
        x[i] = int(input(f'x[{i}]: '))             
    
    
    ky = int(input('검색할 값을 입력하세요.: '))   # 검색할 키 ky를 입력받기
    
    
    idx = seq_search(x, ky)
    
    
    if idx == -1:
        print('검색값을 갖는 원소가 존재하지 않습니다.')
    else:
        print(f'검색값은 x[{idx}]에 있습니다.')
```
