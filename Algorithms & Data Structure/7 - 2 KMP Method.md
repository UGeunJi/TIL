브루트 포스법은 일치하지 않는 문자를 만나면 다시 패턴의 첫 문자부터 검사를 수행하지만, 이와 달리 KMP법은 검사한 결과를 효율적으로 사용할 수 있는 알고리즘입니다.

## KMP법 알아보기

KMP법은 **건너뛰기 표**(skip table)검사했던 결과를 버리지 않고 효율적으로 활용하는 알고리즘입니다.

```python
# KMP법으로 문자열 검색하기

def kmp_match(txt: str, pat: str) -> int:
    """KMP법으로 문자열 검색"""
    pt = 1                        # txt를 따라가는 커서
    pp = 0                        # pat를 따라가는 커서
    skip = [0] * (len(pat) + 1)   # 건너뛰기 표

    # 건너뛰기 표 만들기
    skip[pt] = 0
    while pt != len(pat):
        if pat[pt] == pat[pp]:
            pt += 1
            pp += 1
            skip[pt] = pp
        elif pp == 0:
            pt += 1
            skip[pt] == pp
        else:
            pp = skip[pp]                    # skip한 곳부터 탐색하도록

    # 문자열 검색하기
    pt = pp = 0
    while pt != len(txt) and pp != len(pat):
        if txt[pt] == pat[pp]:
            pt += 1
            pp += 1
        elif pp == 0:
            pt += 1
        else:
            pp = skip[pp]

    return pt - pp if pp == len(pat) else -1

if __name__ == '__main__':
    s1 = input('텍스트를 입력하세요.: ')      # 텍스트용 문자열
    s2 = input('패턴를 입력하세요.: ')        # 패턴용 문자열

    idx = kmp_match(s1, s2)                  # 문자열 s1 ~ s2까지 KMP법으로 검색

    if idx == -1:
        print('텍스트 안에 패턴이 존재하지 않습니다')
    else:
        print(f'{(idx + 1)}번째 문자가 일치합니다.')
```

```
텍스트를 입력하세요.: FNLAWOAWWANFS
패턴를 입력하세요.: AN
10번째 문자가 일치합니다.
```

- 이 알고리즘은 복잡할 뿐 보이어-무어법보다 성능면에서 같거나 오히려 낮은 수준
- 따라서 KMP법은 별로 사용하지 않음
