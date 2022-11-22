## 타이타닉 데이터셋 도전

- 승객의 나이, 성별, 승객 등급, 승선 위치 같은 속성을 기반으로 하여 승객의 생존 여부를 예측하는 것이 목표

- [캐글](https://www.kaggle.com)의 [타이타닉 챌린지](https://www.kaggle.com/c/titanic)에서 `train.csv`와 `test.csv`를 다운로드
- 두 파일을 각각 datasets 디렉토리에 titanic_train.csv titanic_test.csv로 저장

## 1. 데이터 탐색
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
#### 1.1 데이터 적재
```py
titanic_df = pd.read_csv('./Datasets/titanic_train.csv')
```
#### 1.2 titanic_df 살펴보기
```py
titanic_df
```
* **Survived**: 타깃. 0은 생존하지 못한 것이고 1은 생존을 의미
* **Pclass**: 승객 등급. 1, 2, 3등석.
* **Name**, **Sex**, **Age**: 이름 그대로의 의미
* **SibSp**: 함께 탑승한 형제, 배우자의 수
* **Parch**: 함께 탑승한 자녀, 부모의 수
* **Ticket**: 티켓 아이디
* **Fare**: 티켓 요금 (파운드)
* **Cabin**: 객실 번호
* **Embarked**: 승객이 탑승한 곳. C(Cherbourg), Q(Queenstown), S(Southampton)


#### 1.3 누락 데이터 살펴보기
```py
titanic_df.info()
```
```py
titanic_df.isnull()
```
#### 1.4 통계치 살펴보기
```py
titanic_df.describe()
```
```py
titanic_df.describe(include='object')
```
#### 1.5 Survived 컬럼 값의 빈도수 확인
```py
titanic_df['Survived'].value_counts()
```
#### 1.6 범주형(카테고리) 특성들의 빈도수 확인
- **Pclass**, **Sex**, **Embarked**
- **Embarked** 특성은 승객이 탑승한 곳 : C=Cherbourg, Q=Queenstown, S=Southampton.
```py
titanic_df['Pclass'].value_counts()
```
```py
titanic_df['Sex'].value_counts()
```
```py
titanic_df['Embarked'].value_counts()
```
#### 1.7 Name과 Age 열 을 Age 순으로 정렬해서 보기
```py
Age_df = titanic_df[['Name', 'Age']].sort_values(by = 'Age')
Age_df
```
#### 1.8 나이(Age)가 60 이상인 사람들의 Name과 Age 확인해 보기
```py
A_df = Age_df[(titanic_df['Age'] > 60)]
A_df
```
```py
# option 1
titanic_df[titanic_df['Age'] >= 60][['Name', 'Age']]
```
```py
# option 2
titanic_df.loc[titanic_df['Age'] >= 60, ['Name', 'Age']]
```
#### 1.9 나이가(Age)가 60 이상이고 1등석에 탔으며 여성인 탑승자 확인해 보기
```py
titanic_df[(titanic_df['Age'] > 60) & (titanic_df['Pclass'] == 1) & (titanic_df['Sex'] == 'female')]
```
#### 1.10 요금(Fare)의 최대값 최소값 확인해 보기
```py
titanic_df['Fare'].max()
```
```py
titanic_df['Fare'].min()
```
#### 1.11 등급(Pcalss) 그룹별 생존률 확인해보기
```py
S = titanic_df.groupby('Pclass').mean()['Survived']
S
```
```py
S.plot(kind = 'pie' , autopct = '%.1f%%')
```
```py
titanic_df.groupby('Pclass').size()
```
```py
titanic_df['Pclass'].value_counts()
```
```py
titanic_df.groupby(['Pclass', 'Survived']).size()
```
## 2. 데이터 전처리 (누락 데이터 처리, 범주화 등)

#### 2.1 Cabin 열 : 전체 삭제하기
```py
titanic_df
```
```py
titanic_df.drop('Cabin', axis = 1)
```
#### 2.2  Embarked 열 : 누락데이터를 승선도시 최고 빈도수 값으로 대체하기
```py
titanic_df['Embarked'].value_counts()
```
```py
titanic_df['Embarked'].fillna({'NaN':'S'})
```
```py
# ---------------------------------------------------------------
titanic_df['Embarked'].isnull().sum()
```
```py
sr = titanic_df['Embarked'].value_counts(dropna = False)
sr
```
```py
# numpy에서 가장 큰 값의 인덱스를 구하는 함수: argmax()
# pandas에서 가장 큰 값의 인덱스를 구하는 함수 idxmax()
```
```py
most_idx = sr.idxmax()
titanic_df['Embarked'].fillna(most_idx)
```
#### 2.3  Age 열 : 중간값으로 대체하기
```py
titanic_df.describe()
```
```py
me = titanic_df['Age'].median()
me
```
```py
titanic_df['Age'].fillna(me)
```
#### 2.4  Age 열: 범주로 나눠보기

* 0~18세
* 18~25세
* 25~35세
* 35~60세
* 60~80세
```py
Age = titanic_df['Age']
Age
```
```py
bins = [0, 18, 25, 35, 60, 80]
A = pd.cut(Age, bins, labels = ["0~18세", "18~25세", "25~35세", "35~60세", "60~80세"])
A
```
```py
A.hist()
```
```py
titanic_df['Acat'] = A
titanic_df['Acat']
```
```py
titanic_df['Acat'].value_counts()
```
```py
titanic_df.groupby('Acat').mean()['Survived']
```
```py
sns.barplot(data = titanic_df, x = 'Acat', y = 'Survived')
```
```py
sns.boxplot(data = titanic_df, x = 'Acat', y = 'Fare')
```
```py
sns.pointplot(data = titanic_df, x = 'Acat', y = 'Pclass')
```
* 범주 데이터를 dummy 변수로 바꿔보기 (One-Hot Encoding)
```py
titanic_df.describe()
```
```py
dummies = pd.get_dummies(titanic_df['PassengerId'])
dummies
```
```py
dummies1 = pd.get_dummies(titanic_df['Survived'])
dummies1
```
```py
dummies2 = pd.get_dummies(titanic_df['Pclass'])
dummies2
```
```py
dummies3 = pd.get_dummies(titanic_df['Age'])
dummies3
```
```py
dummies4 = pd.get_dummies(titanic_df['SibSp'])
dummies4
```
```py
dummies5 = pd.get_dummies(titanic_df['Parch'])
dummies5
```
```py
dummies6 = pd.get_dummies(titanic_df['Fare'])
dummies6
```
#### 2.5 중복 데이터 확인
```py
titanic_df.duplicated().sum()
```
