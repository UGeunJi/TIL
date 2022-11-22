## Pandas 개요
- pandas는 for문을 사용하지 않고 데이터를 처리한다거나 배열 기반의 함수를 제공하는 등 NumPy의 배열 기반 계산 스타일을 많이 차용
- pandas가 NumPy 스타일을 많이 차용했지만 가장 큰 차이점은 pandas는 표 형식의 데이터나 다양한 형태의 데이터를 다루는 데 초점을 맞춰 설계
- 그에 비해 NumPy는 단일 산술 배열 데이터를 다루는 데 특화
- 고수준의 자료구조를 제공하고 파이썬 생태계 내의 다른 분석 라이브러리 등과 함께 사용

## 1. Pandas 자료구조
```py
import pandas as pd
import numpy as np
```
### 1.1 Series
- 1차원 데이터
```py
obj = pd.Series([4, 6, 12, -2, 21])
obj
```
```py
obj.values
```
```py
obj.index
```
```py
type(obj)
```
```py
obj2 = pd.Series([4, 7,-5, 3], index = ['d', 'b', 'a', 'c'])
obj2
```
```py
obj2.index
```
```py
obj2.values
```
```py
obj2['d']  # label 이름으로 색인
```
```py
obj2[2]   # 정수로 색인
```
```py
obj2[[0, 1, 3]] # 팬시 색인 (정수로)
```
```py
obj2[['d', 'c', 'c']]   # 팬시 색인 (라벨로)
```
```py
obj2 > 0
```
```py
obj2[obj2 > 0]   # boolean 색인
```
```py
obj2 * 2 # broadcasting
```
```py
np.exp(obj2)  # universal function
```
```py
sdata = {'Ohio': 3500, 'Texas': 71000, 'Oregon': 16000, 'Utah': 5000}
obj3 = pd.Series(sdata)
obj3
```
```py
states = ['Califonia', 'Ohio', 'Oregon', 'Texas']
obj4 = pd.Series(sdata, index = states)
obj4           # NaN: Not a Number
```
```py
pd.isnull(obj4)  # obj4.isnull
```
```py
pd.isnull(obj4).sum() # null인 항목의 합
```
```py
pd.notnull(obj4)
```
```py
obj4.index
```
```py
obj4.values
```
```py
obj4.name = 'population'
obj4
```
```py
obj4.index.name = 'state'
obj4
```
```py
obj
```
```py
obj.index = ["Bob", "Joe", "Sea", "Bare", "Hurry"]
obj
```

### Workshop

- 딕셔너리 -> 시리즈 변환 (index, values 출력)

```py
dict_data = {'a': 1, 'b': 2, 'c': 3}
```
```py
pd.Series(dict_data)
```

- 리스트 -> 시리즈 변환 (index, values 출력)

```py
list_data = ['2019-01-02', 3.14, 'ABC', 100, True]
```
```py
pd.Series(list_data)
```

- 튜플 -> 시리즈 변환 (index, values 출력)

```py
tuple_data = ('영인', '2010-05-01', '여', True)
```
```py
sr = pd.Series(tuple_data)
```
```py
sr.index
```
```py
sr.values
```

- 튜플 -> 시리즈 변환 (index 설정)

```py
tuple_data = ('영인', '2010-05-01', '여', True)
index_name = ['이름', '생년월일', '성별', '학생여부']
```
```py
sr = pd.Series(tuple_data, index = index_name)
```
```py
# 색인을 통해 '영인'값이 나오도록

pd.Series(tuple_data[0])
```

- 시리즈 원소 선택

```py
# 슬라이스 색인을 통해 '2010-05-01', '여' 값이 나오도록
pd.Series(tuple_data[1:3])
```
```py
sr.index
```
```py
sr.values
```
```py
sr['이름']
```
```py
sr[1:3]
```
```py
sr['생년월일':'성별']
```
### 1.2 DataFrame
- 2차원 데이터

```py
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'], 'year': [2000, 2001, 2002, 2001, 2002, 2003], 
        'pop':[1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}
frame = pd.DataFrame(data)
frame
```
```py
frame.index
```
```py
frame.columns
```
```py
frame.values
```
```py
type(frame)
```
```py
frame.head(3)  # 전체 데이터 중 앞에서부터 5행만 보여줌 - 숫자 설정으로 현재는 3행만
```
```py
frame.tail(3)  # 전체 데이터 중 뒤에서부터 5행만 보여줌 - 숫자 설정으로 현재는 3행만
```
```py
frame
```
```py
pd.DataFrame(data, columns = ['year', 'state', 'pop'])  # 컬럼 이름 바꾸기
```
```py
pd.DataFrame(data, columns = ['year', 'state', 'pop', 'debt'])  # 컬럼 추가하기
```
```py
frame2 = pd.DataFrame(data, columns = ['year', 'state', 'pop', 'debt'], index = ['one', 'two', 'three', 'four', 'five', 'six'])  # 컬럼 추가하기
```
```py
frame2
```
```py
frame2.columns
```
```py
frame2.index
```
```py
frame2.values
```

