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
