# 시간 복잡도 계산하기

**시간 복잡도 표기법**

- 빅-오(O(n)): 최악일 때의 연산 횟수를 나타낸 표기법

```python
# 1에서 100 사이의 무작위수를 찾아 출력
import random

findNumber = random.randrange(1, 101) # fineNumber

for i in range(1, 101):  # 1 ~ 100
    if i == findNumber:
        print(i)
        break

# 최선일 때 1 회
# 보통일 때 50회
# 최악일 때 100회: O(n)
```

```
98
```

```python
sum = 0
fact = 1

for i in range(10):
    sum += i

for j in range(1, 11):
    fact *= j

print(sum, fact)

# 시간 복잡도: O(2n) --> O(n)으로 간주
```

```
45 3628800
```

```python
array = [3, 5, 1, 2, 4]   # 5개의 데이터

for i in array:    # array에는 5개의 데이터
    for j in array:   # array에는 5개의 데이터
        temp = i * j
        print(temp)

# 시간 복잡도 --> O(n ** 2)
```

```
9
15
3
6
12
15
25
5
10
20
3
5
1
2
4
6
10
2
4
8
12
20
4
8
16
```

```python
# manatee1 = {"name": "cute", "age": 2, ....}       # 총 m개의 키
# manatee2 = {"name": "handsome", "age": 1, ....}   # 총 m개의 키
# manatee3 = {"name": "pretty", "age": 3, ....}     # 총 m개의 키
# manatees = [manatee1, manatee2, manatee3, ...]   # 총 n마리의 manatee를 저장하는 리스트
```

```python
def example1(manatees):
    for manatee in manatees: # n iterations
        print(manatee['name'])

# 시간 복잡도 --> O(n)

def example2(manatees):
    print(manatees[0]['name'])
    print(manatees[0]['age'])

# 시간 복잡도 --> O(2) --> O(1)

def example3(manatees):
    for manatee in manatees: # n iterations
        for manatee_property in manatee: # m iterations
            print(manatee_property, ": ", manatee[manatee_property])

# 시간 복잡도 --> O(n * m)

def example4(manatees):
    oldest_manatee = "No manatees here!"
    for manatee1 in manatees: # n iterations
        for manatee2 in manatees:# n iterations
            if manatee1['age'] < manatee2['age']:  
                oldest_manatee = manatee2['name']  # 1회 
            else:
                oldest_manatee = manatee1['name']  # 1회   중에 하나
    print(oldest_manatee)

# 시간 복잡도 --> 2 * n ** 2 --> O(n ** 2) or O(n ^ 2)
```