**(1) 열 색인**

```py
frame2['state'] # 2차원 데이터인 DataFrame을 색인하면 1차원 데이터인 Series
```

**(2) 행 색인**

```py
frame2
```
```py
frame2['one'] # error!
```
```py
frame2.loc['one'] # 1차원 Series 데이터
```
```py
type(frame2.loc['one'])
```
```py
frame2
```
```py
frame2.loc['one':'two']
```
```py
frame2['one':'two']  # 슬라이싱을 통해서 행을 가져올 때는 loc를 안써도 선택이 됨
```
```py
frame2['debt'] = 16.5 # 브로드캐스팅
frame2
```
```py
frame2['debt'] = np.arange(6)
frame2
```
```py
sr = pd.Series([1, 2, 3, 4, 5, 6], index = ['one', 'two', 'three', 'four', 'five', 'six'])
```
```py
frame2['debt'] = sr
frame2
```
```py
sr = pd.Series([1, 3, 5], index = ['one', 'three', 'five'])
frame2['debt'] = sr
frame2
```
```py
pop = {'Nevada': {2001: 2.4, 2002: 2.9}, 'Ohio': {2000: 1.5, 2001: 1.7, 2002: 3.6}}
frame3 = pd.DataFrame(pop)
frame3
```
```py
frame3.T
```
```py
pd.DataFrame(pop, index=[2001, 2002, 2003])
```
```py
frame3.name = 'population'
frame3
```
```py
frame3.index.name = 'year'
frame3.columns.name= 'state'

frame3
```

### 1.3 Index
- 컬럼명, 인덱스 (데이터과 행과 열을 알려주는 메타 데이터) 

```py
obj = pd.Series(range(3), index=['a', 'b', 'c'])
obj
```
```py
obj.index
```
```py
obj.index[:2]
```
```py
labels = pd.Index(np.arange(3))
pd.Series([1, 2, 3], index = labels)
```

### Workshop

- 딕셔너리 -> 데이터프레임

```py
dict_data = {'c0':[1,2,3], 'c1':[4,5,6], 'c2':[7,8,9], 'c3':[10,11,12], 'c4':[13,14,15]}
```
```py
pd.DataFrame(dict_data)
```
- 행인덱스/열이름 설정

```py
df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])
df
```
```py
# 준서, 예은 -> 학생1, 학생2

df.index = ['학생1', '학생2']
df
```
```py
# 나이, 성별, 학교 -> 연령, 남녀, 소속

df.columns = ['연령', '남녀', '소속']
df
```
```py
# 행인덱스/열이름 변경
# rename 사용하여 변경 (부분적으로 수정하고 싶을 때)

df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])
df
```
```py
df.rename(index = {'준서': '학생1', '예은': '학생2'}, inplace = True)

df
```
```py
df.rename(columns = {'나이': '연령', '성별': '남녀', '학교': '소속'}, inplace = True)
df
```
```py
df = pd.DataFrame([[15, '남', '덕영중'], [17, '여', '수리중']], 
                   index=['준서', '예은'],
                   columns=['나이', '성별', '학교'])
df
```
```py
df.rename(index = {'준서': '학생1', '예은': '학생2'}, columns = {'나이': '연령', '성별': '남녀', '학교': '소속'})
```
## 2. 중요한 기능들

### 2.1 재색인 
```py
sr = pd.Series([1, 2, 3, 4], index = [0, 3, 4, 5])
sr
```
```py
np.arange(6)
```
```py
sr.reindex(np.arange(6), method = 'bfill')
```
```py
sr.reindex(np.arange(6), method = 'ffill')
```
### 2.2 로우나 컬럼 삭제하기
```py
obj = pd.Series(np.arange(5), index=['a', 'b', 'c', 'd', 'e'])
obj
```
```py
obj.drop('c')
```
```py
obj.drop(['c', 'd'])
```
```py
data = pd.DataFrame(np)
```
```py
data = pd.DataFrame(np.arange(16).reshape(4, 4),
                   index = ['Ohio', 'Colorado', 'Utah', 'New York'],
                   columns = ['one', 'two', 'three', 'four'])
data
```
```py
# axis = 0 (행축), axis = 1(열축)
# (1) drop 연산을 할 경우에는 지정된 "축을" 삭제
# (2) 통계/수학 메서드(sum, mean...)를 사용할 때는 "축을 따라서~" 계산

# 아래 세 라인은 모두 동일한 결과임
data.drop('Colorado') # axis = 0이 default value
data.drop('Colorado', axis = 0) # 행축을 삭제
data.drop('Colorado', axis = 'index') # 행축을 삭제
```
```py
data.drop('two', axis = 1)
data.drop('two', axis = 'columns')
```
```py
data.drop(['two', 'four'], axis = 'columns')
```
### 2.3 색인하기, 선택하기, 거르기
```py
data = pd.DataFrame(np.arange(16).reshape(4, 4),
                   index = ['Ohio', 'Colorado', 'Utah', 'New York'],
                   columns = ['one', 'two', 'three', 'four'])
data
```
```py
data['two']   # data.two와 동일
```
```py
data[['two', 'four']]
```
```py
data.two
```
```py
data['four is']
```
```py
data[['two', 'four']]
```
```py
data[data < 5] = 0
data
```

