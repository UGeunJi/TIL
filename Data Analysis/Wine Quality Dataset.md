## Data 개요

**적포도주 및 백포도주 샘플의 물리화학적 특성 및 품질 등급**

- UCI 머신러닝 저장소에 공개 : [dataset](https://archive.ics.uci.edu/ml/datasets/Wine+Quality)
- 포르투갈 "Vinho Verde" 와인의 레드 및 화이트 변종 샘플에 대한 정보를 제공
- 각 와인 샘플은 와인 전문가에 의해 품질 평가를 받았고 화학적 테스트를 거쳤음
- 개인 정보 보호 및 물류 문제로 인해 포도 유형, 와인 브랜드, 와인 판매 가격 등에 대한 데이터가 없음

```
   Input variables (based on physicochemical tests):
   1 - fixed acidity (고정된 산도)
   2 - volatile acidity (휘발성 산도)
   3 - citric acid (구연산)
   4 - residual sugar (잔여 설탕)
   5 - chlorides (염화물)
   6 - free sulfur dioxide (유리 이산화황)
   7 - total sulfur dioxide (총 이산화황)
   8 - density (밀도)
   9 - pH (산도)
   10 - sulphates (황산염)
   11 - alcohol (알코올)

   Output variable (based on sensory data): 
   12 - quality (품질) (score between 0 and 10) 
```

## Step 1: 질문하기 (Ask questions)

데이터가 주어진 상태에서 질문을 할 수도 있고, 질문에 답할 수 있는 데이터를 수집할 수도 있다.

**질문 예시**

- 와인의 품질을 예측하는 데 가장 중요한 화학적 특성은 무엇일까?
- 어떤 유형(white, red)의 와인이 더 좋은 평가를 받을까?
- 알코올 도수가 높은 와인이 더 좋은 평가를 받을까?
- 더 달콤한 와인이 더 나은 평가를 받을까?
- 어느 정도의 산도가 와인 품질에 영향을 미칠까?

## Step 2: 데이터 랭글링 (Wrangle data)

- 데이터 랭글링 : 원자료(raw data)를 보다 쉽게 접근하고 분석할 수 있도록 데이터를 정리하고 통합하는 과정
  (참고. 위키피디아)
- 세부적으로는 데이터의 수집(gather), 평가(assess), 정제(clean) 작업으로 나눌 수 있다.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2.1 수집(gather)

```python
red = pd.read_csv('./Datasets/winequality-red.csv', sep = ';')
white = pd.read_csv('./Datasets/winequality-white.csv', sep = ';')
```

### 2.2 평가(assess)

**샘플의 개수**, **컬럼의 개수**

**누락 데이터 확인**

```python
print(red.shape, white.shape)
```

```
(1599, 12) (4898, 12)
```

```python
red.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.8</td>
      <td>0.88</td>
      <td>0.00</td>
      <td>2.6</td>
      <td>0.098</td>
      <td>25.0</td>
      <td>67.0</td>
      <td>0.9968</td>
      <td>3.20</td>
      <td>0.68</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.8</td>
      <td>0.76</td>
      <td>0.04</td>
      <td>2.3</td>
      <td>0.092</td>
      <td>15.0</td>
      <td>54.0</td>
      <td>0.9970</td>
      <td>3.26</td>
      <td>0.65</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.2</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.9</td>
      <td>0.075</td>
      <td>17.0</td>
      <td>60.0</td>
      <td>0.9980</td>
      <td>3.16</td>
      <td>0.58</td>
      <td>9.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

```python
white.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.0</td>
      <td>0.27</td>
      <td>0.36</td>
      <td>20.7</td>
      <td>0.045</td>
      <td>45.0</td>
      <td>170.0</td>
      <td>1.0010</td>
      <td>3.00</td>
      <td>0.45</td>
      <td>8.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6.3</td>
      <td>0.30</td>
      <td>0.34</td>
      <td>1.6</td>
      <td>0.049</td>
      <td>14.0</td>
      <td>132.0</td>
      <td>0.9940</td>
      <td>3.30</td>
      <td>0.49</td>
      <td>9.5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8.1</td>
      <td>0.28</td>
      <td>0.40</td>
      <td>6.9</td>
      <td>0.050</td>
      <td>30.0</td>
      <td>97.0</td>
      <td>0.9951</td>
      <td>3.26</td>
      <td>0.44</td>
      <td>10.1</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.2</td>
      <td>0.23</td>
      <td>0.32</td>
      <td>8.5</td>
      <td>0.058</td>
      <td>47.0</td>
      <td>186.0</td>
      <td>0.9956</td>
      <td>3.19</td>
      <td>0.40</td>
      <td>9.9</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.2</td>
      <td>0.23</td>
      <td>0.32</td>
      <td>8.5</td>
      <td>0.058</td>
      <td>47.0</td>
      <td>186.0</td>
      <td>0.9956</td>
      <td>3.19</td>
      <td>0.40</td>
      <td>9.9</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>

```python
red.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1599 entries, 0 to 1598
Data columns (total 12 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   fixed acidity         1599 non-null   float64
 1   volatile acidity      1599 non-null   float64
 2   citric acid           1599 non-null   float64
 3   residual sugar        1599 non-null   float64
 4   chlorides             1599 non-null   float64
 5   free sulfur dioxide   1599 non-null   float64
 6   total sulfur dioxide  1599 non-null   float64
 7   density               1599 non-null   float64
 8   pH                    1599 non-null   float64
 9   sulphates             1599 non-null   float64
 10  alcohol               1599 non-null   float64
 11  quality               1599 non-null   int64  
dtypes: float64(11), int64(1)
memory usage: 150.0 KB
```

```python
white.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4898 entries, 0 to 4897
Data columns (total 12 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   fixed acidity         4898 non-null   float64
 1   volatile acidity      4898 non-null   float64
 2   citric acid           4898 non-null   float64
 3   residual sugar        4898 non-null   float64
 4   chlorides             4898 non-null   float64
 5   free sulfur dioxide   4898 non-null   float64
 6   total sulfur dioxide  4898 non-null   float64
 7   density               4898 non-null   float64
 8   pH                    4898 non-null   float64
 9   sulphates             4898 non-null   float64
 10  alcohol               4898 non-null   float64
 11  quality               4898 non-null   int64  
dtypes: float64(11), int64(1)
memory usage: 459.3 KB
```

**중복 데이터 확인**

```python
red.duplicated().sum()
```

```
240
```

```python
white.duplicated().sum()
```

```
937
```

**quality 컬럼(특성)의 고유값과 개수**

```python
red['quality'].unique()
```

```
array([5, 6, 7, 4, 8, 3], dtype=int64)
```

```python
white['quality'].unique()
```

```
array([6, 5, 7, 8, 4, 3, 9], dtype=int64)
```

```python
red['quality'].nunique()
```

```
6
```

```python
white['quality'].nunique()
```

```
7
```

**통계 정보 확인**

```python
red.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
      <td>1599.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>8.319637</td>
      <td>0.527821</td>
      <td>0.270976</td>
      <td>2.538806</td>
      <td>0.087467</td>
      <td>15.874922</td>
      <td>46.467792</td>
      <td>0.996747</td>
      <td>3.311113</td>
      <td>0.658149</td>
      <td>10.422983</td>
      <td>5.636023</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.741096</td>
      <td>0.179060</td>
      <td>0.194801</td>
      <td>1.409928</td>
      <td>0.047065</td>
      <td>10.460157</td>
      <td>32.895324</td>
      <td>0.001887</td>
      <td>0.154386</td>
      <td>0.169507</td>
      <td>1.065668</td>
      <td>0.807569</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.600000</td>
      <td>0.120000</td>
      <td>0.000000</td>
      <td>0.900000</td>
      <td>0.012000</td>
      <td>1.000000</td>
      <td>6.000000</td>
      <td>0.990070</td>
      <td>2.740000</td>
      <td>0.330000</td>
      <td>8.400000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>7.100000</td>
      <td>0.390000</td>
      <td>0.090000</td>
      <td>1.900000</td>
      <td>0.070000</td>
      <td>7.000000</td>
      <td>22.000000</td>
      <td>0.995600</td>
      <td>3.210000</td>
      <td>0.550000</td>
      <td>9.500000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.900000</td>
      <td>0.520000</td>
      <td>0.260000</td>
      <td>2.200000</td>
      <td>0.079000</td>
      <td>14.000000</td>
      <td>38.000000</td>
      <td>0.996750</td>
      <td>3.310000</td>
      <td>0.620000</td>
      <td>10.200000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>9.200000</td>
      <td>0.640000</td>
      <td>0.420000</td>
      <td>2.600000</td>
      <td>0.090000</td>
      <td>21.000000</td>
      <td>62.000000</td>
      <td>0.997835</td>
      <td>3.400000</td>
      <td>0.730000</td>
      <td>11.100000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>15.900000</td>
      <td>1.580000</td>
      <td>1.000000</td>
      <td>15.500000</td>
      <td>0.611000</td>
      <td>72.000000</td>
      <td>289.000000</td>
      <td>1.003690</td>
      <td>4.010000</td>
      <td>2.000000</td>
      <td>14.900000</td>
      <td>8.000000</td>
    </tr>
  </tbody>
</table>
</div>

```python
white.describe()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
      <td>4898.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.854788</td>
      <td>0.278241</td>
      <td>0.334192</td>
      <td>6.391415</td>
      <td>0.045772</td>
      <td>35.308085</td>
      <td>138.360657</td>
      <td>0.994027</td>
      <td>3.188267</td>
      <td>0.489847</td>
      <td>10.514267</td>
      <td>5.877909</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.843868</td>
      <td>0.100795</td>
      <td>0.121020</td>
      <td>5.072058</td>
      <td>0.021848</td>
      <td>17.007137</td>
      <td>42.498065</td>
      <td>0.002991</td>
      <td>0.151001</td>
      <td>0.114126</td>
      <td>1.230621</td>
      <td>0.885639</td>
    </tr>
    <tr>
      <th>min</th>
      <td>3.800000</td>
      <td>0.080000</td>
      <td>0.000000</td>
      <td>0.600000</td>
      <td>0.009000</td>
      <td>2.000000</td>
      <td>9.000000</td>
      <td>0.987110</td>
      <td>2.720000</td>
      <td>0.220000</td>
      <td>8.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.300000</td>
      <td>0.210000</td>
      <td>0.270000</td>
      <td>1.700000</td>
      <td>0.036000</td>
      <td>23.000000</td>
      <td>108.000000</td>
      <td>0.991723</td>
      <td>3.090000</td>
      <td>0.410000</td>
      <td>9.500000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.800000</td>
      <td>0.260000</td>
      <td>0.320000</td>
      <td>5.200000</td>
      <td>0.043000</td>
      <td>34.000000</td>
      <td>134.000000</td>
      <td>0.993740</td>
      <td>3.180000</td>
      <td>0.470000</td>
      <td>10.400000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7.300000</td>
      <td>0.320000</td>
      <td>0.390000</td>
      <td>9.900000</td>
      <td>0.050000</td>
      <td>46.000000</td>
      <td>167.000000</td>
      <td>0.996100</td>
      <td>3.280000</td>
      <td>0.550000</td>
      <td>11.400000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>14.200000</td>
      <td>1.100000</td>
      <td>1.660000</td>
      <td>65.800000</td>
      <td>0.346000</td>
      <td>289.000000</td>
      <td>440.000000</td>
      <td>1.038980</td>
      <td>3.820000</td>
      <td>1.080000</td>
      <td>14.200000</td>
      <td>9.000000</td>
    </tr>
  </tbody>
</table>
</div>

### 2.3 정제(clean)

**중복데이터 삭제**

```python
red.drop_duplicates(inplace = True)
```

```python
white.drop_duplicates(inplace = True)
```

```python
print(red.shape, white.shape)
```

```
(1359, 12) (3961, 12)
```

**두 데이터 프레임 합치기**

```python
wine = pd.concat([red, white])
wine
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.99780</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.8</td>
      <td>0.88</td>
      <td>0.00</td>
      <td>2.6</td>
      <td>0.098</td>
      <td>25.0</td>
      <td>67.0</td>
      <td>0.99680</td>
      <td>3.20</td>
      <td>0.68</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.8</td>
      <td>0.76</td>
      <td>0.04</td>
      <td>2.3</td>
      <td>0.092</td>
      <td>15.0</td>
      <td>54.0</td>
      <td>0.99700</td>
      <td>3.26</td>
      <td>0.65</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.2</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.9</td>
      <td>0.075</td>
      <td>17.0</td>
      <td>60.0</td>
      <td>0.99800</td>
      <td>3.16</td>
      <td>0.58</td>
      <td>9.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.4</td>
      <td>0.66</td>
      <td>0.00</td>
      <td>1.8</td>
      <td>0.075</td>
      <td>13.0</td>
      <td>40.0</td>
      <td>0.99780</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
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
      <th>4893</th>
      <td>6.2</td>
      <td>0.21</td>
      <td>0.29</td>
      <td>1.6</td>
      <td>0.039</td>
      <td>24.0</td>
      <td>92.0</td>
      <td>0.99114</td>
      <td>3.27</td>
      <td>0.50</td>
      <td>11.2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4894</th>
      <td>6.6</td>
      <td>0.32</td>
      <td>0.36</td>
      <td>8.0</td>
      <td>0.047</td>
      <td>57.0</td>
      <td>168.0</td>
      <td>0.99490</td>
      <td>3.15</td>
      <td>0.46</td>
      <td>9.6</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4895</th>
      <td>6.5</td>
      <td>0.24</td>
      <td>0.19</td>
      <td>1.2</td>
      <td>0.041</td>
      <td>30.0</td>
      <td>111.0</td>
      <td>0.99254</td>
      <td>2.99</td>
      <td>0.46</td>
      <td>9.4</td>
      <td>6</td>
    </tr>
    <tr>
      <th>4896</th>
      <td>5.5</td>
      <td>0.29</td>
      <td>0.30</td>
      <td>1.1</td>
      <td>0.022</td>
      <td>20.0</td>
      <td>110.0</td>
      <td>0.98869</td>
      <td>3.34</td>
      <td>0.38</td>
      <td>12.8</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4897</th>
      <td>6.0</td>
      <td>0.21</td>
      <td>0.38</td>
      <td>0.8</td>
      <td>0.020</td>
      <td>22.0</td>
      <td>98.0</td>
      <td>0.98941</td>
      <td>3.26</td>
      <td>0.32</td>
      <td>11.8</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>5320 rows × 12 columns</p>
</div>

```python
wine.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fixed acidity</th>
      <th>volatile acidity</th>
      <th>citric acid</th>
      <th>residual sugar</th>
      <th>chlorides</th>
      <th>free sulfur dioxide</th>
      <th>total sulfur dioxide</th>
      <th>density</th>
      <th>pH</th>
      <th>sulphates</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.4</td>
      <td>0.70</td>
      <td>0.00</td>
      <td>1.9</td>
      <td>0.076</td>
      <td>11.0</td>
      <td>34.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7.8</td>
      <td>0.88</td>
      <td>0.00</td>
      <td>2.6</td>
      <td>0.098</td>
      <td>25.0</td>
      <td>67.0</td>
      <td>0.9968</td>
      <td>3.20</td>
      <td>0.68</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.8</td>
      <td>0.76</td>
      <td>0.04</td>
      <td>2.3</td>
      <td>0.092</td>
      <td>15.0</td>
      <td>54.0</td>
      <td>0.9970</td>
      <td>3.26</td>
      <td>0.65</td>
      <td>9.8</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11.2</td>
      <td>0.28</td>
      <td>0.56</td>
      <td>1.9</td>
      <td>0.075</td>
      <td>17.0</td>
      <td>60.0</td>
      <td>0.9980</td>
      <td>3.16</td>
      <td>0.58</td>
      <td>9.8</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.4</td>
      <td>0.66</td>
      <td>0.00</td>
      <td>1.8</td>
      <td>0.075</td>
      <td>13.0</td>
      <td>40.0</td>
      <td>0.9978</td>
      <td>3.51</td>
      <td>0.56</td>
      <td>9.4</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>

```python
wine.info()
```

```
<class 'pandas.core.frame.DataFrame'>
Int64Index: 5320 entries, 0 to 4897
Data columns (total 12 columns):
 #   Column                Non-Null Count  Dtype  
---  ------                --------------  -----  
 0   fixed acidity         5320 non-null   float64
 1   volatile acidity      5320 non-null   float64
 2   citric acid           5320 non-null   float64
 3   residual sugar        5320 non-null   float64
 4   chlorides             5320 non-null   float64
 5   free sulfur dioxide   5320 non-null   float64
 6   total sulfur dioxide  5320 non-null   float64
 7   density               5320 non-null   float64
 8   pH                    5320 non-null   float64
 9   sulphates             5320 non-null   float64
 10  alcohol               5320 non-null   float64
 11  quality               5320 non-null   int64  
dtypes: float64(11), int64(1)
memory usage: 540.3 KB
```

## Step 3: 데이터 탐색 (Exploratory Data Analysis)

데이터의 패턴을 찾고, 관계를 시각화 하는 작업 등으로 통해 데이터에 대한 직관을 극대화 한다.

### 3.1 새로 결합된 데이터 프레임으로 histogram 그리기

- fixed acidity, total sulfur dioxide, pH, alcohol

```python
wine[['fixed acidity', 'total sulfur dioxide', 'pH', 'alcohol']].hist(bins = 20, figsize = (24, 16))
```

```
array([[<AxesSubplot:title={'center':'fixed acidity'}>,
        <AxesSubplot:title={'center':'total sulfur dioxide'}>],
       [<AxesSubplot:title={'center':'pH'}>,
        <AxesSubplot:title={'center':'alcohol'}>]], dtype=object)
```

![image](https://user-images.githubusercontent.com/84713532/204096937-759163f1-b552-4d27-9bd1-e9219ce2c57c.png)


- Question) 특성 중 오른쪽으로 꼬리가 긴 분포(right skewed distribution)는 어떤것인가?
- Answer) fixed acidity

