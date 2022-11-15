### 삼항 연산자 a if b else c

```py
a = x if x > y else y
print('c는 0입니다.' if c == 0 else 'c는 0이 아닙니다.')
```

```py
# 실습 1-9 정수의 합 구하기

print('a부터 b까지 정수의 합을 구합니다.')
a = int(input('정수 a를 입력하세요.: '))
b = int(input('정수 a를 입력하세요.: '))

if a > b:
    a, b = b, a    # a와 b를 오름차순으로 정렬
    
sum = 0
for i in range(a, b + 1):
    sum += i

print(f'{a}부터 {b}까지 정수의 합은 {sum}입니다.')
```

```py
# 실습 1 - 12 '+' '-' 번갈아 출력하기

print('+와 -를 번갈아 출력합니다.')
n = int(input('몇 개를 출력할까요?'))

for i in range(n):
    if i % 2:              # i % 2 != 0이면, 즉, 나머지가 존재하면
        print('-', end = '')
    else:
        print('+', end = '')
        
print()
```

### 2가지 문제점
- 반복할 때마다 if문을 수행해서 비효율적
- 상황에 따라 유연하게 수정하기 어렵다.

```py
# 실습 1 - 13  (실습 1 - 12) 개선 코드

print('+와 -를 번갈아 출력합니다.')
n = int(input('몇 개를 출력할까요?: '))

for _ in range(n // 2):
    print('+-', end = '')
    
if n % 2:
    print('+', end = '')
    
print()
```

if 문을 반복문에서 수행하지 않으므로 효율적이며 개수에 따라 마지막에 홀수이면 +만 추가해줌으로써 해결

```py
for i in range(1, 10):
    for j in range(1, 10):
        print(f'{i * j:5}', end = '')
    print()
```

```py
n = int(input())

for i in range(n):
    for j in range(i + 1):
        print('*', end = '')
    print()
```

```py
n = int(input())

for i in range(n):
    for j in range(n - i - 1):
        print(' ', end = '')
    for k in range(i + 1):
        print('*', end = '')
    print()
```