- loc, iloc
```py
data.loc['Colorado']['one']   # 라벨 색인
```
```py
data.iloc[1][0]   # 정수로 색인
```
```py
data.loc['Colorado'][['one', 'three']]
```
```py
data.loc['Colorado', ['one', 'three']]
```
```py
data.iloc[1, [0, 2]]
```
```py
data.loc[:'Utah']
```
```py
data.iloc[:3]
```
### Workshop

- 행삭제

```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '서준'행 삭제

df.drop('서준')
```
```py
# '서준', '우현' 행 삭제

df.drop(['서준', '우현'])
```
- 열 삭제
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '수학' 열 삭제
df.drop('수학', axis = 1)
```
```py
# '수학', '영어' 열 삭제
df.drop(['수학', '영어'], 1)
```
- 행 선택
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '서준' 행 선택(라벨 색인, 정수 색인)
df.loc['서준']
```
```py
# '서준', '우현' 행 선택 (라벨 색인, 정수 색인, 슬라이싱)
df.loc[['서준', '우현']]
```
```py
df.iloc[[0, 1]]
```
```py
df.loc['서준':'우현']
```
```py
df.iloc[:2]
```
- 열 선택
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '수학' 열 선택
df['수학']
```
```py
# '음악', '체육' 열 선택
df[['음악', '체육']]
```

- 원소 선택
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '서준'의 '음악' 점수
df.loc['서준'][['음악']]
```
```py
#'서준'의 '음악','체육' 점수
df.loc['서준'][['음악', '체육']]
```
```py
#'서준','우현'의 '음악','체육' 점수
df.loc[['서준', '우현']][['음악', '체육']]
```
- 열 추가
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '국어' 열 추가, 값은 80 점 지정
df['국어'] = 80
df
```
- 행 추가
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# "본인 이름" 으로 행추가, 과목 점수도 지정
df.loc['우근'] = (100, 100, 100, 100)
df
```
- 원소 값 변경
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
# '서준'의 '체육' 점수를 80 점으로 변경(라벨 색인, 정수 색인)
df.loc['서준'][['체육']] = 80
df
```
```py
# '서준'의 '음악','체육' 점수 변경
df.loc['서준'][['음악', '체육']] = (80, 100)
df
```
- 행, 열 바꾸기
```py
exam_data = {'수학' : [ 90, 80, 70], '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100], '체육' : [ 100, 90, 90]}

df = pd.DataFrame(exam_data, index=['서준', '우현', '인아'])
df
```
```py
df.T
```
```py
exam_data = {'이름' : [ '서준', '우현', '인아'],
             '수학' : [ 90, 80, 70],
             '영어' : [ 98, 89, 95],
             '음악' : [ 85, 95, 100],
             '체육' : [ 100, 90, 90]}
df = pd.DataFrame(exam_data)
df
```
```py
df.set_index(['이름'], inplace = True)
df
```
```py
df.reindex(['인아', '서준', '우현', '우근'])

df
```
```py
df.reset_index()
```
```py
data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9]}
frame2 = pd.DataFrame(data, columns=['year', 'state', 'pop', 'debt'],
                      index=['one', 'two', 'three', 'four', 'five'])
frame2
```
```py
frame2['state']
```
```py

frame2[['state', 'pop', 'debt']]
```
```py
frame2.loc['two']
```
```py
frame2.loc['two':'four']
```
```py
from IPython.display import Image
Image('./images/image7.png', width=400)
```
```py
frame2.loc[['three', 'four'], ['pop', 'debt']]
```
```py
frame2[['pop', 'debt', 'state']]
```
```py
frame2.loc[['three', 'four', 'two']]
```
```py
import numpy as np
import pandas as pd
```
## 3. 산술 연산과 데이터 정렬
```py
s1 = pd.Series([7.3, -2.5, 3.4, 1.5], index=['a', 'c', 'd', 'e'])
s2 = pd.Series([-2.1, 3.6, -1.5, 4, 3.1], index = ['a', 'c', 'e', 'f', 'g'])

s1
```
```py
s2
```
```py
s1 + s2      # 한 쪽이라도 정보가 없으면 NaN 처리됨
```
```py
df1 = pd.DataFrame(np.arange(12).reshape(3, 4), columns = list('abcd'))
df2 = pd.DataFrame(np.arange(20).reshape(4, 5), columns = list('abcde'))
df2.loc[1, 'b'] = np.nan
```
```py
df1
```
```py
df2
```
```py
df1 + df2
```
```py
df1.add(df2, fill_value=0) # 값이 없는 원소들은 0으로 지정을 한 뒤에 add
```
```py
frame = pd.DataFrame(np.arange(12.).reshape((4, 3)),
            columns = list('bde'),
            index = ['Utah', 'Ohio', 'Texas', 'Oregon'])
