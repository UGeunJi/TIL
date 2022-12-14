## 문자열 검색이란?

**문자열 검색**은 어떤 문자열 안에 다른 문자열이 포함되어 있는지 검사하고, 만약 포함되어 있다면 어디에 위치하는지 찾아내는 것을 말합니다.

검색되는 쪽의 문자열을 **텍스트**, 찾아내는 문자열을 **패턴**이라고 합니다.

## 브루트 포스법 알아보기

문자열 검색 알고리즘 중에서 가장 기초적인 검색법입니다. 이 방법은 선형 검색을 단순하게 확장한 알고리즘이라서 **단순법**이라고 합니다.

#### 검사한 위치를 기억하지 못하므로 브루트 포스법은 효율이 좋지 않습니다.

```python
# 브루트 포스법으로 문자열 검색하기

def bf_match(txt: str, pat: str) -> int:
    """브루트 포스법으로 문자열 검색"""
    pt = 0                                       # txt를 따라가는 커서
    pp = 0                                       # pat를 따라가는 커서

    while pt != len(txt) and pp != len(pat):     # 아예 못찾았거나 찾았을 때
        if txt[pt] == pat[pp]:
            pt += 1                              # 문자열이 일치하면 1씩 더해줌
            pp += 1
        else:
            pt = pt - pp + 1                     # 일치하지 않으면 pt는 다음 칸부터 다시 수색
            pp = 0                               # pp는 초기화

    return pt - pp if pp == len(pat) else -1     # pt - pp: 찾았을 때, -1: 못찾았을 때

if __name__ == '__main__':
    s1 = input('텍스트를 입력하세요.: ')       # 텍스트용 문자열
    s2 = input('패턴를 입력하세요.: ')         # 패턴용 문자열

    idx = bf_match(s1, s2)                    # 문자열 s1 ~ s2를 브루트 포스법으로 검색

    if idx == -1:
        print('텍스트 안에 패턴이 존재하지 않습니다')
    else:
        print(f'{(idx + 1)}번째 문자가 일치합니다.')
```

```
텍스트를 입력하세요.: BMLAWHILAWF
패턴를 입력하세요.: LA
3번째 문자가 일치합니다.
```

### 멤버십 연산자와 표준 라이브러리를 사용한 문자열 검색

멤버십 연산자

- in
- not in

find, index 계열 함수로 구현하기

- str.find(sub[, start [, end]]) $~~~$ - sub의 가장 작은 인덱스 반환(그렇지 않으면 -1 반환)
- str.rfind(sub[, start [, end]]) $~~~$ - sub의 가장 큰 인덱스 반환(그렇지 않으면 -1 반환)
- str.index(sub[, start [, end]]) $~~~$ - sub의 가장 작은 인덱스 반환(그렇지 않으면 ValueError 반환)
- str.rindex(sub[, start [, end]]) $~~~$ - sub의 가장 큰 인덱스 반환(그렇지 않으면 ValueError 반환)

with 계열 함수로 구현하기

- str.startwith(prefix[, start [, end]]) $~~~$ - 문자열이 prefix로 시작하면 True, 그렇지 않으면 False
- str.endwith(suffix[, start [, end]]) $~~~$ - 문자열이 suffix로 끝하면 True, 그렇지 않으면 False
