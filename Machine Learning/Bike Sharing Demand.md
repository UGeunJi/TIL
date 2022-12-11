# Bike Sharing Demand

- 도시 자전거 공유 시스템 사용 예측
- [캐글](https://www.kaggle.com)의 [Bike Sharing Demand](https://www.kaggle.com/c/bike-sharing-demand)에서 `train.csv`와 `test.csv`를 다운로드
- 두 파일을 각각 datasets 디렉토리에 bike_train.csv bike_test.csv로 저장

## 1. 문제 정의

- 자전거 대여량을 예측하는 문제
- Evaluation : Submissions are evaluated one the Root Mean Squared Logarithmic Error (RMSLE).

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

## 2. 데이터 가져오기

```python
bike_train = pd.read_csv('datasets/bike_train.csv') # 훈련 데이터
bike_test = pd.read_csv('datasets/bike_test.csv') # 테스트 데이터
submission = pd.read_csv('datasets/sampleSubmission.csv') # 제출 샘플 데이터
```

```python
bike_train.shape, bike_test.shape
```

```
((10886, 12), (6493, 9))
```

## 3. 데이터 훑어보기

```python
bike_train.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>season</th>
      <th>holiday</th>
      <th>workingday</th>
      <th>weather</th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>casual</th>
      <th>registered</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-01 00:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>81</td>
      <td>0.0</td>
      <td>3</td>
      <td>13</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-01 01:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0</td>
      <td>8</td>
      <td>32</td>
      <td>40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-01 02:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0</td>
      <td>5</td>
      <td>27</td>
      <td>32</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-01 03:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0</td>
      <td>3</td>
      <td>10</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-01 04:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>

```python
bike_test.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>season</th>
      <th>holiday</th>
      <th>workingday</th>
      <th>weather</th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-20 00:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>11.365</td>
      <td>56</td>
      <td>26.0027</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-20 01:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>56</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-20 02:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>56</td>
      <td>0.0000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-20 03:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>56</td>
      <td>11.0014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-20 04:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>56</td>
      <td>11.0014</td>
    </tr>
  </tbody>
</table>
</div>

```python
submission.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-20 00:00:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-20 01:00:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-20 02:00:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-20 03:00:00</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-20 04:00:00</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>

datetime: hourly date + timestamp  
season: 1 = 봄, 2 = 여름, 3 = 가을, 4 = 겨울  
holiday: 1 = 토, 일요일의 주말을 제외한 국경일 등의 휴일, 0 = 휴일이 아닌 날  
workingday: 1 = 토, 일요일의 주말 및 휴일이 아닌 주중, 0 = 주말 및 휴일  
weather:  
• 1 = 맑음, 약간 구름 낀 흐림  
• 2 = 안개, 안개 + 흐림  
• 3 = 가벼운 눈, 가벼운 비 + 천둥  
• 4 = 심한 눈/비, 천둥/번개  
temp: 온도(섭씨)  
atemp: 체감온도(섭씨)  
humidity: 상대습도  
windspeed: 풍속  
casual: 사전에 등록되지 않는 사용자가 대여한 횟수  
registered: 사전에 등록된 사용자가 대여한 횟수  
count: 대여 횟수

```python
h = bike_train.hist(bins=50, figsize=(20, 15))
```

![image](https://user-images.githubusercontent.com/84713532/206894888-5bad0d7b-ae81-409b-b058-e05f085c8713.png)


- target 값(count 열) 의 분포가 오른쪽으로 꼬리가 긴 모양

```python
bike_train.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 10886 entries, 0 to 10885
Data columns (total 12 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   datetime    10886 non-null  object 
 1   season      10886 non-null  int64  
 2   holiday     10886 non-null  int64  
 3   workingday  10886 non-null  int64  
 4   weather     10886 non-null  int64  
 5   temp        10886 non-null  float64
 6   atemp       10886 non-null  float64
 7   humidity    10886 non-null  int64  
 8   windspeed   10886 non-null  float64
 9   casual      10886 non-null  int64  
 10  registered  10886 non-null  int64  
 11  count       10886 non-null  int64  
dtypes: float64(3), int64(8), object(1)
memory usage: 1020.7+ KB
```

```python
bike_test.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 6493 entries, 0 to 6492
Data columns (total 9 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   datetime    6493 non-null   object 
 1   season      6493 non-null   int64  
 2   holiday     6493 non-null   int64  
 3   workingday  6493 non-null   int64  
 4   weather     6493 non-null   int64  
 5   temp        6493 non-null   float64
 6   atemp       6493 non-null   float64
 7   humidity    6493 non-null   int64  
 8   windspeed   6493 non-null   float64
dtypes: float64(3), int64(5), object(1)
memory usage: 456.7+ KB
```

- 누락데이터는 없으나, datetime 의 타입이 문자열로 되어 있음
- 효과적인 분석을 위해 datetime 특성을 datetime(pandas에서 제공하는 타입)으로 바꾼 뒤
- 년, 월, 일, 시간 추출

```python
bike_train['datetime'] = bike_train.datetime.apply(pd.to_datetime)
```

```python
bike_train['year'] = bike_train.datetime.apply(lambda x : x.year)
bike_train['month'] = bike_train.datetime.apply(lambda x : x.month)
bike_train['day'] = bike_train.datetime.apply(lambda x : x.day)
bike_train['hour'] = bike_train.datetime.apply(lambda x : x.hour)
bike_train['minute'] = bike_train.datetime.apply(lambda x : x.minute)
bike_train['dayofweek'] = bike_train.datetime.apply(lambda x : x.dayofweek) # 요일
```

- season과 weather 컬럼을 숫자에서 실제 의미 있는 단어로 표시
- **season** (1 = 봄, 2 = 여름, 3 = 가을, 4 = 겨울 )
- **weather** (1 = 맑음, 약간 구름 낀 흐림, 2 = 안개, 안개 + 흐림, 3 = 가벼운 눈, 가벼운 비 + 천둥, 4 = 심한 눈/비, 천둥/번개)

```python
bike_train['season'] = bike_train['season'].map({1 : 'Spring', 
                                                 2 : 'Summer',
                                                 3 : 'Fall', 
                                                 4 : 'Winter'})

bike_train['weather'] = bike_train['weather'].map({1 : 'Clear', 
                                                   2 : 'Mist, Few clouds',
                                                   3 : 'Light Snow, Rain, Thunder',
                                                   4 : 'Heavy Snow, Rain, Thunder'})
```

```python
bike_train.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>season</th>
      <th>holiday</th>
      <th>workingday</th>
      <th>weather</th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>casual</th>
      <th>registered</th>
      <th>count</th>
      <th>year</th>
      <th>month</th>
      <th>day</th>
      <th>hour</th>
      <th>minute</th>
      <th>dayofweek</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-01 00:00:00</td>
      <td>Spring</td>
      <td>0</td>
      <td>0</td>
      <td>Clear</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>81</td>
      <td>0.0</td>
      <td>3</td>
      <td>13</td>
      <td>16</td>
      <td>2011</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-01 01:00:00</td>
      <td>Spring</td>
      <td>0</td>
      <td>0</td>
      <td>Clear</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0</td>
      <td>8</td>
      <td>32</td>
      <td>40</td>
      <td>2011</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-01 02:00:00</td>
      <td>Spring</td>
      <td>0</td>
      <td>0</td>
      <td>Clear</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0</td>
      <td>5</td>
      <td>27</td>
      <td>32</td>
      <td>2011</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-01 03:00:00</td>
      <td>Spring</td>
      <td>0</td>
      <td>0</td>
      <td>Clear</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0</td>
      <td>3</td>
      <td>10</td>
      <td>13</td>
      <td>2011</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-01 04:00:00</td>
      <td>Spring</td>
      <td>0</td>
      <td>0</td>
      <td>Clear</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>2011</td>
      <td>1</td>
      <td>1</td>
      <td>4</td>
      <td>0</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

## 4. 데이터 탐색

### 4.1 타깃값(count) 의 분포도 그려보기

```python
sns.displot(bike_train['count'])
```

```
<seaborn.axisgrid.FacetGrid at 0x17430ddff40>
```

![image](https://user-images.githubusercontent.com/84713532/206894911-f94a580d-b3c4-40af-ae88-a496b8a39ebf.png)

- x축은 타깃값 count, y축은 빈도수(횟수)
- 오른쪽으로 꼬리가 긴 분포
- 회귀 모델이 좋은 성능 내려면 데이터가 정규분포를 따르는게 좋음
- 따라서 타깃값으 정규분포에 가깝게 만들기 위해 로그 변환 사용

```python
sns.displot(np.log(bike_train['count']))
```

```
<seaborn.axisgrid.FacetGrid at 0x1742fd459d0>
```

![image](https://user-images.githubusercontent.com/84713532/206894923-d066e64d-bece-45e9-b3d0-e5b6c0171339.png)


### 4.2 대여 시간대(년, 월, 일, 요일, 시간, 분) 에 따른 자전거 대여율

범주형 데이터에 따른 수치형 데이터의 평균값(막대그래프)

```python
bike_train.columns
```

```
Index(['datetime', 'season', 'holiday', 'workingday', 'weather', 'temp',
       'atemp', 'humidity', 'windspeed', 'casual', 'registered', 'count',
       'year', 'month', 'day', 'hour', 'minute', 'dayofweek'],
      dtype='object')
```

```python
figure, axes = plt.subplots(nrows=2, ncols=3)
plt.tight_layout()
figure.set_size_inches(15, 9)

sns.barplot(data=bike_train, x="year", y="count", ax=axes[0][0]) # 년도별 자전거 대여량의 평균
sns.barplot(data=bike_train, x="month", y="count", ax=axes[0][1]) # 월별 자전거 대여량의 평균
sns.barplot(data=bike_train, x="day", y="count", ax=axes[0][2]) # 날짜별 자전거 대여량의 평균

sns.barplot(data=bike_train, x="dayofweek", y="count", ax=axes[1][0]) # 요일별 자전거 대여량의 평균
sns.barplot(data=bike_train, x="hour", y="count", ax=axes[1][1]) # 시간별 자전거 대여량의 평균
sns.barplot(data=bike_train, x="minute", y="count", ax=axes[1][2]) # 분별 자전거 대여량의 평균


axes[0][0].set(title="number of rentals per year")
axes[0][1].set(title="number of rentals per month")
axes[0][2].set(title="number of rentals per day")

axes[1][0].set(title="number of rentals per dayofweek")
axes[1][1].set(title="number of rentals per hour")
axes[1][2].set(title="number of rentals per minute")
```

```
[Text(0.5, 1.0, 'number of rentals per minute')]
```

![image](https://user-images.githubusercontent.com/84713532/206894934-abb22e5d-3880-472c-a33e-b24f6a54eb28.png)


- 년도별 대여량은 2011년보다 2012년이 더 많음
- 월별 대여량은 6월에 가장 많고, 7~10월도 대여량이 많음. 1월이 가장 적음
- 일별 대여량은 1일부터 19일까지만 데이터가 있고 예측력도 없어 보임. 20~31일 데이터는 테스트 데이터에 있음(사용불가)
- 시간대 대여량은 오전 8시, 오후 17~18시에 에 많은것으로 보아 출퇴근 시간대로 추측(주말과 평일을 나누어 분석해보기)

### 4.3 대여 시간대를 제외한 다른 범주형 데이터(계절, 날씨, 공휴일여부 등)에 따른 자전거 대여율

```python
bike_train.columns
```

```
Index(['datetime', 'season', 'holiday', 'workingday', 'weather', 'temp',
       'atemp', 'humidity', 'windspeed', 'casual', 'registered', 'count',
       'year', 'month', 'day', 'hour', 'minute', 'dayofweek'],
      dtype='object')
```

```python
figure, axes = plt.subplots(nrows=2, ncols=2)
plt.tight_layout()
figure.set_size_inches(10, 10)

sns.barplot(data=bike_train, x="workingday", y="count", ax=axes[0][0]) 
sns.barplot(data=bike_train, x="holiday", y="count", ax=axes[0][1]) 

sns.barplot(data=bike_train, x="season", y="count", ax=axes[1][0]) 
sns.barplot(data=bike_train, x="weather", y="count", ax=axes[1][1]) 



axes[0][0].set(title="number of rentals per workingday")
axes[0][1].set(title="number of rentals per holiday")

axes[1][0].set(title="number of rentals per season")
axes[1][1].set(title="number of rentals per weather")

axes[1][1].set_xticklabels(axes[1][1].get_xticklabels(), rotation=30)
```

```
[Text(0, 0, 'Clear'),
 Text(1, 0, 'Mist, Few clouds'),
 Text(2, 0, 'Light Snow, Rain, Thunder'),
 Text(3, 0, 'Heavy Snow, Rain, Thunder')]
```

![image](https://user-images.githubusercontent.com/84713532/206894947-04215460-59d0-4d53-aaac-572211b19d18.png)


- 가을(Fall, 3)에 대여량이 많음 (앞의 month 특성과 겹치는 부분이 있음)
- 데이터가 지나치게 세분화 되어 있으면 분류별 데이터수가 적이지므로 month 특성 제거 고려
- 날씨가 좋을수록 대여 수량이 많음
- 그러나 heavy snow 기상상태에서 160건 이상의 대여량이 있는것이 이상

```python
bike_train.groupby("weather").size() # countplot
```

```
weather
Clear                        7192
Heavy Snow, Rain, Thunder       1
Light Snow, Rain, Thunder     859
Mist, Few clouds             2834
dtype: int64
```

```python
bike_train.groupby("weather").mean()['count'] # barplot
```

```
weather
Clear                        205.236791
Heavy Snow, Rain, Thunder    164.000000
Light Snow, Rain, Thunder    118.846333
Mist, Few clouds             178.955540
Name: count, dtype: float64
```

### 4.4 위의 범주형 데이터(계절, 날씨, 공휴일 여부 등)의 사분위 분포 확인

```python
figure, axes = plt.subplots(nrows=2, ncols=2)
plt.tight_layout()
figure.set_size_inches(10, 10)

sns.boxplot(data=bike_train, x="workingday", y="count", ax=axes[0][0]) 
sns.boxplot(data=bike_train, x="holiday", y="count", ax=axes[0][1]) 

sns.boxplot(data=bike_train, x="season", y="count", ax=axes[1][0]) 
sns.boxplot(data=bike_train, x="weather", y="count", ax=axes[1][1]) 



axes[0][0].set(title="box plot on count across workingday")
axes[0][1].set(title="box plot on count across holiday")

axes[1][0].set(title="box plot on count across season")
axes[1][1].set(title="box plot on count across weather")

axes[1][1].set_xticklabels(axes[1][1].get_xticklabels(), rotation=30)
```

```
[Text(0, 0, 'Clear'),
 Text(1, 0, 'Mist, Few clouds'),
 Text(2, 0, 'Light Snow, Rain, Thunder'),
 Text(3, 0, 'Heavy Snow, Rain, Thunder')]
```

![image](https://user-images.githubusercontent.com/84713532/206894978-ca31e959-7fe0-46aa-9317-7250036a7d1a.png)

- 공휴일이 아닐 때 특잇값(outlier)가 많음
- 근무일일 때 특잇값이 많음
- 가을(Fall, 3)에 대여량이 많음
- 날씨가 좋을수록 대여량이 많음
- 악천후 속 자전거 대여수 한건(특잇값)데 대해 제거 고려

### 4.5 시간대별 자건거 대여율을 추가 정보와 함께 보기

추가정보 : 공휴일여부

```python
figure, (ax1, ax2) = plt.subplots(nrows=2)
sns.pointplot(data=bike_train, x="hour", y="count", ax=ax1) # 시간별 자전거 대여량의 평균
sns.pointplot(data=bike_train, x="hour", y="count", hue='workingday', ax=ax2)
```

```
<AxesSubplot:xlabel='hour', ylabel='count'>
```

![image](https://user-images.githubusercontent.com/84713532/206894996-9eca594a-3856-49b8-bf71-bd84e5e2bc33.png)


- 근무일에는 출퇴근 시간에 대여량이 많고
- 쉬는날에는 오후 12~2시 사이에 대여량이 많음

### 4.6 상관관계

수치형 데이터 간 상관관계를 파악하기 위해 산점도 그래프(회귀선 포함한) 그리기

- **(1)** 온도, 체감온도, 습도, 풍속별 대여 수량 산점도 그래프('temp', 'atemp', 'humidity', 'windspeed')

```python
figure, axes = plt.subplots(nrows=2, ncols=2)
plt.tight_layout()
figure.set_size_inches(7, 6)

sns.regplot(data=bike_train, x='temp', y='count', ax=axes[0][0],
           scatter_kws={'alpha':0.2}, line_kws={'color' : 'blue'})
sns.regplot(data=bike_train, x='atemp', y='count', ax=axes[0][1],
           scatter_kws={'alpha':0.2}, line_kws={'color' : 'blue'})
sns.regplot(data=bike_train, x='humidity', y='count', ax=axes[1][0],
           scatter_kws={'alpha':0.2}, line_kws={'color' : 'blue'})
sns.regplot(data=bike_train, x='windspeed', y='count', ax=axes[1][1],
           scatter_kws={'alpha':0.2}, line_kws={'color' : 'blue'})
```

```
<AxesSubplot:xlabel='windspeed', ylabel='count'>
```

![image](https://user-images.githubusercontent.com/84713532/206895001-7296fed1-07f3-4e61-8ff7-a02e0d3aa6a6.png)


- 온도, 체감온도가 높을수록 대여 수량이 많음
  
- 습하지 않을수록 대여 수량이 많음
  
- 풍속이 셀수록 대여 수량이 많은지는 확실치가 않고
  
- 풍속이 0일 때 표시되어 있는 값을이 다수 발견되었고, 만약 결측치라면 제거하는 것 고려
  

- **(2)** 상관계수
  

```python
bike_train[['temp', 'atemp', 'humidity', 'windspeed', 'count']].corr()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>temp</th>
      <td>1.000000</td>
      <td>0.984948</td>
      <td>-0.064949</td>
      <td>-0.017852</td>
      <td>0.394454</td>
    </tr>
    <tr>
      <th>atemp</th>
      <td>0.984948</td>
      <td>1.000000</td>
      <td>-0.043536</td>
      <td>-0.057473</td>
      <td>0.389784</td>
    </tr>
    <tr>
      <th>humidity</th>
      <td>-0.064949</td>
      <td>-0.043536</td>
      <td>1.000000</td>
      <td>-0.318607</td>
      <td>-0.317371</td>
    </tr>
    <tr>
      <th>windspeed</th>
      <td>-0.017852</td>
      <td>-0.057473</td>
      <td>-0.318607</td>
      <td>1.000000</td>
      <td>0.101369</td>
    </tr>
    <tr>
      <th>count</th>
      <td>0.394454</td>
      <td>0.389784</td>
      <td>-0.317371</td>
      <td>0.101369</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

```python
corr = bike_train[['temp', 'atemp', 'humidity', 'windspeed', 'count']].corr()
plt.figure(figsize=(8,8)) # sns.heatmap 함수가 axes level api 이므로 figure 사이즈 조절 가능
sns.heatmap(corr, annot=True, fmt='.2f', linewidths=0.5, cmap='YlGnBu')
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/206895014-bc64f964-610b-4259-9926-b53f7938efab.png)


- 온도(temp)와 대여수량(count)간 상관계수 0.39(양의 상관관계)
- 풍속(windspeed)과 대여수량(count)간 상관계수는 0.1(상관관계가 매우 약함)
- windspeed는 대여 수량 예측에 별 도움을 주지 못하면서 결측치(0인값)도 많으므로 제거 고려

**선형회귀에서 다중공선성 문제(Multicollinearity in Regression)**

- https://towardsdatascience.com/multi-collinearity-in-regression-fe7a2c1467ea
- temp와 atemp가 상관관계가 높으므로 원하는 coef값이 나오지 않을 수 있음
- 두 특성 모두 예측변수에 양의 상관관계가 있으므로 coef가 양수값이 나오길 기대하지만
- 다중 선형회귀에선느 이 값이 바뀔 수 있음

## 5. 데이터 전처리

훈련 데이터와 테스트 데이터를 준비하는 방법

1. 훈련 데이터에 대한 전처리를 해준 뒤, 동일한 방법으로 테스트 데이터에 적용한다.
2. 훈련 데이터와 테스트 데이터를 합쳐서 모든 전처리가 끝난 뒤, 분리한다.

```python
from IPython.display import Image
Image('./images/img5.png')
```

![image](https://user-images.githubusercontent.com/84713532/206895024-a6bc5840-f466-4bda-858c-15bddd2a0ac3.png)


```python
bike_train = pd.read_csv('datasets/bike_train.csv')
bike_test = pd.read_csv('datasets/bike_test.csv')
submission = pd.read_csv('datasets/sampleSubmission.csv')
```

### 5.1 이상치 제거

```python
(bike_train['weather'] == 4).sum()
```

```
1
```

```python
bike_train.shape
```

```
(10886, 12)
```

```python
bike_train = bike_train[bike_train['weather'] != 4]
```

```python
bike_train.shape
```

```
(10885, 12)
```

### 5.2 훈련 데이터와 테스트 데이터 합치기

```python
pd.concat([bike_train, bike_test], axis=0) # 행축으로 연결
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>season</th>
      <th>holiday</th>
      <th>workingday</th>
      <th>weather</th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>casual</th>
      <th>registered</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-01 00:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>81</td>
      <td>0.0000</td>
      <td>3.0</td>
      <td>13.0</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-01 01:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0000</td>
      <td>8.0</td>
      <td>32.0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-01 02:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0000</td>
      <td>5.0</td>
      <td>27.0</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-01 03:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0000</td>
      <td>3.0</td>
      <td>10.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-01 04:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0000</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6488</th>
      <td>2012-12-31 19:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6489</th>
      <td>2012-12-31 20:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6490</th>
      <td>2012-12-31 21:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6491</th>
      <td>2012-12-31 22:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>56</td>
      <td>8.9981</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6492</th>
      <td>2012-12-31 23:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>65</td>
      <td>8.9981</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>17378 rows × 12 columns</p>
</div>

```python
all_data = pd.concat([bike_train, bike_test], axis=0, ignore_index=True) # 행축으로 연결
all_data
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>season</th>
      <th>holiday</th>
      <th>workingday</th>
      <th>weather</th>
      <th>temp</th>
      <th>atemp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>casual</th>
      <th>registered</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011-01-01 00:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>81</td>
      <td>0.0000</td>
      <td>3.0</td>
      <td>13.0</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2011-01-01 01:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0000</td>
      <td>8.0</td>
      <td>32.0</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2011-01-01 02:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.02</td>
      <td>13.635</td>
      <td>80</td>
      <td>0.0000</td>
      <td>5.0</td>
      <td>27.0</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2011-01-01 03:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0000</td>
      <td>3.0</td>
      <td>10.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011-01-01 04:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>9.84</td>
      <td>14.395</td>
      <td>75</td>
      <td>0.0000</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>17373</th>
      <td>2012-12-31 19:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17374</th>
      <td>2012-12-31 20:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17375</th>
      <td>2012-12-31 21:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>12.880</td>
      <td>60</td>
      <td>11.0014</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17376</th>
      <td>2012-12-31 22:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>56</td>
      <td>8.9981</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17377</th>
      <td>2012-12-31 23:00:00</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>10.66</td>
      <td>13.635</td>
      <td>65</td>
      <td>8.9981</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>17378 rows × 12 columns</p>
</div>

### 5.3 datetime으로부터 파생특성 추가(특성 공학, feature engineering)

```python
all_data['datetime'] = all_data.datetime.apply(pd.to_datetime)
all_data['year'] = all_data.datetime.apply(lambda x : x.year)
all_data['month'] = all_data.datetime.apply(lambda x : x.month)
all_data['hour'] = all_data.datetime.apply(lambda x : x.hour)
all_data['dayofweek'] = all_data.datetime.apply(lambda x : x.dayofweek) 
```

### 5.4 필요없는 특성 제거

```python
drop_features = ['casual', 'registered', 'datetime', 'windspeed', 'month']
all_data = all_data.drop(drop_features, axis=1)
```

- 탐색적 데이터 분석에서 얻은 인사트를 활용해 의미있는 특성과 불필요한 특성을 구분(특성 선택)

- 특성이 많다고 무조건 좋은게 아님
- 예측 성능을 높이려면 타기값과 관련있는 특성이 필요
- 탐색적 데이터 분석, 상관관계 매트릭스 등의 배경지식을 종합적으로 활용해 판단해야 함
- 모델링 과정에서 특성 중요도(Tree model), 회귀 계수등을 참고해 볼 수 있음

### 5.5 훈련 데이터와 테스트 데이터 나누기

```python
all_data[pd.isnull(all_data['count'])]
```

```
0        False
1        False
2        False
3        False
4        False
         ...  
17373     True
17374     True
17375     True
17376     True
17377     True
Name: count, Length: 17378, dtype: bool
```

```python
# Train/Test 데이터 분리하기
X_train = all_data[~pd.isnull(all_data['count'])]
X_test = all_data[pd.isnull(all_data['count'])]
```

```python
# 타깃값, 특성 분리하기
y_train = X_train['count']
X_train = X_train.drop(['count'], axis=1)


X_test = X_test.drop(['count'], axis=1)
# y_test = 없음
```

## 6. 평가지표 계산 함수 작성

```python
Image('./images/img6.png')
```

![image](https://user-images.githubusercontent.com/84713532/206895044-f772297f-ddb3-4724-a4a7-7af19806f10c.png)


```python
from sklearn.metrics import make_scorer
# log 값 변환 시 언더플로우 영향으로 log() 가 아닌 log1p() 를 이용하여 RMSLE 계산
def rmsle(y, pred, convertExp=True):
    if convertExp:
        y = np.expm1(y)
        pred = np.expm1(pred)

    log_y = np.log1p(y)
    log_pred = np.log1p(pred)
    squared_error = (log_y - log_pred) ** 2
    rmsle = np.sqrt(np.mean(squared_error))
    return rmsle

rmsle_scorer = make_scorer(rmsle, greater_is_better=False)
```

## 7. 모델 선택과 훈련

### 7.1 선형회귀 모델

```python
from sklearn.linear_model import LinearRegression

lin_reg = LinearRegression()
```

```python
log_y = np.log1p(y_train)
lin_reg.fit(X_train, log_y)
```

```
LinearRegression()
```

### 7.2 잘못된 검증 (X_train으로 학습하고, X_train으로 검증을 했으므로)

```python
y_pred = lin_reg.predict(X_train)
rmsle(log_y, y_pred, True)
```

```
1.0183455499651857
```

### 7.3 모델 성능 검증(교차 검증)

```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(lin_reg, X_train, log_y, scoring=rmsle_scorer, cv=5)
-scores.mean() # 5개 교차 검증한 결과의 평균 rmsle
```

```
1.0259377040159592
```

```python
# 공식 문서에 나와 있는  predefined values(‘neg_mean_squared_log_error’)를 사용해도 되나
# underflow 처리가 안되어 있는 것으로 보임
# https://scikit-learn.org/stable/modules/model_evaluation.html#the-scoring-parameter-defining-model-evaluation-rules
# scores = cross_val_score(lin_reg, X_train, y_train, scoring='neg_mean_squared_log_error', cv=5)
# -scores.mean()
```

```
C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py:696: UserWarning: Scoring failed. The score on this train-test partition for these parameters will be set to nan. Details: 
Traceback (most recent call last):
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py", line 687, in _score
    scores = scorer(estimator, X_test, y_test)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 87, in __call__
    score = scorer._score(cached_call, estimator,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 242, in _score
    return self._sign * self._score_func(y_true, y_pred,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\utils\validation.py", line 63, in inner_f
    return f(*args, **kwargs)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_regression.py", line 413, in mean_squared_log_error
    raise ValueError("Mean Squared Logarithmic Error cannot be used when "
ValueError: Mean Squared Logarithmic Error cannot be used when targets contain negative values.

  warnings.warn(
C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py:696: UserWarning: Scoring failed. The score on this train-test partition for these parameters will be set to nan. Details: 
Traceback (most recent call last):
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py", line 687, in _score
    scores = scorer(estimator, X_test, y_test)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 87, in __call__
    score = scorer._score(cached_call, estimator,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 242, in _score
    return self._sign * self._score_func(y_true, y_pred,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\utils\validation.py", line 63, in inner_f
    return f(*args, **kwargs)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_regression.py", line 413, in mean_squared_log_error
    raise ValueError("Mean Squared Logarithmic Error cannot be used when "
ValueError: Mean Squared Logarithmic Error cannot be used when targets contain negative values.

  warnings.warn(
C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py:696: UserWarning: Scoring failed. The score on this train-test partition for these parameters will be set to nan. Details: 
Traceback (most recent call last):
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\model_selection\_validation.py", line 687, in _score
    scores = scorer(estimator, X_test, y_test)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 87, in __call__
    score = scorer._score(cached_call, estimator,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_scorer.py", line 242, in _score
    return self._sign * self._score_func(y_true, y_pred,
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\utils\validation.py", line 63, in inner_f
    return f(*args, **kwargs)
  File "C:\Users\Playdata\anaconda3\lib\site-packages\sklearn\metrics\_regression.py", line 413, in mean_squared_log_error
    raise ValueError("Mean Squared Logarithmic Error cannot be used when "
ValueError: Mean Squared Logarithmic Error cannot be used when targets contain negative values.

  warnings.warn(

nan
```

### 7.4 규제모델(릿지, 라쏘, 엘라스티넷 모델)

```python
from sklearn.linear_model import Ridge, Lasso, ElasticNet

# 모델 생성
ridge = Ridge()
lasso = Lasso()
elastic = ElasticNet()
```

```python
scores = cross_val_score(ridge, X_train, log_y, scoring=rmsle_scorer, cv=5)
-scores.mean() # 릿지모델을 5개 교차 검증한 결과의 평균 rmsle
```

```
1.0259457332657096
```

```python
scores= cross_val_score(lasso, X_train, log_y, scoring=rmsle_scorer, cv=5)
-scores.mean() # 라쏘모델을 5개 교차 검증한 결과의 평균 rmsle
```

```
1.1142719258697973
```

```python
scores = cross_val_score(elastic, X_train, log_y, scoring=rmsle_scorer, cv=5)
-scores.mean() # 엘라스틱넷 모델을 5개 교차 검증한 결과의 평균 rmsle
```

```
1.1035342525816867
```

## 8. 모델 세부 튜닝

```python
from sklearn.model_selection import GridSearchCV
```

### 8.1 릿지 모델

```python
ridge = Ridge()

ridge_params = {'alpha' : [0.1, 1, 2, 3, 4, 10, 30, 100, 200, 300, 400, 800, 900, 1000]} # 14개

gridsearch_ridge = GridSearchCV(ridge, ridge_params, scoring=rmsle_scorer, cv=5, n_jobs=-1) # 14 * 5
```

```python
%time gridsearch_ridge.fit(X_train, log_y)
```

```
Wall time: 6.33 s





GridSearchCV(cv=5, estimator=Ridge(), n_jobs=-1,
             param_grid={'alpha': [0.1, 1, 2, 3, 4, 10, 30, 100, 200, 300, 400,
                                   800, 900, 1000]},
             scoring=make_scorer(rmsle, greater_is_better=False))
```

```python
gridsearch_ridge.best_params_
```

```
{'alpha': 0.1}
```

```python
cvres = gridsearch_ridge.cv_results_

for mean_score, params in zip(cvres['mean_test_score'], cvres['params']):
    print(-mean_score, params) # rmsle와 그 때의 하이퍼 파라미터
```

```
1.0259385051524947 {'alpha': 0.1}
1.0259457332657098 {'alpha': 1}
1.0259538020203387 {'alpha': 2}
1.0259619099095543 {'alpha': 3}
1.0259700565712468 {'alpha': 4}
1.0260197314469994 {'alpha': 10}
1.0261944516002468 {'alpha': 30}
1.0268953328557835 {'alpha': 100}
1.0280667404301447 {'alpha': 200}
1.0293631168653716 {'alpha': 300}
1.0307297219760279 {'alpha': 400}
1.036310230958598 {'alpha': 800}
1.0376557036987102 {'alpha': 900}
1.0389657418631324 {'alpha': 1000}
```

```python
coef = pd.Series(gridsearch_ridge.best_estimator_.coef_, index= X_train.columns)
coef_sort = coef.sort_values(ascending=False)
sns.barplot(x=coef_sort.values, y=coef_sort.index)
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/206895071-a995af4c-71ac-4d67-980b-a025089a705b.png)


### 8.2 랜덤포레스트

```python
from sklearn.ensemble import RandomForestRegressor

rf_params = {'n_estimators' : [100, 120, 140]}
rnd_forest = RandomForestRegressor(random_state=42)

gridsearch_forest = GridSearchCV(rnd_forest, rf_params, scoring=rmsle_scorer, cv=5, n_jobs=-1)

%time gridsearch_forest.fit(X_train, log_y)
```

```
Wall time: 37.8 s





GridSearchCV(cv=5, estimator=RandomForestRegressor(random_state=42), n_jobs=-1,
             param_grid={'n_estimators': [100, 120, 140]},
             scoring=make_scorer(rmsle, greater_is_better=False))
```

```python
gridsearch_forest.best_params_
```

```
{'n_estimators': 140}
```

```python
cvres = gridsearch_forest.cv_results_

for mean_score, params in zip(cvres['mean_test_score'], cvres['params']):
    print(-mean_score, params) # rmsle와 그 때의 하이퍼 파라미터
```

```
0.4624358747986295 {'n_estimators': 100}
0.461783777710962 {'n_estimators': 120}
0.46092376487614306 {'n_estimators': 140}
```

```python
# best_model = gridsearch_forest.best_estimator_
```

```python
sorted(zip(gridsearch_forest.best_estimator_.feature_importances_, X_train.columns), reverse=True)
```

```
[(0.7595180825712268, 'hour'),
 (0.04792802447771889, 'temp'),
 (0.03752619933445052, 'workingday'),
 (0.03460172064058957, 'season'),
 (0.03269870315942869, 'year'),
 (0.029982293239748867, 'dayofweek'),
 (0.022842240593619653, 'humidity'),
 (0.021451786722442186, 'atemp'),
 (0.011859502465998137, 'weather'),
 (0.001591446794776728, 'holiday')]
```

### 8.3 그레디언트 부스팅 모델

```python
from sklearn.ensemble import GradientBoostingRegressor
```

```python
gbrt_params = { 'learning_rate' : [0.01, 0.02, 0.03, 0.04], # 각 트리의 기여도
               'n_estimators' : [1000, 1500],
               'subsample' : [0.9, 0.5, 0.2],
               'max_depth' : [2, 4, 6, 8]

}

gbrt = GradientBoostingRegressor()

gridsearch_gbrt = GridSearchCV(gbrt, gbrt_params, scoring=rmsle_scorer, cv=5, n_jobs=-1)
```

```python
%time gridsearch_gbrt.fit(X_train, log_y)
```

```
Wall time: 33min 23s





GridSearchCV(cv=5, estimator=GradientBoostingRegressor(), n_jobs=-1,
             param_grid={'learning_rate': [0.01, 0.02, 0.03, 0.04],
                         'max_depth': [2, 4, 6, 8],
                         'n_estimators': [1000, 1500],
                         'subsample': [0.9, 0.5, 0.2]},
             scoring=make_scorer(rmsle, greater_is_better=False))
```

```python
gridsearch_gbrt.best_params_
```

```
{'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.2}
```

```python
cvres = gridsearch_gbrt.cv_results_

for mean_score, params in zip(cvres['mean_test_score'], cvres['params']):
    print(-mean_score, params) # rmsle와 그 때의 하이퍼 파라미터
```

```
0.5906089141705806 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.9}
0.579921762585159 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.5}
0.5663741039667025 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.2}
0.5471539011441585 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.9}
0.5311834646856217 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.5}
0.5145898623173469 {'learning_rate': 0.01, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.2}
0.4118950190737608 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.9}
0.3996996455607074 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.5}
0.3905148703809438 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.2}
0.39833687563844705 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.9}
0.38808278161602433 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.5}
0.3795914616843881 {'learning_rate': 0.01, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.2}
0.39842096753383477 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.9}
0.3869577673518602 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.5}
0.3824838450407437 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.2}
0.3968372102507972 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.9}
0.39148892207077896 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.5}
0.38106460343540627 {'learning_rate': 0.01, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.2}
0.41987668866867167 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.9}
0.4035587622239323 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.5}
0.39139526613132203 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.2}
0.42247997388135533 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.9}
0.403033968363641 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.5}
0.39254128948034345 {'learning_rate': 0.01, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.2}
0.5154467384447439 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.9}
0.49609546286244033 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.5}
0.48872050896328895 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.2}
0.47444137116187884 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.9}
0.4632210788301265 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.5}
0.4511927968064321 {'learning_rate': 0.02, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.2}
0.3940615219421288 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.9}
0.3907714604259203 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.5}
0.38265131183936385 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.2}
0.39509294536118206 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.9}
0.38500914270823694 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.5}
0.37793852547802886 {'learning_rate': 0.02, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.2}
0.40214516345353346 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.9}
0.393040935756728 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.5}
0.3919363193335945 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.2}
0.4080759521079864 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.9}
0.40018541504501376 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.5}
0.39243648284144406 {'learning_rate': 0.02, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.2}
0.426434870907884 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.9}
0.4102075452980422 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.5}
0.39741837857782814 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.2}
0.43375255879637037 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.9}
0.4122889744185871 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.5}
0.40760283095423794 {'learning_rate': 0.02, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.2}
0.47349613105504024 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.9}
0.4594690737140569 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.5}
0.4543533894350437 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.2}
0.44317495889783987 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.9}
0.43001870458437974 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.5}
0.4296998651477966 {'learning_rate': 0.03, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.2}
0.39487445439739466 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.9}
0.3835997293245262 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.5}
0.3850881912330891 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.2}
0.395186027786576 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.9}
0.388819941216073 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.5}
0.38981905398852745 {'learning_rate': 0.03, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.2}
0.4037401446700408 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.9}
0.3987030387428145 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.5}
0.3890568570237579 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.2}
0.41305108506417343 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.9}
0.40366887040582444 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.5}
0.399786031773361 {'learning_rate': 0.03, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.2}
0.4316671890920107 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.9}
0.41792501166325113 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.5}
0.40250766060061577 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.2}
0.4370268233120105 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.9}
0.4202238864805464 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.5}
0.4063778498773357 {'learning_rate': 0.03, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.2}
0.45100112068068154 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.9}
0.43927772220082273 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.5}
0.44152917410971737 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1000, 'subsample': 0.2}
0.4294218912667092 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.9}
0.41517980250739406 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.5}
0.4156676064827886 {'learning_rate': 0.04, 'max_depth': 2, 'n_estimators': 1500, 'subsample': 0.2}
0.3949748055358647 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.9}
0.38914522370176813 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.5}
0.39001818425548423 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1000, 'subsample': 0.2}
0.39978233756910975 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.9}
0.39507044815115694 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.5}
0.38730094156576234 {'learning_rate': 0.04, 'max_depth': 4, 'n_estimators': 1500, 'subsample': 0.2}
0.41272352555900715 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.9}
0.40557251093134256 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.5}
0.39501935398901855 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1000, 'subsample': 0.2}
0.4156625204444511 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.9}
0.4095703434330421 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.5}
0.4066175320762581 {'learning_rate': 0.04, 'max_depth': 6, 'n_estimators': 1500, 'subsample': 0.2}
0.43516100506982786 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.9}
0.4260868241573953 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.5}
0.4197472575914326 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1000, 'subsample': 0.2}
0.43322665401448024 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.9}
0.4279644987244298 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.5}
0.4204275535001128 {'learning_rate': 0.04, 'max_depth': 8, 'n_estimators': 1500, 'subsample': 0.2}
```

```python
best_model = gridsearch_gbrt.best_estimator_
```

```python
sorted(zip(gridsearch_gbrt.best_estimator_.feature_importances_, X_train.columns), reverse=True)
```

```
[(0.7238389424392861, 'hour'),
 (0.04384496892905651, 'temp'),
 (0.0425674121293566, 'workingday'),
 (0.03834706261079211, 'dayofweek'),
 (0.035668256399721286, 'season'),
 (0.03370358086159958, 'year'),
 (0.0322601838824559, 'atemp'),
 (0.030783224044040294, 'humidity'),
 (0.016553611107436732, 'weather'),
 (0.0024327575962549927, 'holiday')]
```

## 9.모델 예측과 성능 평가

```python
X_test.shape
```

```
(6493, 10)
```

```python
best_pred = best_model.predict(X_test)
best_pred
```

```
array([2.46204042, 1.78796519, 1.3283687 , ..., 4.73332347, 4.42257987,
       3.82758356])
```

```python
submission['count'] = np.expm1(best_pred)
```

```python
ver = 1
```

```python
submission.to_csv('bike_{}_submission.csv'.format(ver), index=False)
```

# 더 해볼만한것!

- registered와 casual을 각각 예측해서 합산해보는 방법도 있음
- 더 강력한 모델(boosting 모델)로 도전