```
```py
series = frame.iloc[0]
```
```py
frame
```
```py
series
```
```py
frame - series  # 2차원 - 1차원
```
```py
series2 = pd.Series(range(3), index = ['b', 'e', 'f'])
series2
```
```py
frame + series2
```
```py
series3 = frame['d']
series3
```
```py
frame
```
```py
frame - series3
```
```py
frame.sub(series3, axis = 'index') # 2차원 - 1차원
```

## 4. 함수 적용과 매핑
```py
frame = pd.DataFrame(np.arange(12).reshape(4,3), columns= list('bde'),
                     index = ["Utah", "Ohio", "Texas", "Oregon"])
frame
```
```py
frame.sum()  # pandas에서는 numpy와 다르게 axis = 0이 기본값으로 지정
```
```py
frame.sum(axis = 1)
```
```py
frame.sum(axis = 0)
```
```py
# 컬럼명 합계
frame.sum(axis = 'columns')
```
```py
# 행별 합계
np.sum(frame, axis = 1) # numpy도 사용 가능
```
```py
frame.min(axis = 0)
```
```py
frame.max(axis = 1)
```
```py
frame
```
```py
frame.max() - frame.min()
```
```py
# 위의 코드를 나만의 함수로 만들어서 적용 (동일한 결과)
def range_f(x):      # x는 frame을 행축으로 색인한 series
    return x.max() - x.min()

frame.apply(range_f)    # axis = 0 아 기본값
```
### applymap은 모든 원소에 어떤 함수를 적용할 때
```py
x = 0.45678
'%.2f' %x
```
```py
def fmt(x):
    return '%.2f' %x
```
```py
frame.applymap(fmt)   # applymap은 frame 전체 원소에 fmt 함수를 적용
```
```py
lambda x: '%.2f' %x
frame.applymap(lambda x: '%.2f' %x)  # lambda 함수로 대체
```
```py
frame['b'].applymap(fmt)  # series 데이터에는 applymap을 적용할 수 없고, 대신 map 함수를 적용
```
```py
frame['b'].map(fmt)
```
### Workshop
```py
import seaborn as sns # 시각화 모듈

titanic = sns.load_dataset('titanic') # 데이터를 DataFrame으로 반환

type(titanic)
```
```py
# 데이터 훑어보기
titanic.head()
```
- 두 열(age, fare)만 색인해서 DataFrame으로 만들기

```py
df = titanic[['age', 'fare']]
df
```
- 각 열의 최댓값과 최솟값 구하기
```py
df.max(), df.min()
```
- 각 열의 "최댓값과 최솟값의 차이" 구하기 (apply) 함수 이용
```py
def a(x):
    return x.max() - x.min()
```
```py
df.apply(a)
```
- 모든 원소의 format을 소수점 두자리로 맞추기
```py
def b(x):
    return '%.2f' %x
```
```py
df.applymap(b)
```
- 누락된 값(NaN)이 있는지 Boolean value로 확인하기
```py
pd.isnull(df)
```
## 5. 정렬과 순위
```py
obj = pd.Series(np.arange(4), index = ['d', 'a', 'b', 'c'])
obj
```
```py
obj.sort_values()
```
```py
obj.sort_index()
```
```py
frame = pd.DataFrame(np.arange(8).reshape(2, 4), index = ['three', 'one'], columns = ['d', 'a', 'b', 'c'])
frame
```
```py
frame.sort_index(axis = 0) # 인덱스 자체를 정렬
```
```py
frame.sort_index(axis = 1)  # column 자체를 정렬
```
```py
frame = pd.DataFrame({'b':[4, 7, -3, 2], 'c':[0, 1, 0, 1]})
frame
```
```py
frame.sort_values(by = 'b', axis = 0)
```
```py
frame.sort_values(by = 'c', axis = 0)
```
```py
frame.sort_values(by = 'c', axis = 0, ascending = False)
```
```py
frame.sort_values(by = ['c', 'b'], axis = 0)
```

## 6. 중복색인
```py
obj = pd.Series(np.arange(5), index = ['a', 'a', 'b', 'b', 'c'])
obj
```
```py
obj.index
```
```py
obj.index.is_unique
```
```py
obj['a']
```
```py
obj.b
```
```py
obj.c
```
```py
df = pd.DataFrame(np.random.randn(4, 3), index = ['a', 'a', 'b', 'b'])
df
```
```py
df.loc['b']
```

## 7. 기술 통계 계산과 요약
```py
df = pd.DataFrame([[1.4, np.nan], [7.1, -4.5],
                   [np.nan, np.nan], [0.75, -1.3]],
                  index=['a', 'b', 'c', 'd'],
                  columns=['one', 'two'])