### 3.2 새로 결합된 데이터 프레임으로 산점도 그리기

- quality와 아래의 특성들간의 상관관계 파악하기
- volatile acidity, residual sugar, pH, alcohol

```python
plt.scatter(data = wine, x = 'quality', y = 'volatile acidity', alpha = 0.3)
```

```
<matplotlib.collections.PathCollection at 0x24237957e80>
```

![image](https://user-images.githubusercontent.com/84713532/204096980-22e59e1f-de10-4adb-b9ef-d129ed5c42c5.png)


```python
plt.scatter(data = wine, x = 'quality', y = 'residual sugar', alpha = 0.3)
```

```
<matplotlib.collections.PathCollection at 0x24237c767c0>
```

![image](https://user-images.githubusercontent.com/84713532/204097000-6449688b-a60d-4c73-b268-e29ad3888d19.png)


```python
plt.scatter(data = wine, x = 'quality', y = 'alcohol', alpha = 0.3)
```

```
<matplotlib.collections.PathCollection at 0x24237fa3400>
```

![image](https://user-images.githubusercontent.com/84713532/204097037-5b48e84f-4cd6-47a9-8f16-87769ee7a95f.png)


```python
plt.scatter(data = wine, x = 'quality', y = 'pH', alpha = 0.3)
```

```
<matplotlib.collections.PathCollection at 0x2423800b6a0>
```

![image](https://user-images.githubusercontent.com/84713532/204097065-ed082924-8175-4343-b06e-641cb7563479.png)


```python
scatter_col = ['volatile acidity', 'residual sugar', 'pH', 'alcohol', 'quality']
```

```python
obj = pd.plotting.scatter_matrix(wine[scatter_col], figsize=(16, 10))
```

![image](https://user-images.githubusercontent.com/84713532/204097092-5be5c745-e03d-4c4a-8755-8b3bae31ee37.png)


```python
scatter_col = ['volatile acidity', 'residual sugar', 'pH', 'alcohol', 'quality']

figrue, axes = plt.subplots(nrows=1, ncols=len(scatter_col)-1, figsize=(22, 4))

for index, column in enumerate(scatter_col[:-1]):
    sns.regplot(data=wine[scatter_col], x=column, y='quality', ax=axes[index] )
```

![image](https://user-images.githubusercontent.com/84713532/204097125-83236063-6094-45dc-a29f-c74a1fcc5a3f.png)


```python
wine[scatter_col].corr()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>volatile acidity</th>
      <th>residual sugar</th>
      <th>pH</th>
      <th>alcohol</th>
      <th>quality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>volatile acidity</th>
      <td>1.000000</td>
      <td>-0.163696</td>
      <td>0.246687</td>
      <td>-0.065411</td>
      <td>-0.265205</td>
    </tr>
    <tr>
      <th>residual sugar</th>
      <td>-0.163696</td>
      <td>1.000000</td>
      <td>-0.234522</td>
      <td>-0.305242</td>
      <td>-0.056830</td>
    </tr>
    <tr>
      <th>pH</th>
      <td>0.246687</td>
      <td>-0.234522</td>
      <td>1.000000</td>
      <td>0.097314</td>
      <td>0.039733</td>
    </tr>
    <tr>
      <th>alcohol</th>
      <td>-0.065411</td>
      <td>-0.305242</td>
      <td>0.097314</td>
      <td>1.000000</td>
      <td>0.469422</td>
    </tr>
    <tr>
      <th>quality</th>
      <td>-0.265205</td>
      <td>-0.056830</td>
      <td>0.039733</td>
      <td>0.469422</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

- Question) 품질에 긍정적인 영향을 미칠 가능성이 높은 특성은 어떤 것인가?
- Answer) alcohol

## Step 4: 결론 도출 또는 예측 (Draw conclusions or make predictions)

### 4.1 어떤 유형(white, red)의 와인이 더 좋은 평가를 받을까?

```python
red.value_counts().sum()
```

```
1359
```

```python
white.value_counts().sum()
```

```
3961
```

```python
red.mean()['quality']
```

```
5.6232523914643116
```

```python
white.mean()['quality']
```

```
5.854834637717748
```

```python
red['quality'].mean()
```

```
5.6360225140712945
```

```python
white['quality'].mean()
```

```
5.87790935075541
```

- **분석결과** : red 와인보다 white 와인의 퀄리티가 평균적으로 더 높다. 따라서 white 와인이 더 좋은 평가를 받을 것이다.

### 4.2 어느 정도의 산도가 와인 품질에 영향을 미칠까?

- 산도를 4등분하여 (low, medium, medium_high, high ) 어느 단계의 quality의 평균값이 높은지 확인하기

```python
wine['pH'].describe()
```

```
count    5320.000000
mean        3.224664
std         0.160379
min         2.720000
25%         3.110000
50%         3.210000
75%         3.330000
max         4.010000
Name: pH, dtype: float64
```

```python
wi_pH = wine['pH']
wi_pH
```

```
0       3.51
1       3.20
2       3.26
3       3.16
5       3.51
        ... 
4893    3.27
4894    3.15
4895    2.99
4896    3.34
4897    3.26
Name: pH, Length: 5320, dtype: float64
```

```python
bins = [2.72, 3.11, 3.21, 3.32, 4.01]
A = pd.cut(wi_pH, bins, labels = ["low", "medium", "medium_high", "high"])
A
```

```
0              high
1            medium
2       medium_high
3            medium
5              high
           ...     
4893    medium_high
4894         medium
4895            low
4896           high
4897    medium_high
Name: pH, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine['Acat'] = A
wine['Acat']
```

```
0              high
1            medium
2       medium_high
3            medium
5              high
           ...     
4893    medium_high
4894         medium
4895            low
4896           high
4897    medium_high
Name: Acat, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine.groupby('Acat').mean()['quality']
```

```
Acat
low            5.728024
medium         5.766917
medium_high    5.840183
high           5.847470
Name: quality, dtype: float64
```

```python
sns.barplot(data=wine, x='Acat', y='quality')
```

```
<AxesSubplot:xlabel='Acat', ylabel='quality'>
```

![image](https://user-images.githubusercontent.com/84713532/204097144-e76c4bfb-695c-48e0-be2b-4a143845a445.png)


- **분석결과** : 산도가 high인 구간의 퀄리티가 가장 높다.

### 4.3 더 달콤한 와인이 더 나은 평가를 받을까?

```python
wine['residual sugar'].describe()
```

```
count    5320.000000
mean        5.048477
std         4.500180
min         0.600000
25%         1.800000
50%         2.700000
75%         7.500000
max        65.800000
Name: residual sugar, dtype: float64
```

```python
wi_pH = wine['residual sugar']
wi_pH
```

```
0       1.9
1       2.6
2       2.3
3       1.9
5       1.8
       ... 
4893    1.6
4894    8.0
4895    1.2
4896    1.1
4897    0.8
Name: residual sugar, Length: 5320, dtype: float64
```

```python
bins = [0.6, 1.8, 3, 8.1, 65.8]
S = pd.cut(wi_pH, bins, labels = ["low", "medium", "medium_high", "high"])
S
```

```
0            medium
1            medium
2            medium
3            medium
5               low
           ...     
4893            low
4894    medium_high
4895            low
4896            low
4897            low
Name: residual sugar, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine['Scat'] = S
wine['Scat']
```

```
0            medium
1            medium
2            medium
3            medium
5               low
           ...     
4893            low
4894    medium_high
4895            low
4896            low
4897            low
Name: Scat, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine.groupby('Scat').mean()['quality']
```

```
Scat
low            5.785523
medium         5.800902
medium_high    5.894970
high           5.686189
Name: quality, dtype: float64
```

```python
sns.barplot(data=wine, x='Scat', y='quality')
```

```
<AxesSubplot:xlabel='Scat', ylabel='quality'>
```

![image](https://user-images.githubusercontent.com/84713532/204097165-bb2518ae-a36e-404a-85c5-cdcaa41334ae.png)


**분석 결과** : 어느 정도 적당하게 달아야 좋게 평가받는다. 단 거 원하면 사탕을 먹겠지.

### 4.4 알코올 도수가 높은 와인이 더 좋은 평가를 받을까?

```python
wine['alcohol'].describe()
```

```
count    5320.000000
mean       10.549241
std         1.185933
min         8.000000
25%         9.500000
50%        10.400000
75%        11.400000
max        14.900000
Name: alcohol, dtype: float64
```

```python
wi_pH = wine['alcohol']
wi_pH
```

```
0        9.4
1        9.8
2        9.8
3        9.8
5        9.4
        ... 
4893    11.2
4894     9.6
4895     9.4
4896    12.8
4897    11.8
Name: alcohol, Length: 5320, dtype: float64
```

```python
bins = [8.0, 9.5, 10.3, 11.3, 14.9]
B = pd.cut(wi_pH, bins, labels = ["low", "medium", "medium_high", "high"])
B
```

```
0               low
1            medium
2            medium
3            medium
5               low
           ...     
4893    medium_high
4894         medium
4895            low
4896           high
4897           high
Name: alcohol, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine['Bcat'] = B
wine['Bcat']
```

```
0               low
1            medium
2            medium
3            medium
5               low
           ...     
4893    medium_high
4894         medium
4895            low
4896           high
4897           high
Name: Bcat, Length: 5320, dtype: category
Categories (4, object): ['low' < 'medium' < 'medium_high' < 'high']
```

```python
wine.groupby('Bcat').mean()['quality']
```

```
Bcat
low            5.354167
medium         5.539159
medium_high    5.903297
high           6.376113
Name: quality, dtype: float64
```

```python
sns.barplot(data=wine, x='Bcat', y='quality')
```

```
<AxesSubplot:xlabel='Bcat', ylabel='quality'>
```

![image](https://user-images.githubusercontent.com/84713532/204097190-8c71491c-43ae-40f5-aa36-c129d4c3a9aa.png)


**분석 결과** : 도수가 높을 수록 좋은 평가를 받았다. 술은 취하려고 마시는 거니까.

## Step 5: 결과 공유 (Communicate the results)

보고서, 이메일, 블로그 등 다양한 방법을 통해 발견한 통찰들을 공유할 수 있다.

예.
