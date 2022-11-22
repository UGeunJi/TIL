## 자동차 연비 데이터셋

- [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/index.php)의 [
Auto MPG Data Set](https://archive.ics.uci.edu/ml/datasets/auto+mpg)에서 다운로드
 
 
- [Kaggle](https://www.kaggle.com/)의
[Auto-mpg dataset](https://www.kaggle.com/uciml/autompg-dataset)에서 다운로드
```py
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
```
## 1. 데이터 탐색

#### 1.1 데이터 적재
```py
df = pd.read_csv('./Datasets/auto-mpg.csv', header = None)
df
```
#### 1.2 데이터 일부 확인

0. mpg: continuous
1. cylinders: multi-valued discrete
2. displacement: continuous
3. horsepower: continuous
4. weight: continuous
5. acceleration: continuous
6. model year: multi-valued discrete
7. origin: multi-valued discrete
8. car name: string (unique for each instance)
```py
df.head()
```
#### 1.3 열 이름 지정

* 예 : ['mpg','cylinders','displacement','horsepower','weight', 'acceleration','model year','origin','name']
```py
df.rename(columns = {0:'mpg', 1:'cylinders', 2:'displacement', 3:'horsepower', 4:'weight', 5:'acceleration',
                     6:'model year', 7:'origin', 8:'name'}, inplace = True)

df.columns = ['mpg','cylinders','displacement','horsepower','weight', 'acceleration','model year','origin','name']
```
- mpg : 연비
- cylinders : 실린더수 
- displacement : 배기량
- horsepower: 출력
- weight : 차중
- acceleration : 가속능력
- model year : 출시년도
- origin : 제조국 1(USA), 2(EU), 3(JPN)
- name : 모델명

#### 1.4 데이터 형상 확인
```py
df.shape
```
#### 1.5 데이터 요약정보 확인(데이터 타입, 누락정보)
```py
df.info()
```
#### 1.6 데이터 자료형 확인 
```py
df.dtypes
```
#### 1.7 Series(horsepower 열)의 자료형 확인 
```py
df['horsepower'].dtype
```
```py
df['horsepower'].value_counts()
```
```py
df['horsepower'].value_counts().index
```
```py
df['horsepower'].isin(['?']).sum()
```
* (Question) horsepower는 숫자 데이터인데 왜 object 형으로 반환되었을까?
* (Answer) 중간에 6개의 '?'로 인해 object 형으로 반환되었다.

#### 1.8 제조국(origin) 특성의 데이터 분포(건수) 확인하기
- 1(USA), 2(EU), 3(JPN)
```py
df['origin'].unique()
```
```py
df['origin'].nunique()
```
```py
df['origin'].value_counts()
```
```py
df.value_counts('origin')
```
#### 1.9 제조국(origin) 특성을 histogram으로 표현하기
```py
df['origin'].plot(kind = 'hist')
```
```py
df['origin'].hist()
```
#### 1.10 coutry 컬럼 추가하기
* 제조국 1, 2, 3을 각각 "USA", "Europe", "Japan"으로 대체한 값을 새로운 컬럼(country)에 적용하기
```py
df['origin'].replace([1, 2, 3], ['USA', 'Europe', 'Japan'])
```
```py
df['country'] = df['origin'].replace([1, 2, 3], ['USA', 'Europe', 'Japan'])
df
```
* coutry 특성으로 groupby하여 "국가당 몇건"의 샘플이 있는지 확인하기
```py
df.groupby('country').size()
```
```py
df['country'].value_counts()
```
- 위에서 구한 국가당 레코드수를 파이차트 그리기
```py
country = df.groupby('country').size()
type(country)
```
```py
country.plot(kind = 'pie', autopct = '%.1f%%')
```
#### 1.11 국가별(country) mpg 값의 분포를 boxplot으로 확인하기
- (Question) mpg의 중간값이 가장 낮은 국가는?
- (Answer) USA
```py
df['mpg'].median() # 전체 398건에 대한 연비 중앙값
```
```py
df['mpg'].plot(kind = 'box')
```
```py
# (참고) seaborn 모듈에서 범주형 데이터 값에 따른 수치형 데이터 값이 어떠한지 나타내는 그래프
# 막대 그래프(barplot)
# 박스 플롯(boxplot)
# 포인트 플롯(pointplot)
```
#### 제조국(범주형 데이터)에 따른 연비(수치형)를 확인
```py
sns.barplot(data = df, x = 'country', y = 'mpg')
```
```py
sns.pointplot(data = df, x = 'country', y = 'mpg')
```
```py
sns.boxplot(data = df, x = 'country', y = 'mpg')
```
```py
df['cylinders'].value_counts()
```
```py
sns.boxplot(data = df, x = 'cylinders', y = 'mpg')
```
#### 1.12 통계 정보 확인 
```py
df.describe()
```
#### 1.13 특성들 간의 상관관계 구하기 

- 상관계수 매트릭스 : df.corr() 이용
```py
df.corr()  # 범주형 데이터에서는 크게 의미가 없다.
```
- (시각화 1) 상관계수 산점도로 시각화 하기 : pd.plotting.scatter_matrix()
```py
obj = pd.plotting.scatter_matrix(df, figsize = (24, 16))
```
- (시각화 2) 상관계수 히트맵으로 시각화하기
```py
df_corr = df.corr()
f, ax = plt.subplots(figsize=(15, 12))
sns.heatmap(df_corr, annot=True, fmt = '.2f', square=True);
```
* (Question) 타깃(mpg)와의 상관계수가 가장 높은 특성은?
* (Answer) weight가 mpg와 음의 상관관계가 높다.

* [컬러맵 정보](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

- weight 특성과, mpg(타깃) 의 상관관계 및 산점도
```py
df[['weight', 'mpg']].corr()
```
```py
d = df.plot(kind = 'scatter', x = 'weight', y = 'mpg', alpha = 0.5)
```
## 2. 데이터 처리

### 2.1 누락데이터 처리하기

- horsepower 열의 ('?')를 np.nan으로 변경
```py
df['horsepower'].isin(['?']).sum()
```
```py
df['horsepower'].replace('?', np.nan, inplace = True)
```
```py
df['horsepower'].isin(['?']).sum()
```
```py
df['horsepower'].isin(['?']).sum()
```
```py
df['horsepower'].isnull().sum()
```
- 누락 데이터 삭제하기(행삭제)
```py
df.dropna(axis = 0, inplace = True)
df
```
```py
df['horsepower'].isnull().sum()
```
- horsepower 컬럼의 데이터 타입을 실수형으로 변환
```py
df['horsepower'].dtypes
```
```py
df['horsepower'] = df['horsepower'].astype('float64')
```
```py
df['horsepower'].dtypes
```
### 2.2 데이터 구간 분할

- horsepower 컬럼에 대해 3개의 구간으로 나누어 범주화 하기
- 예) 저출력, 보통출력, 고출력
```py
df['hp_cat'] = pd.cut(df['horsepower'], 3, labels = ['저출력', '보통출력', '고출력'])
df['hp_cat']
```
```py
df['hp_cat'].value_counts()
```
```py
# pd.qcut은 데이터 전체 389개를 양으로 3등분한 결과
cats = pd.qcut(df['horsepower'], 3, labels = ['저출력', '보통출력', '고출력'])
cats
```
```py
cats.value_counts()
```
### 2.3 더미 변수

- 범주화된 horwerpower 컬럼을 더미변수화 하기
```py
df['hp_cat'].unique()
```
```py
dummies = pd.get_dummies(df['hp_cat'])
dummies
```
### 2.4 불필요한 컬럼 삭제

- horsepower, hp_cat, name 컬럼 삭제
```py
df.drop(['horsepower', 'hp_cat', 'name'], axis = 1, inplace = True)
```
```py
df.head()
```
```py
pd.concat([df, dummies], axis = 1)
df.head()
```
### 2.5 중복 데이터 확인
```py
df.duplicated().sum()
```