df
```
```py
df.sum() # axis = 0 기본값
```
```py
df.sum(axis = 0, skipna = True) # skipna = True 기본값
```
```py
df.sum(axis = 0, skipna = False)
```
```py
df.sum(axis = 1, skipna = False)
```
```py
# numpy: 최댓값 / 최솟값의 위치를 구할 때 argmax(), argmin()
# pandas: 최댓값과 최솟값 위치를 구할 때 idxmax(), idxmin()
```
```py
df.idxmax()
```
```py
df.idxmin()   # 열축 최댓값의 인덱스
```
```py
df.cumsum() # axis = 0이 default   # 열의 누적합 계산
```
```py
df
```
```py
df.describe()
```
```py
obj = pd.Series(['a', 'a', 'b', 'b'] * 4)
obj
```
```py
obj.describe()  # 문자열을 출력하면 다른 요소가 나옴
```
```py
titanic.describe() # 숫자에 관한 정보만 나옴
```
```py
titanic.describe(include = 'all')  # 문자열 정보까지 원할 때
```
### 7.1 상관관계와 공분산
```py
df = pd.DataFrame({"math" : [50, 60, 40, 30, 70, 50], "physics" : [40, 60, 50, 20, 80, 50]})
df
```
### 7.1 상관관계와 공분산
```py
df = pd.DataFrame({"math" : [50, 60, 40, 30, 70, 50], "physics" : [40, 60, 50, 20, 80, 50]})
df
```
- 산포도(산점도)
```py
# pandas, matplotlib, seaborn

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
```py
df.plot(kind = 'scatter', x = 'math', y = 'physics')  # 기본형: 선 그래프
```
- 상관계수
```py
df.corr()
```
### 범주 데이터 요약
```py
titanic = sns.load_dataset('titanic')
titanic.describe()
```
```py
titanic.describe(include = 'object')
```
```py
titanic.head()
```
```py
titanic['embarked'].unique()  # unique한 원소들
```
```py
titanic['embarked'].nunique()  # unique한 원소들의 개수
```
```py
titanic['embarked'].value_counts()  #  고유값(unique한 원소들)의 빈도수(건수)
```
```py
pd.value_counts(titanic['embarked'])
```
```py
titanic['embarked'].hist()
```

## 8. 데이터 로딩과 저장
```py
import pandas as pd
import numpy as np
```
```py
!ls examples
```
```py
df = pd.read_csv('./examples/ex1.csv')
df
```
```py
df.columns
```
```py
pd.read_table('./examples/ex1.csv', sep = ',')
```
```py
pd.read_csv('./examples/ex2.csv', header = None)  # 1행을 header로 가져오는 것이 default인데, 이것을 해체시킴
```
```py
df = pd.read_csv('./examples/ex2.csv', names = ['a', 'b', 'c', 'd', 'message'])
df
```
```py
names = ['a', 'b', 'c', 'd', 'message']
df = pd.read_csv('./examples/ex2.csv', names = names)
df
```
```py
df.set_index('message')
```
```py
df.reset_index()
```
```py
names = ['a', 'b', 'c', 'd', 'message']
df = pd.read_csv('./examples/ex2.csv', names = names, index_col = 'message')   # 인덱스 이름 동시설정
df
```
```py
names = ['a', 'b', 'c', 'd', 'message']
df = pd.read_csv('./examples/ex2.csv', names = names, index_col = 4)   # 인덱스 숫자로 지정
df
```
```py
df = pd.read_table('./examples/ex3.txt', sep = '\s+')   # 공백 1개 이상의 패턴과 매치시킴
df
```
```py
df = pd.read_csv('./examples/ex2.csv')
df
```
```py
df.to_csv('./examples/out.csv', index = False)
```
```py
pd.read_csv('./examples/out.csv')
```

## 9. 데이터 정제 및 준비

### 9.1 누락된 데이터 처리하기

