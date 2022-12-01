## 재귀 알아보기

어떠한 이벤트에서 자기 자신을 포함하고 다시 자신을 사용하여 정의되는 경우 재귀(recursive)라고 합니다.

#### 자연수의 정의

- 1은 자연수입니다.
- 어떤 자연수의 바로 다음 수도 자연수입니다.

무한히 존재하는 자연수를 재귀적 정의(recursive definition)를 사용해서 위의 두 문장으로 정의했습니다.

### 팩토리얼 알아보기

팩토리얼 n!의 정의(n은 양의 정수)

- 0! = 1
- n > 0이면 n! = n x (n - 1)!

```python
# 양의 정수 n의 팩토리얼 구하기

def factorial(n: int) -> int:
    """양의 정수 n의 팩토리얼값을 재귀적으로 구함"""
    if n > 0:
        return n * factorial(n - 1)
    else:
        return 1

if __name__=='__main__':
    n = int(input('출력할 팩토리얼값을 입력하세요.: '))
    print(f'{n}의 팩토리얼은 {factorial(n)}입니다.')
```

```
출력할 팩토리얼값을 입력하세요.: 4
4의 팩토리얼은 24입니다.
```

#### 보충 수업 5 - 1 math.factorial() 함수

파이썬에서 팩터리얼 값을 구하는 표준 라이브러리로 math 모듈에서 factorial() 함수를 제공합니다. 예를 들어 math.factorial(x)는 정수 x의
팩토리얼값을 반환합니다. x가 아니거나 음수라면 ValueError 예외 처리를 내보냅니다.

### 유클리드 호제법(Euclidean Algorithm) 알아보기

```python
# 유클리드 호제법으로 최대 공약수 구하기

def gcd(x: int, y: int) -> int:
    """정수값 x와 y의 최대 공약수를 반환"""
    if y == 0:
        return x
    else:
        return gcd(y, x % y)

if __name__ == '__main__':
    print('두 정숫값의 최대 공약수를 구합니다.')

x = int(input('첫 번째 정숫값을 입력하세요.: '))
y = int(input('두 번째 정숫값을 입력하세요.: '))

print(f'두 정숫값의 최대 공약수는 {gcd(x, y)}입니다.')
```

```
두 정숫값의 최대 공약수를 구합니다.
첫 번째 정숫값을 입력하세요.: 11
두 번째 정숫값을 입력하세요.: 22
두 정숫값의 최대 공약수는 11입니다.
```

#### 보충 수업 5 - 2 math.gcd() 함수

파이썬에서는 최대 공약수를 구하는 표준 라이브러리로 math 모듈에서 gcd()함수를 제공합니다. 예를 들어 math.gcd(a, b)는 정수 a와 b의 최대
공약수를 반환합니다. a, b가 0이 아닌 경우 gcd(a, b)의 값은 a와 b 모두를 나누어 떨어지게 하는 가장 큰 정수를 반환합니다.