리스트 마지막 원소에 ,(comma) 붙여도 됨

- 튜플은 원소가 하나일 땐 ,(comma) 무조건 붙여줘야 됨
- 안 붙여주면 단순 변수로 취급됨

#### list 패턴 중, list[::-1] **기억**
- 원소들 역순으로 나열해주는 것

- 뮤터블 자료형: 리스트, 딕셔너리, 집합 등이 있으며 값을 변경할 수 있습니다.
- 이뮤터블 자료형: 수, 문자열, 튜플 등이 있으며 값을 변경할 수 없습니다.

---

## 자료구조: 데이터 단위와 데이터 자체 사이의 물리적 또는 논리적인 관계

### 배열 원소의 최댓값을 구하는 함수 구현하기

```py
from typing import Any, Sequence

def max_of (a: Sequence) -> Any:
    """시퀀스형 a 원소의 최댓값을 반환"""
    maximum = a[0]
    for i in range(1, len(a)):
        if a[i] > maximum:
            maximum = a[i]
    return maximum

if __name__ == '__main__':
    print('배열의 최댓값을 구합니다.')
    num = int(input('원소 수를 입력하세요.: '))
    x = [None] * num # 원소 수가 num인 리스트를 생성
    
    for i in range(num):
        x[i] = int(input(f'x[{i}]값을 입력하세요.: '))
                         
    print(f'최댓값은 {max_of(x)}입니다.')
```

- Any는 제약이 없는 임의의 자료형을 의미하며, Sequence는 시퀀스형을 의미합니다.
- 또한 시퀀스형에는 리스트형, 바이트 배열형, 문자열형, 튜플형, 바이트열형이 있습니다.

### 베열의 원솟값을 난수로 결정하기

# 위에서 만든 max 함수 사용
```py
import random

print('난수의 최댓값을 구합니다.')
num = int(input('난수의 개수를 입력하세요.: '))
lo = int(input('난수의 최솟값를 입력하세요.: '))
hi = int(input('난수의 최댓값를 입력하세요.: '))
x = [None] * num

for i in range(num):
    x[i] = random.randint(lo, hi)
    
print(f'{(x)}')
print(f'이 가운데 최댓값은 {max_of(x)}입니다.')

### 10진수 정숫값을 입력받아 2 ~ 36진수로 변환하여 출력하기

def card_cov(x: int, r: int) -> str:
    """정수값 x를 r진수로 변환한 뒤 그 수를 나타내는 문자열을 반환"""
    
    d = ''
    dchar = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    while x > 0:
        d += dchar[x % r]  # 해당하는 문자를 꺼내 겹합
        x //= r
        
    return d[::-1] # 역순으로 반환
```
```py
if __name__ == '__main__':
    print('10진수를 n진수로 변환합니다.')
    
    while True:
        while True:     # 음이 아닌 정수를 입력받음
            no = int(input('변환할 값으로 음이 아닌 정수를 입력하세요.: '))
            if no > 0:
                break
                
        while True:     # 2 ~ 36진수의 정숫값을 입력받음
            cd = int(input('어떤 진수로 변환할까요?: '))
            if 2 <= cd <= 36:
                break
                
        print(f'{cd}진수로는 {card_cov(no, cd)}입니다.')
        
        retry = input( "한 번 더 변환할까요?(Y - 네 / N - 아니요): ")
        if retry in {'N', 'n'}:
            break
```
### 소수 나열하기
```py
counter = 0

for n in range(2, 1001):
    for i in range(2, n):
        counter += 1
        if n % i == 0:
            break
            
    else:
        print(n)
print(f'나눗셈을 실행한 횟수: {counter}')
```

- n이 2와 3으로 나누어 떨어지지 않는다면 2 * 2 = 4와 2 * 3 = 6으로도 나누어 떨어지지 않는 것을 알 수 있습니다.
- 즉, 이 프로그램은 불필요한 나눗셈을 계속 실행하고 있는 것입니다.

### 개선된 알고리즘 1
```py
counter = 0
ptr = 0
prime = [None] * 500

prime[ptr] = 2
ptr += 1

for n in range(3, 1001, 2):
    for i in range(1, ptr):
        counter += 1
        if n % prime[i] == 0:
            break
            
    else:
        prime[ptr] = n
        ptr += 1
        
for i in range(ptr):
    print(prime[i])

print(f'나눗셈을 실행한 횟수: {counter}')

나눗셈을 실행한 횟수: 78022 -> 14622
```

### 개선된 알고리즘 2
```py
counter = 0
ptr = 0
prime = [None] * 500

prime[ptr] = 2
ptr += 1

prime[ptr] = 3
ptr += 1

for n in range(5, 1001, 2):
    i = 1
    while prime[i] * prime[i] <= n:
        counter += 2
        if n % prime[i] == 0:
            break
        i += 1
    else:
        prime[ptr] = n
        ptr += 1
        counter += 1
        
for i in range(ptr):
    print(prime[i])
print(f'곱셈과 나눗셈을 실행한 횟수: {counter}')
```
### 나눗셈을 실행한 횟수: 78022 -> 14622 -> 3774