- 결측치 골라내기
```py
type(np.nan)
```
```py
string_data = pd.Series(['abc', 'def', np.nan, 'ghi'])
string_data
```
```py
pd.isnull(string_data)
```
```py
string_data.isnull()
```
```py
type(None) # 파이썬의 Nonetype 자료형
```
```py
string_data = pd.Series(['abc', 'def', None, 'ghi'])
string_data
```
```py
string_data.isnull()  # None값도 null로 간주됨
```
```py
data = pd.Series([1, np.nan, 3.5, np.nan, 7])
data
```
```py
data.isnull()
```
```py
data[data.isnull()]  # boolean 색인
```
```py
# null인 행을 삭제하고 싶다면 null행의 인덱스를 구해서 drop 함수에 적용
data.drop([1, 3]) # null인 행을 삭제
```
```py
null_idx = data[data.isnull()].index
data.drop(null_idx, axis = 0)
```
```py
# dropna를 사용하면 null인 행을 삭제
data.dropna()  # 위의 과정을 이걸로 대체
```
```py
data = pd.DataFrame([[1.0, 6.5, 3.0],
                     [1.0, np.nan, np.nan],
                     [np.nan, np.nan, np.nan],
                     [np.nan, 6.0, 3.0]])
data
```
```py
data.dropna()  # axis = 0으로 설정되어 있으므로 행을 삭제
               # how = 'any' 설정되어 있으므로 null이 하나라도 있으면 삭제
```
```py
data.dropna(how = 'any')
```
```py
data.dropna(how = 'all')  # 행을 삭제하되, 그 행에 모든 값이 null인 행만 삭제
```
```py
data[100] = np.nan
data
```
```py
data.dropna(axis = 1, how = 'all')  # 열을 삭제하되, 그 열의 모든 값이 null일 경우에 삭제
```
```py
data.dropna(axis = 1, how = 'any') # 열을 삭제하되, 그 열의 값이 하나라도 null일 경우에 삭제
```
```py
df = pd.DataFrame(np.random.randn(7, 3))
df
```
```py
df.iloc[0:4, 1] = np.nan
df.iloc[0:2, 2] = np.nan
df
```
```py
df.dropna() # axis = 0, how = 'any'
```
```py
df.dropna(axis = 1)
```
```py
df.dropna(axis = 1, thresh = 5) # thresh = 5: null이 아닌 데이터가 5개 미만인 데이터만 삭제하기
```
- 결측치 채우기
```py
df.fillna(0)
```
```py
df.fillna({1:0, 2:0.5})  # dictionary를 이용해서 열마다 다른 값으로 대체
```
```py
df.fillna(0, inplace = True)
df
```
```py
df = pd.DataFrame(np.random.randn(6, 3))
df
```
```py
df.iloc[2:, 1] = np.nan
df.iloc[4:, 2] = np.nan
df
```
```py
df.fillna(axis = 0, method = 'ffill')  # axis = 0이므로 "행축을 따라서" 채워넣기
```
```py
df.fillna(axis = 1, method = 'ffill')  # axis = 0이므로 "열축을 따라서" 채워넣기
```
```py
df.fillna(axis = 0, method = 'ffill', limit = 1)
```
```py
m = df.mean(axis = 0).mean()  # 최종 평균
df.fillna(m)
```
### 9.2 데이터 변형 

- 중복 제거하기
```py
data = pd.DataFrame({'k1':['one', 'two']*3 + ['two'],
             'k2':[1, 1, 2, 3, 3, 4, 4]})
data
```
```py
# 중복인지 체크
data.duplicated()
```
```py
data.duplicated(keep='first')
```
```py
data.duplicated(keep='last')
```
```py
data
```
```py
# 중복인지 체크(k1 컬럼 기준으로)
data.duplicated(['k1'])
```
```py
# k1열 기준으로 삭제
data.drop_duplicates(['k1'])
```
```py
data.drop_duplicates(['k1'], keep = 'last')
```
```py
data.duplicated(['k1'], keep = 'last')
```
```py
data['v1'] = range(7)
data
```
```py
data.drop_duplicates()
```
```py
data.drop_duplicates(['k1', 'k2'])
```
- 값 치환하기
```py
data = pd.Series([1, -999, 2, -999, -1000, 3])
data
```
```py
data.replace(-999, np.nan)
```
```py
data.replace([-999, -1000], np.nan)
```
```py
data.replace([-999, -1000], [np.nan, 0])
```
```py
data.replace({-999:np.nan, -1000:0})
```
- 축 색인 이름 바꾸기
```py
data =pd.DataFrame(np.arange(12).reshape(3, 4), index = ['Ohio', 'Colorado', 'New York'], columns = ['one', 'two', 'three', 'four'])
data
```
```py
data.index
```
```py
# option 1
def upper_tx(x):
    return x.upper()
```
```py
data.index.map(upper_tx)
```
```py
# option 2
upper_tx = lambda x:x.upper()
data.index.map(upper_tx)
```
```py
# option 3
data.index.map(lambda x:x.upper())
```
```py
data
```
```py
data.rename(index = {'Ohio':'Indiana'})
```
```py
data.rename(index = str.upper)
```
```py
data.rename(columns = str.upper)
```
```py
data.rename(index = str.upper, columns = str.lower)
```
```py
data.rename(index = str.upper, columns = str.title)
```
- 벡터화된 문자열 함수
```py
data = {'Dave':'dave@gmail.com',
        'Steve': 'steve@gmail.com',
        'Rob':'rob@gmail.com',
        'Wes':np.nan,
        'Puppy':'p',
        'Number':'123'}
sr_data= pd.Series(data)
sr_data
```
```py
sr_data.str.isnumeric()   # 숫자인지 물어봄
```
```py
import numpy as np
import pandas as pd
```

## 10. 데이터 준비하기

### 10.1 계층적 색인
```py
data = pd.Series(np.random.randn(9),
                 index = [['a', 'a', 'a', 'b', 'b', 'c', 'c', 'd', 'd'],
                          [1, 2, 3, 1, 3, 1, 2, 2, 3]])
data
```
```py
data.index
```
```py
data['b']
```
```py
data['b':'c'] # 라벨 색인
```
```py
data.loc['b':'c'] # 라벨색인
```
```py
data.iloc[3:7] # 정수색인
```
```py
data
```
```py
data_unstack = data.unstack()
data_unstack
```
```py
data_stack = data_unstack.stack()
data_stack
```
```py
data_stack.unstack()
```
```py
data_stack.unstack().reset_index()
```
```py
data_unstack.stack().reset_index()
```
### 10.2 데이터 합치기

- 데이터베이스 스타일로 DataFrame 합치기

- inner join
```py
df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                    'data1': range(7)})
df2 = pd.DataFrame({'key': ['a', 'b', 'd'],
                    'data2': range(3)})
```
```py
df1
```
```py
df2
```
```py
pd.merge(df1, df2, on='key', how='inner')
```
```py
# select data1, data1
#   from df1 a
#   inner join df2 b
#     on a.key = b.key;
```
```py
pd.merge(df1, df2, on='key') # how='inner' 가 기본값
```
```py
df3 = pd.DataFrame({'lkey': ['b', 'b', 'a', 'c', 'a', 'a', 'b'], 'data1': range(7)})
df4 = pd.DataFrame({'rkey': ['a', 'b', 'd'], 'data2': range(3)})
```
```py
df3
```
```py
df4
```
```py
pd.merge(df3, df4, left_on='lkey', right_on='rkey')
```
```py
# select data1, data1
#   from df1 a
#   inner join df2 b
#     on a.lkey = b.rkey;
```
- outer join

```py
df1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                    'data1': range(7)})
df2 = pd.DataFrame({'key': ['a', 'b', 'd'],
                    'data2': range(3)})
```
```py
df1
```
```py
df2
```
```py
pd.merge(df1, df2, how='left')
```
```py
pd.merge(df1, df2, how='right')
```
```py
pd.merge(df1, df2, how='outer')
```
- 색인 병합하기
```py
left1 = pd.DataFrame({'key': ['a', 'b', 'a', 'a', 'b', 'c'], 'value': range(6)})
right1 = pd.DataFrame({'group_val': [3.5, 7]}, index=['a', 'b'])
```
```py
left1
```
```py
right1
```
```py
pd.merge(left1, right1, left_on='key', right_index = True) #inner join
```
```py
pd.merge(left1, right1, left_on='key', right_index = True, how='outer') #outer join
```
```py
left2 = pd.DataFrame([[1., 2.], [3., 4.], [5., 6.]],
                     index=['a', 'c', 'e'],
                     columns=['Ohio', 'Nevada'])
right2 = pd.DataFrame([[7., 8.], [9., 10.], [11., 12.], [13, 14]],
                      index=['b', 'c', 'd', 'e'],
                      columns=['Missouri', 'Alabama'])
```
```py
left2
```
```py
right2
```
```py
pd.merge(left2, right2, right_index=True, left_index=True) # how='inner' 기본값
```
```py
# join 함수는 인덱스 값을 기준으로 조인을 함
left2.join(right2, how='inner') # pd.merge(left2, right2, right_index=True, left_index=True)
                                # how='left' 기본값이므로 how='inner'로 바꿔줘야 위와 동일한 결과
```
```py
left1
```
```py
right1
```
```py
pd.merge(left1, right1, left_on='key', right_index = True, how='inner') # inner join
```
```py
left1.join(right1, on='key', how='inner') # 위의 pd.merge와 동일한 결과
```
- 축따라 이어붙이기

**참고** np.concatenate
```py
arr = np.arange(12).reshape(3, 4)
arr
```
```py
np.concatenate([arr, arr], axis=0) # axis=0 기본값, 0번축을 따라서 이어붙힘
```
```py
np.concatenate([arr, arr], axis=1)
```
```py
s1 = pd.Series([0, 1], index=['a', 'b'])
s2 = pd.Series([2, 3, 4], index=['c', 'd', 'e'])
s3 = pd.Series([5, 6], index=['f', 'g'])
```
```py
s1
```
```py
s2
```
```py
s3
```
```py
pd.concat([s1, s2, s3], axis=0)
```
```py
pd.concat([s1, s2, s3], axis=1)
```
```py
df1 = pd.DataFrame(np.random.randn(3, 4), columns=['a', 'b', 'c', 'd'])
df2 = pd.DataFrame(np.random.randn(2, 3), columns=['b', 'd', 'a'])
```
```py
df1
```
```py
df2
```
```py
pd.concat([df1, df2], axis=0)
```
```py
pd.concat([df1, df2], axis=0, ignore_index=True)
```
### Workshop

- 축따라 이어붙이기
```py
df1 = pd.DataFrame({'a': ['a0', 'a1', 'a2', 'a3'],
                    'b': ['b0', 'b1', 'b2', 'b3'],
                    'c': ['c0', 'c1', 'c2', 'c3']},
                    index=[0, 1, 2, 3])
 
df2 = pd.DataFrame({'a': ['a2', 'a3', 'a4', 'a5'],
                    'b': ['b2', 'b3', 'b4', 'b5'],
                    'c': ['c2', 'c3', 'c4', 'c5'],
                    'd': ['d2', 'd3', 'd4', 'd5']},
                    index=[2, 3, 4, 5])
```
```py
df1
```
```py
df2
```
```py
# 2개의 데이터프레임을 위, 아래 (행축으로) 이어붙이듯 연결하기

pd.concat([df1, df2], axis=0)
```
```py
# 인덱스를 재 설정

pd.concat([df1, df2], axis=0, ignore_index=True)
```
```py
# 2개의 데이터프레임을 좌, 우 (열축으로) 이어붙이듯 연결하기

pd.concat([df1, df2], axis=1)

sr1 = pd.Series(['e0', 'e1', 'e2', 'e3'], name='e')
sr2 = pd.Series(['f0', 'f1', 'f2'], name='f', index=[3, 4, 5])
sr3 = pd.Series(['g0', 'g1', 'g2', 'g3'], name='g')
```
```py
# df1과 sr1을 좌, 우(열축으로) 이어붙이듯 연결하기

df1
```
```py
sr1
```
```py
pd.concat([df1, sr1], axis=1)
```
- 데이터베이스 스타일로 DataFrame 합치기
```py
df1 = pd.read_excel('./datasets/stock price.xlsx')
df2 = pd.read_excel('./datasets/stock valuation.xlsx')
```
```py
df1
```
```py
df2
```
```py
# id 를 조인 조건으로 해서 inner join

pd.merge(df1, df2, on='id', how='inner')
```
```py
# 위와 같은 결과, 조인조건에 해당하는 컬럼명이 같으면 생략
pd.merge(df1, df2)
```
```py
# id 를 조인 조건으로 해서 outer join

pd.merge(df1, df2, on='id', how='outer')
```
```py
pd.merge(df1, df2, how='outer')
```
```py
# 왼쪽 데이터프레임(df1)에서는 stock_name, 오른쪽 데이터프레임(df2)에서는 name을 조인조건으로 하되
# left join

pd.merge(df1, df2, left_on='stock_name', right_on='name', how='left')
```
```py
# 왼쪽 데이터프레임(df1)에서는 stock_name, 오른쪽 데이터프레임(df2)에서는 name을 조인조건으로 하되
# right join

pd.merge(df1, df2, left_on='stock_name', right_on='name', how='right')
```

- 색인 병합으로 데이터프레임 합치기
```py
df1 = pd.read_excel('./datasets/stock price.xlsx', index_col = 'id')
df2 = pd.read_excel('./datasets/stock valuation.xlsx', index_col = 'id')
```
```py
df1
```
```py
df2
```
```py
# 데이터프레임 인덱스를 기준으로 병합 (왼쪽 데이터프레임(df1) 기준)

df1.join(df2) # join 함수의 how='left' 가 기본값
```
```py
# 데이터프레임 인덱스를 기준으로 병합 (공통된 인덱스만)

df1.join(df2, how='inner')
```
```py
sr_data.str.isalpha()   # 알파벳인지 물어봄
```
```py
sr_data.str.contains('gmail')  # 어떤 문자열이 들어있는지 물어봄
```
- 데이터 구간 분할
```py
# 수치형 데이터(양적 데이터) -> 범주형 데이터(질적 데이터)
ages = [20, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]
ages
```
```py
bins = [18, 25, 35, 60, 100]
cats = pd.cut(ages, bins, labels = ["Youth", "YoungAdult", "MiddleAged", "Senior"])  # 가장 작은 값에서 큰 값까지 n등분

cats
```
```py
pd.value_counts(cats)
```
```py
cats = pd.cut(ages, 4)
pd.value_counts(cats)
```
```py
qcats = pd.qcut(ages, 4)  # quantile cut
pd.value_counts(qcats)
```
- 특잇값(바깥값, outlier) 찾고 제외하기
```py
data = pd.DataFrame(np.random.randn(1000, 4))
data.describe()
```
```py
# 3보다 큰 값을 특이값(바깥값, outlier)로 가정하고, 해당되는 값을 3으로 치환
data > 3
```
```py
(data > 3).any(axis = 1) # 열축을 따라서 True값이 하나라도 있는지 확인
```
```py
(data > 3).any(axis = 1).sum()
```
```py
data[(data > 3).any(axis = 1)]
```
```py
data[data>3] = 3
```
```py
data.describe()
```
- 더미변수 계산하기(one-hot encoding)
```py
df = pd.DataFrame({'fruit':['apple', 'apple', 'pear', 'peach', 'pear'], 'data':range(5)})
df
```
```py
dummies = pd.get_dummies(df['fruit'], prefix = 'fruit')
dummies
```
```py
pd.concat([df[['data']], dummies], axis = 1)
```
