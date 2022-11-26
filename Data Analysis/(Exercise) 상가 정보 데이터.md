## Data 개요

**소상공인시장진흥공단_상가(상권)정보**

- 영업 중인 전국 상가업소 데이터를 제공
  
- (상호명, 업종코드, 업종명, 지번주소, 도로명주소, 경도, 위도 등)
  
- 공공 데이터 포털 
  https://www.data.go.kr/data/15083033/fileData.do
  

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
```

```python
plt.rc("font", family="Malgun Gothic")
plt.rc("axes", unicode_minus=False)
pd.options.display.max_columns = 39
```

## Step 1: 질문하기 (Ask questions)

데이터가 주어진 상태에서 질문을 할 수도 있고, 질문에 답할 수 있는 데이터를 수집할 수도 있다.

**예시**

- (1) 서초구에는 어떤 음식점 업종이 많을까?
- (2) 구별 음식점 업종 분포는 어떻게 다를까?
- (3) 어느 구에 학원수가 많을까?
- (4) 구별 학원 분포는 어떻게 다를까?
- (5) 관심 동네 비교해보기

## Step 2: 데이터 랭글링 (Wrangle data)

- 데이터 랭글링 : 원자료(raw data)를 보다 쉽게 접근하고 분석할 수 있도록 데이터를 정리하고 통합하는 과정
  (참고. 위키피디아)
- 세부적으로는 데이터의 수집(gather), 평가(assess), 정제(clean) 작업으로 나눌 수 있다.

### 2.1 수집(gather)

```python
sales = pd.read_csv('./Datasets/소상공인시장진흥공단_상가(상권)정보_서울_202209.csv')
```

```python
sales.head().T # 컬럼이 많아서 스크롤해야 보이므로 회전시킴
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>상가업소번호</th>
      <td>23324279</td>
      <td>24525909</td>
      <td>24715368</td>
      <td>15554136</td>
      <td>17174175</td>
    </tr>
    <tr>
      <th>상호명</th>
      <td>제중건강원</td>
      <td>민속악기사</td>
      <td>태평양진주</td>
      <td>김선희꼼꼼국어교습소</td>
      <td>비지트</td>
    </tr>
    <tr>
      <th>지점명</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>상권업종대분류코드</th>
      <td>D</td>
      <td>D</td>
      <td>D</td>
      <td>R</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>상권업종대분류명</th>
      <td>소매</td>
      <td>소매</td>
      <td>소매</td>
      <td>학문/교육</td>
      <td>음식</td>
    </tr>
    <tr>
      <th>상권업종중분류코드</th>
      <td>D10</td>
      <td>D04</td>
      <td>D26</td>
      <td>R01</td>
      <td>Q01</td>
    </tr>
    <tr>
      <th>상권업종중분류명</th>
      <td>건강/미용식품</td>
      <td>취미/오락관련소매</td>
      <td>시계/귀금속소매</td>
      <td>학원-보습교습입시</td>
      <td>한식</td>
    </tr>
    <tr>
      <th>상권업종소분류코드</th>
      <td>D10A07</td>
      <td>D04A09</td>
      <td>D26A01</td>
      <td>R01A01</td>
      <td>Q01A01</td>
    </tr>
    <tr>
      <th>상권업종소분류명</th>
      <td>건강원</td>
      <td>악기판매</td>
      <td>시계/귀금속</td>
      <td>학원-입시</td>
      <td>한식/백반/한정식</td>
    </tr>
    <tr>
      <th>표준산업분류코드</th>
      <td>G47216</td>
      <td>G47593</td>
      <td>G47830</td>
      <td>P85501</td>
      <td>I56111</td>
    </tr>
    <tr>
      <th>표준산업분류명</th>
      <td>건강보조식품 소매업</td>
      <td>악기 소매업</td>
      <td>시계 및 귀금속 소매업</td>
      <td>일반 교과 학원</td>
      <td>한식 음식점업</td>
    </tr>
    <tr>
      <th>시도코드</th>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
      <td>11</td>
    </tr>
    <tr>
      <th>시도명</th>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
    </tr>
    <tr>
      <th>시군구코드</th>
      <td>11560</td>
      <td>11200</td>
      <td>11110</td>
      <td>11710</td>
      <td>11650</td>
    </tr>
    <tr>
      <th>시군구명</th>
      <td>영등포구</td>
      <td>성동구</td>
      <td>종로구</td>
      <td>송파구</td>
      <td>서초구</td>
    </tr>
    <tr>
      <th>행정동코드</th>
      <td>1156053500</td>
      <td>1120079000</td>
      <td>1111061500</td>
      <td>1171056100</td>
      <td>1165062100</td>
    </tr>
    <tr>
      <th>행정동명</th>
      <td>영등포동</td>
      <td>용답동</td>
      <td>종로1.2.3.4가동</td>
      <td>방이1동</td>
      <td>방배4동</td>
    </tr>
    <tr>
      <th>법정동코드</th>
      <td>1156010600</td>
      <td>1120012200</td>
      <td>1111015200</td>
      <td>1171011100</td>
      <td>1165010100</td>
    </tr>
    <tr>
      <th>법정동명</th>
      <td>영등포동5가</td>
      <td>용답동</td>
      <td>봉익동</td>
      <td>방이동</td>
      <td>방배동</td>
    </tr>
    <tr>
      <th>지번코드</th>
      <td>1156010600100410001</td>
      <td>1120012200101420011</td>
      <td>1111015200100430001</td>
      <td>1171011100101970003</td>
      <td>1165010100108540018</td>
    </tr>
    <tr>
      <th>대지구분코드</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>대지구분명</th>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
    </tr>
    <tr>
      <th>지번본번지</th>
      <td>41</td>
      <td>142</td>
      <td>43</td>
      <td>197</td>
      <td>854</td>
    </tr>
    <tr>
      <th>지번부번지</th>
      <td>1</td>
      <td>11</td>
      <td>1</td>
      <td>3</td>
      <td>18</td>
    </tr>
    <tr>
      <th>지번주소</th>
      <td>서울특별시 영등포구 영등포동5가 41-1</td>
      <td>서울특별시 성동구 용답동 142-11</td>
      <td>서울특별시 종로구 봉익동 43-1</td>
      <td>서울특별시 송파구 방이동 197-3</td>
      <td>서울특별시 서초구 방배동 854-18</td>
    </tr>
    <tr>
      <th>도로명코드</th>
      <td>115604154799</td>
      <td>112004109480</td>
      <td>111104100163</td>
      <td>117104169448</td>
      <td>116504163117</td>
    </tr>
    <tr>
      <th>도로명</th>
      <td>서울특별시 영등포구 영중로14길</td>
      <td>서울특별시 성동구 용답5길</td>
      <td>서울특별시 종로구 서순라길</td>
      <td>서울특별시 송파구 위례성대로12길</td>
      <td>서울특별시 서초구 동광로18길</td>
    </tr>
    <tr>
      <th>건물본번지</th>
      <td>11</td>
      <td>2</td>
      <td>17</td>
      <td>31</td>
      <td>82</td>
    </tr>
    <tr>
      <th>건물부번지</th>
      <td>17</td>
      <td>NaN</td>
      <td>10</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>건물관리번호</th>
      <td>1156010600100410002034626</td>
      <td>1120012200101420011000227</td>
      <td>1111015200100440000000001</td>
      <td>1171011100101970003017195</td>
      <td>1165010100108540018009586</td>
    </tr>
    <tr>
      <th>건물명</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>금사랑투빌딩</td>
      <td>NaN</td>
      <td>상랑의빌딩</td>
    </tr>
    <tr>
      <th>도로명주소</th>
      <td>서울특별시 영등포구 영중로14길 11-17, (영등포동5가)</td>
      <td>서울특별시 성동구 용답5길 2, (용답동)</td>
      <td>서울특별시 종로구 서순라길 17-10, (봉익동)</td>
      <td>서울특별시 송파구 위례성대로12길 31, (방이동)</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
    </tr>
    <tr>
      <th>구우편번호</th>
      <td>150030</td>
      <td>133849</td>
      <td>110390</td>
      <td>138834</td>
      <td>137837</td>
    </tr>
    <tr>
      <th>신우편번호</th>
      <td>7250</td>
      <td>4803</td>
      <td>3138</td>
      <td>5640</td>
      <td>6572</td>
    </tr>
    <tr>
      <th>동정보</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>층정보</th>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>호정보</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>경도</th>
      <td>126.907</td>
      <td>127.049</td>
      <td>126.994</td>
      <td>127.122</td>
      <td>126.991</td>
    </tr>
    <tr>
      <th>위도</th>
      <td>37.5206</td>
      <td>37.5669</td>
      <td>37.5718</td>
      <td>37.511</td>
      <td>37.4884</td>
    </tr>
  </tbody>
</table>
</div>

### 2.2 평가(assess)

**샘플의 개수**, **컬럼의 개수**

```python
sales.shape
```

```
(361490, 39)
```

```python
sales.index
```

```
RangeIndex(start=0, stop=361490, step=1)
```

```python
sales.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 361490 entries, 0 to 361489
Data columns (total 39 columns):
 #   Column     Non-Null Count   Dtype  
---  ------     --------------   -----  
 0   상가업소번호     361490 non-null  int64  
 1   상호명        361490 non-null  object 
 2   지점명        61624 non-null   object 
 3   상권업종대분류코드  361490 non-null  object 
 4   상권업종대분류명   361490 non-null  object 
 5   상권업종중분류코드  361490 non-null  object 
 6   상권업종중분류명   361490 non-null  object 
 7   상권업종소분류코드  361490 non-null  object 
 8   상권업종소분류명   361490 non-null  object 
 9   표준산업분류코드   336942 non-null  object 
 10  표준산업분류명    336942 non-null  object 
 11  시도코드       361490 non-null  int64  
 12  시도명        361490 non-null  object 
 13  시군구코드      361490 non-null  int64  
 14  시군구명       361490 non-null  object 
 15  행정동코드      361490 non-null  int64  
 16  행정동명       361490 non-null  object 
 17  법정동코드      361490 non-null  int64  
 18  법정동명       361490 non-null  object 
 19  지번코드       361490 non-null  int64  
 20  대지구분코드     361490 non-null  int64  
 21  대지구분명      361490 non-null  object 
 22  지번본번지      361490 non-null  int64  
 23  지번부번지      286583 non-null  float64
 24  지번주소       361490 non-null  object 
 25  도로명코드      361490 non-null  int64  
 26  도로명        361490 non-null  object 
 27  건물본번지      361490 non-null  int64  
 28  건물부번지      48289 non-null   float64
 29  건물관리번호     361490 non-null  object 
 30  건물명        179097 non-null  object 
 31  도로명주소      361490 non-null  object 
 32  구우편번호      361490 non-null  int64  
 33  신우편번호      361490 non-null  int64  
 34  동정보        41048 non-null   object 
 35  층정보        221085 non-null  object 
 36  호정보        0 non-null       float64
 37  경도         361490 non-null  float64
 38  위도         361490 non-null  float64
dtypes: float64(5), int64(12), object(22)
memory usage: 107.6+ MB
```

**인덱스 정보 보기**

```python
sales.describe()
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
      <th>상가업소번호</th>
      <th>시도코드</th>
      <th>시군구코드</th>
      <th>행정동코드</th>
      <th>법정동코드</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>도로명코드</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.614900e+05</td>
      <td>361490.0</td>
      <td>361490.000000</td>
      <td>3.614900e+05</td>
      <td>3.614900e+05</td>
      <td>3.614900e+05</td>
      <td>361490.000000</td>
      <td>361490.000000</td>
      <td>286583.000000</td>
      <td>3.614900e+05</td>
      <td>361490.000000</td>
      <td>48289.000000</td>
      <td>361490.000000</td>
      <td>361490.000000</td>
      <td>0.0</td>
      <td>361490.000000</td>
      <td>361490.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.931741e+07</td>
      <td>11.0</td>
      <td>11447.440953</td>
      <td>1.144806e+09</td>
      <td>1.144755e+09</td>
      <td>1.144755e+18</td>
      <td>1.000714</td>
      <td>422.386384</td>
      <td>35.504465</td>
      <td>1.144780e+11</td>
      <td>139.732366</td>
      <td>8.071507</td>
      <td>137050.810033</td>
      <td>5207.071902</td>
      <td>NaN</td>
      <td>126.993759</td>
      <td>37.544906</td>
    </tr>
    <tr>
      <th>std</th>
      <td>4.309452e+06</td>
      <td>0.0</td>
      <td>196.827914</td>
      <td>1.968164e+07</td>
      <td>1.968207e+07</td>
      <td>1.968207e+16</td>
      <td>0.026706</td>
      <td>426.373510</td>
      <td>106.040693</td>
      <td>1.968288e+09</td>
      <td>259.077055</td>
      <td>9.766006</td>
      <td>14338.428718</td>
      <td>2149.908034</td>
      <td>NaN</td>
      <td>0.083937</td>
      <td>0.049022</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2.896730e+06</td>
      <td>11.0</td>
      <td>11110.000000</td>
      <td>1.111052e+09</td>
      <td>1.111010e+09</td>
      <td>1.111010e+18</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.111020e+11</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>100011.000000</td>
      <td>1000.000000</td>
      <td>NaN</td>
      <td>126.768169</td>
      <td>37.434081</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.673368e+07</td>
      <td>11.0</td>
      <td>11260.000000</td>
      <td>1.126066e+09</td>
      <td>1.126010e+09</td>
      <td>1.126011e+18</td>
      <td>1.000000</td>
      <td>102.000000</td>
      <td>4.000000</td>
      <td>1.126041e+11</td>
      <td>19.000000</td>
      <td>1.000000</td>
      <td>131823.000000</td>
      <td>3440.000000</td>
      <td>NaN</td>
      <td>126.922367</td>
      <td>37.504588</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.822703e+07</td>
      <td>11.0</td>
      <td>11470.000000</td>
      <td>1.147056e+09</td>
      <td>1.147010e+09</td>
      <td>1.147010e+18</td>
      <td>1.000000</td>
      <td>301.000000</td>
      <td>11.000000</td>
      <td>1.147031e+11</td>
      <td>46.000000</td>
      <td>5.000000</td>
      <td>137726.000000</td>
      <td>5288.000000</td>
      <td>NaN</td>
      <td>127.009557</td>
      <td>37.542195</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.307572e+07</td>
      <td>11.0</td>
      <td>11650.000000</td>
      <td>1.165052e+09</td>
      <td>1.165010e+09</td>
      <td>1.165010e+18</td>
      <td>1.000000</td>
      <td>644.000000</td>
      <td>28.000000</td>
      <td>1.165021e+11</td>
      <td>154.000000</td>
      <td>11.000000</td>
      <td>150092.000000</td>
      <td>6957.000000</td>
      <td>NaN</td>
      <td>127.056107</td>
      <td>37.572518</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2.852486e+07</td>
      <td>11.0</td>
      <td>11740.000000</td>
      <td>1.174070e+09</td>
      <td>1.174011e+09</td>
      <td>1.174011e+18</td>
      <td>2.000000</td>
      <td>9999.000000</td>
      <td>3784.000000</td>
      <td>1.174049e+11</td>
      <td>3581.000000</td>
      <td>203.000000</td>
      <td>158887.000000</td>
      <td>8866.000000</td>
      <td>NaN</td>
      <td>127.182588</td>
      <td>37.690787</td>
    </tr>
  </tbody>
</table>
</div>

```python
sales.index
```

```
RangeIndex(start=0, stop=361490, step=1)
```

**컬럼 정보 보기**

```python
sales.columns
```

```
Index(['상가업소번호', '상호명', '지점명', '상권업종대분류코드', '상권업종대분류명', '상권업종중분류코드',
       '상권업종중분류명', '상권업종소분류코드', '상권업종소분류명', '표준산업분류코드', '표준산업분류명', '시도코드',
       '시도명', '시군구코드', '시군구명', '행정동코드', '행정동명', '법정동코드', '법정동명', '지번코드',
       '대지구분코드', '대지구분명', '지번본번지', '지번부번지', '지번주소', '도로명코드', '도로명', '건물본번지',
       '건물부번지', '건물관리번호', '건물명', '도로명주소', '구우편번호', '신우편번호', '동정보', '층정보',
       '호정보', '경도', '위도'],
      dtype='object')
```

**요약 정보 보기**

```python
sales.head()
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
      <th>상가업소번호</th>
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도코드</th>
      <th>시도명</th>
      <th>시군구코드</th>
      <th>시군구명</th>
      <th>행정동코드</th>
      <th>행정동명</th>
      <th>법정동코드</th>
      <th>법정동명</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>지번주소</th>
      <th>도로명코드</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>동정보</th>
      <th>층정보</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23324279</td>
      <td>제중건강원</td>
      <td>NaN</td>
      <td>D</td>
      <td>소매</td>
      <td>D10</td>
      <td>건강/미용식품</td>
      <td>D10A07</td>
      <td>건강원</td>
      <td>G47216</td>
      <td>건강보조식품 소매업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11560</td>
      <td>영등포구</td>
      <td>1156053500</td>
      <td>영등포동</td>
      <td>1156010600</td>
      <td>영등포동5가</td>
      <td>1156010600100410001</td>
      <td>1</td>
      <td>대지</td>
      <td>41</td>
      <td>1.0</td>
      <td>서울특별시 영등포구 영등포동5가 41-1</td>
      <td>115604154799</td>
      <td>서울특별시 영등포구 영중로14길</td>
      <td>11</td>
      <td>17.0</td>
      <td>1156010600100410002034626</td>
      <td>NaN</td>
      <td>서울특별시 영등포구 영중로14길 11-17, (영등포동5가)</td>
      <td>150030</td>
      <td>7250</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.907168</td>
      <td>37.520613</td>
    </tr>
    <tr>
      <th>1</th>
      <td>24525909</td>
      <td>민속악기사</td>
      <td>NaN</td>
      <td>D</td>
      <td>소매</td>
      <td>D04</td>
      <td>취미/오락관련소매</td>
      <td>D04A09</td>
      <td>악기판매</td>
      <td>G47593</td>
      <td>악기 소매업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11200</td>
      <td>성동구</td>
      <td>1120079000</td>
      <td>용답동</td>
      <td>1120012200</td>
      <td>용답동</td>
      <td>1120012200101420011</td>
      <td>1</td>
      <td>대지</td>
      <td>142</td>
      <td>11.0</td>
      <td>서울특별시 성동구 용답동 142-11</td>
      <td>112004109480</td>
      <td>서울특별시 성동구 용답5길</td>
      <td>2</td>
      <td>NaN</td>
      <td>1120012200101420011000227</td>
      <td>NaN</td>
      <td>서울특별시 성동구 용답5길 2, (용답동)</td>
      <td>133849</td>
      <td>4803</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.049018</td>
      <td>37.566857</td>
    </tr>
    <tr>
      <th>2</th>
      <td>24715368</td>
      <td>태평양진주</td>
      <td>NaN</td>
      <td>D</td>
      <td>소매</td>
      <td>D26</td>
      <td>시계/귀금속소매</td>
      <td>D26A01</td>
      <td>시계/귀금속</td>
      <td>G47830</td>
      <td>시계 및 귀금속 소매업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11110</td>
      <td>종로구</td>
      <td>1111061500</td>
      <td>종로1.2.3.4가동</td>
      <td>1111015200</td>
      <td>봉익동</td>
      <td>1111015200100430001</td>
      <td>1</td>
      <td>대지</td>
      <td>43</td>
      <td>1.0</td>
      <td>서울특별시 종로구 봉익동 43-1</td>
      <td>111104100163</td>
      <td>서울특별시 종로구 서순라길</td>
      <td>17</td>
      <td>10.0</td>
      <td>1111015200100440000000001</td>
      <td>금사랑투빌딩</td>
      <td>서울특별시 종로구 서순라길 17-10, (봉익동)</td>
      <td>110390</td>
      <td>3138</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.993530</td>
      <td>37.571848</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15554136</td>
      <td>김선희꼼꼼국어교습소</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R01</td>
      <td>학원-보습교습입시</td>
      <td>R01A01</td>
      <td>학원-입시</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11710</td>
      <td>송파구</td>
      <td>1171056100</td>
      <td>방이1동</td>
      <td>1171011100</td>
      <td>방이동</td>
      <td>1171011100101970003</td>
      <td>1</td>
      <td>대지</td>
      <td>197</td>
      <td>3.0</td>
      <td>서울특별시 송파구 방이동 197-3</td>
      <td>117104169448</td>
      <td>서울특별시 송파구 위례성대로12길</td>
      <td>31</td>
      <td>NaN</td>
      <td>1171011100101970003017195</td>
      <td>NaN</td>
      <td>서울특별시 송파구 위례성대로12길 31, (방이동)</td>
      <td>138834</td>
      <td>5640</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>127.121520</td>
      <td>37.510967</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17174175</td>
      <td>비지트</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165062100</td>
      <td>방배4동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100108540018</td>
      <td>1</td>
      <td>대지</td>
      <td>854</td>
      <td>18.0</td>
      <td>서울특별시 서초구 방배동 854-18</td>
      <td>116504163117</td>
      <td>서울특별시 서초구 동광로18길</td>
      <td>82</td>
      <td>NaN</td>
      <td>1165010100108540018009586</td>
      <td>상랑의빌딩</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
      <td>137837</td>
      <td>6572</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.991394</td>
      <td>37.488375</td>
    </tr>
  </tbody>
</table>
</div>

```python
sales.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 361490 entries, 0 to 361489
Data columns (total 39 columns):
 #   Column     Non-Null Count   Dtype  
---  ------     --------------   -----  
 0   상가업소번호     361490 non-null  int64  
 1   상호명        361490 non-null  object 
 2   지점명        61624 non-null   object 
 3   상권업종대분류코드  361490 non-null  object 
 4   상권업종대분류명   361490 non-null  object 
 5   상권업종중분류코드  361490 non-null  object 
 6   상권업종중분류명   361490 non-null  object 
 7   상권업종소분류코드  361490 non-null  object 
 8   상권업종소분류명   361490 non-null  object 
 9   표준산업분류코드   336942 non-null  object 
 10  표준산업분류명    336942 non-null  object 
 11  시도코드       361490 non-null  int64  
 12  시도명        361490 non-null  object 
 13  시군구코드      361490 non-null  int64  
 14  시군구명       361490 non-null  object 
 15  행정동코드      361490 non-null  int64  
 16  행정동명       361490 non-null  object 
 17  법정동코드      361490 non-null  int64  
 18  법정동명       361490 non-null  object 
 19  지번코드       361490 non-null  int64  
 20  대지구분코드     361490 non-null  int64  
 21  대지구분명      361490 non-null  object 
 22  지번본번지      361490 non-null  int64  
 23  지번부번지      286583 non-null  float64
 24  지번주소       361490 non-null  object 
 25  도로명코드      361490 non-null  int64  
 26  도로명        361490 non-null  object 
 27  건물본번지      361490 non-null  int64  
 28  건물부번지      48289 non-null   float64
 29  건물관리번호     361490 non-null  object 
 30  건물명        179097 non-null  object 
 31  도로명주소      361490 non-null  object 
 32  구우편번호      361490 non-null  int64  
 33  신우편번호      361490 non-null  int64  
 34  동정보        41048 non-null   object 
 35  층정보        221085 non-null  object 
 36  호정보        0 non-null       float64
 37  경도         361490 non-null  float64
 38  위도         361490 non-null  float64
dtypes: float64(5), int64(12), object(22)
memory usage: 107.6+ MB
```

**누락 데이터 확인**

```python
null_sum = sales.isnull().sum()
null_sum
```

```
상가업소번호            0
상호명               0
지점명          299866
상권업종대분류코드         0
상권업종대분류명          0
상권업종중분류코드         0
상권업종중분류명          0
상권업종소분류코드         0
상권업종소분류명          0
표준산업분류코드      24548
표준산업분류명       24548
시도코드              0
시도명               0
시군구코드             0
시군구명              0
행정동코드             0
행정동명              0
법정동코드             0
법정동명              0
지번코드              0
대지구분코드            0
대지구분명             0
지번본번지             0
지번부번지         74907
지번주소              0
도로명코드             0
도로명               0
건물본번지             0
건물부번지        313201
건물관리번호            0
건물명          182393
도로명주소             0
구우편번호             0
신우편번호             0
동정보          320442
층정보          140405
호정보          361490
경도                0
위도                0
dtype: int64
```

```python
null_sum.plot(kind='barh', figsize=(10, 10))
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/204099245-ef33a6f0-61f6-425c-b4ad-ff6543b29542.png)

```python
plt.figure(figsize=(10, 10))
sns.barplot(y=null_sum.index, x=null_sum.values)
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/204099258-61e35e21-9e67-413f-9657-45bbc4dff1c3.png)


### 2.3 정제(clean)

**누락 데이터가 많은 컬럼 삭제**

```python
not_use = null_sum.sort_values(ascending=False).head(9)
not_use_col = not_use.index
not_use_col
```

```
Index(['호정보', '동정보', '건물부번지', '지점명', '건물명', '층정보', '지번부번지', '표준산업분류명',
       '표준산업분류코드'],
      dtype='object')
```

```python
df = sales.drop(not_use_col, axis=1)
```

```python
df.isnull().sum()
```

```
상가업소번호       0
상호명          0
상권업종대분류코드    0
상권업종대분류명     0
상권업종중분류코드    0
상권업종중분류명     0
상권업종소분류코드    0
상권업종소분류명     0
시도코드         0
시도명          0
시군구코드        0
시군구명         0
행정동코드        0
행정동명         0
법정동코드        0
법정동명         0
지번코드         0
대지구분코드       0
대지구분명        0
지번본번지        0
지번주소         0
도로명코드        0
도로명          0
건물본번지        0
건물관리번호       0
도로명주소        0
구우편번호        0
신우편번호        0
경도           0
위도           0
dtype: int64
```

```python
sales.drop(['지점명', '표준산업분류코드', '표준산업분류명', '지번부번지', '건물부번지', '건물명', '동정보', '층정보', '호정보'], axis = 1, inplace = True)
```

```python
sales.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 361490 entries, 0 to 361489
Data columns (total 39 columns):
 #   Column     Non-Null Count   Dtype  
---  ------     --------------   -----  
 0   상가업소번호     361490 non-null  int64  
 1   상호명        361490 non-null  object 
 2   지점명        61624 non-null   object 
 3   상권업종대분류코드  361490 non-null  object 
 4   상권업종대분류명   361490 non-null  object 
 5   상권업종중분류코드  361490 non-null  object 
 6   상권업종중분류명   361490 non-null  object 
 7   상권업종소분류코드  361490 non-null  object 
 8   상권업종소분류명   361490 non-null  object 
 9   표준산업분류코드   336942 non-null  object 
 10  표준산업분류명    336942 non-null  object 
 11  시도코드       361490 non-null  int64  
 12  시도명        361490 non-null  object 
 13  시군구코드      361490 non-null  int64  
 14  시군구명       361490 non-null  object 
 15  행정동코드      361490 non-null  int64  
 16  행정동명       361490 non-null  object 
 17  법정동코드      361490 non-null  int64  
 18  법정동명       361490 non-null  object 
 19  지번코드       361490 non-null  int64  
 20  대지구분코드     361490 non-null  int64  
 21  대지구분명      361490 non-null  object 
 22  지번본번지      361490 non-null  int64  
 23  지번부번지      286583 non-null  float64
 24  지번주소       361490 non-null  object 
 25  도로명코드      361490 non-null  int64  
 26  도로명        361490 non-null  object 
 27  건물본번지      361490 non-null  int64  
 28  건물부번지      48289 non-null   float64
 29  건물관리번호     361490 non-null  object 
 30  건물명        179097 non-null  object 
 31  도로명주소      361490 non-null  object 
 32  구우편번호      361490 non-null  int64  
 33  신우편번호      361490 non-null  int64  
 34  동정보        41048 non-null   object 
 35  층정보        221085 non-null  object 
 36  호정보        0 non-null       float64
 37  경도         361490 non-null  float64
 38  위도         361490 non-null  float64
dtypes: float64(5), int64(12), object(22)
memory usage: 107.6+ MB
```

**컬럼명에 "코드" 또는 "번호"가 들어간 컬럼 삭제**

```python
sales.columns.str.contains("코드")
```

```
array([False, False, False,  True, False,  True, False,  True, False,
        True, False,  True, False,  True, False,  True, False,  True,
       False,  True,  True, False, False, False, False,  True, False,
       False, False, False, False, False, False, False, False, False,
       False, False, False])
```

```python
code_cols = df.columns[df.columns.str.contains("코드")]
code_cols
```

```
Index(['상권업종대분류코드', '상권업종중분류코드', '상권업종소분류코드', '시도코드', '시군구코드', '행정동코드',
       '법정동코드', '지번코드', '대지구분코드', '도로명코드'],
      dtype='object')
```

```python
df = df.drop(code_cols, axis=1)
```

```python
num_cols = df.columns[df.columns.str.contains("번호")]
num_cols
```

```
Index(['상가업소번호', '건물관리번호', '구우편번호', '신우편번호'], dtype='object')
```

```python
df = df.drop(num_cols, axis=1)
```

```python
df.shape
```

```
(361490, 16)
```

```python
df.head().T
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>상호명</th>
      <td>제중건강원</td>
      <td>민속악기사</td>
      <td>태평양진주</td>
      <td>김선희꼼꼼국어교습소</td>
      <td>비지트</td>
    </tr>
    <tr>
      <th>상권업종대분류명</th>
      <td>소매</td>
      <td>소매</td>
      <td>소매</td>
      <td>학문/교육</td>
      <td>음식</td>
    </tr>
    <tr>
      <th>상권업종중분류명</th>
      <td>건강/미용식품</td>
      <td>취미/오락관련소매</td>
      <td>시계/귀금속소매</td>
      <td>학원-보습교습입시</td>
      <td>한식</td>
    </tr>
    <tr>
      <th>상권업종소분류명</th>
      <td>건강원</td>
      <td>악기판매</td>
      <td>시계/귀금속</td>
      <td>학원-입시</td>
      <td>한식/백반/한정식</td>
    </tr>
    <tr>
      <th>시도명</th>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
      <td>서울특별시</td>
    </tr>
    <tr>
      <th>시군구명</th>
      <td>영등포구</td>
      <td>성동구</td>
      <td>종로구</td>
      <td>송파구</td>
      <td>서초구</td>
    </tr>
    <tr>
      <th>행정동명</th>
      <td>영등포동</td>
      <td>용답동</td>
      <td>종로1.2.3.4가동</td>
      <td>방이1동</td>
      <td>방배4동</td>
    </tr>
    <tr>
      <th>법정동명</th>
      <td>영등포동5가</td>
      <td>용답동</td>
      <td>봉익동</td>
      <td>방이동</td>
      <td>방배동</td>
    </tr>
    <tr>
      <th>대지구분명</th>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
      <td>대지</td>
    </tr>
    <tr>
      <th>지번본번지</th>
      <td>41</td>
      <td>142</td>
      <td>43</td>
      <td>197</td>
      <td>854</td>
    </tr>
    <tr>
      <th>지번주소</th>
      <td>서울특별시 영등포구 영등포동5가 41-1</td>
      <td>서울특별시 성동구 용답동 142-11</td>
      <td>서울특별시 종로구 봉익동 43-1</td>
      <td>서울특별시 송파구 방이동 197-3</td>
      <td>서울특별시 서초구 방배동 854-18</td>
    </tr>
    <tr>
      <th>도로명</th>
      <td>서울특별시 영등포구 영중로14길</td>
      <td>서울특별시 성동구 용답5길</td>
      <td>서울특별시 종로구 서순라길</td>
      <td>서울특별시 송파구 위례성대로12길</td>
      <td>서울특별시 서초구 동광로18길</td>
    </tr>
    <tr>
      <th>건물본번지</th>
      <td>11</td>
      <td>2</td>
      <td>17</td>
      <td>31</td>
      <td>82</td>
    </tr>
    <tr>
      <th>도로명주소</th>
      <td>서울특별시 영등포구 영중로14길 11-17, (영등포동5가)</td>
      <td>서울특별시 성동구 용답5길 2, (용답동)</td>
      <td>서울특별시 종로구 서순라길 17-10, (봉익동)</td>
      <td>서울특별시 송파구 위례성대로12길 31, (방이동)</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
    </tr>
    <tr>
      <th>경도</th>
      <td>126.907</td>
      <td>127.049</td>
      <td>126.994</td>
      <td>127.122</td>
      <td>126.991</td>
    </tr>
    <tr>
      <th>위도</th>
      <td>37.5206</td>
      <td>37.5669</td>
      <td>37.5718</td>
      <td>37.511</td>
      <td>37.4884</td>
    </tr>
  </tbody>
</table>
</div>

```python
sales.drop(['상가업소번호', '상권업종대분류코드', '상권업종중분류코드', '상권업종소분류코드', '시도코드', '시군구코드', '행정동코드',
             '법정동코드', '지번코드', '대지구분코드', '도로명코드', '건물관리번호', '구우편번호', '신우편번호'], axis = 1, inplace = True)
```

```python
sales.info()
```

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 361490 entries, 0 to 361489
Data columns (total 16 columns):
 #   Column    Non-Null Count   Dtype  
---  ------    --------------   -----  
 0   상호명       361490 non-null  object 
 1   상권업종대분류명  361490 non-null  object 
 2   상권업종중분류명  361490 non-null  object 
 3   상권업종소분류명  361490 non-null  object 
 4   시도명       361490 non-null  object 
 5   시군구명      361490 non-null  object 
 6   행정동명      361490 non-null  object 
 7   법정동명      361490 non-null  object 
 8   대지구분명     361490 non-null  object 
 9   지번본번지     361490 non-null  int64  
 10  지번주소      361490 non-null  object 
 11  도로명       361490 non-null  object 
 12  건물본번지     361490 non-null  int64  
 13  도로명주소     361490 non-null  object 
 14  경도        361490 non-null  float64
 15  위도        361490 non-null  float64
dtypes: float64(2), int64(2), object(12)
memory usage: 44.1+ MB
```

## Step 3: 데이터 탐색 (Exploratory Data Analysis)

데이터의 패턴을 찾고, 관계를 시각화 하는 작업 등으로 통해 데이터에 대한 직관을 극대화 한다.

```python
sales.head()
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
      <th>상호명</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류명</th>
      <th>시도명</th>
      <th>시군구명</th>
      <th>행정동명</th>
      <th>법정동명</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번주소</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>도로명주소</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>제중건강원</td>
      <td>소매</td>
      <td>건강/미용식품</td>
      <td>건강원</td>
      <td>서울특별시</td>
      <td>영등포구</td>
      <td>영등포동</td>
      <td>영등포동5가</td>
      <td>대지</td>
      <td>41</td>
      <td>서울특별시 영등포구 영등포동5가 41-1</td>
      <td>서울특별시 영등포구 영중로14길</td>
      <td>11</td>
      <td>서울특별시 영등포구 영중로14길 11-17, (영등포동5가)</td>
      <td>126.907168</td>
      <td>37.520613</td>
    </tr>
    <tr>
      <th>1</th>
      <td>민속악기사</td>
      <td>소매</td>
      <td>취미/오락관련소매</td>
      <td>악기판매</td>
      <td>서울특별시</td>
      <td>성동구</td>
      <td>용답동</td>
      <td>용답동</td>
      <td>대지</td>
      <td>142</td>
      <td>서울특별시 성동구 용답동 142-11</td>
      <td>서울특별시 성동구 용답5길</td>
      <td>2</td>
      <td>서울특별시 성동구 용답5길 2, (용답동)</td>
      <td>127.049018</td>
      <td>37.566857</td>
    </tr>
    <tr>
      <th>2</th>
      <td>태평양진주</td>
      <td>소매</td>
      <td>시계/귀금속소매</td>
      <td>시계/귀금속</td>
      <td>서울특별시</td>
      <td>종로구</td>
      <td>종로1.2.3.4가동</td>
      <td>봉익동</td>
      <td>대지</td>
      <td>43</td>
      <td>서울특별시 종로구 봉익동 43-1</td>
      <td>서울특별시 종로구 서순라길</td>
      <td>17</td>
      <td>서울특별시 종로구 서순라길 17-10, (봉익동)</td>
      <td>126.993530</td>
      <td>37.571848</td>
    </tr>
    <tr>
      <th>3</th>
      <td>김선희꼼꼼국어교습소</td>
      <td>학문/교육</td>
      <td>학원-보습교습입시</td>
      <td>학원-입시</td>
      <td>서울특별시</td>
      <td>송파구</td>
      <td>방이1동</td>
      <td>방이동</td>
      <td>대지</td>
      <td>197</td>
      <td>서울특별시 송파구 방이동 197-3</td>
      <td>서울특별시 송파구 위례성대로12길</td>
      <td>31</td>
      <td>서울특별시 송파구 위례성대로12길 31, (방이동)</td>
      <td>127.121520</td>
      <td>37.510967</td>
    </tr>
    <tr>
      <th>4</th>
      <td>비지트</td>
      <td>음식</td>
      <td>한식</td>
      <td>한식/백반/한정식</td>
      <td>서울특별시</td>
      <td>서초구</td>
      <td>방배4동</td>
      <td>방배동</td>
      <td>대지</td>
      <td>854</td>
      <td>서울특별시 서초구 방배동 854-18</td>
      <td>서울특별시 서초구 동광로18길</td>
      <td>82</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
      <td>126.991394</td>
      <td>37.488375</td>
    </tr>
  </tbody>
</table>
</div>

```python
sa_corr = sales.corr()
```

```python
f, ax = plt.subplots(figsize=(10, 6))
sns.heatmap(sa_corr, annot=True, fmt = '.2f', square=True);
```

![image](https://user-images.githubusercontent.com/84713532/204099298-5b150d6e-876f-4f92-b617-87de47d98d59.png)


**기술 통계 요약**

```python
sales.describe()
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
      <th>지번본번지</th>
      <th>건물본번지</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>361490.000000</td>
      <td>361490.000000</td>
      <td>361490.000000</td>
      <td>361490.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>422.386384</td>
      <td>139.732366</td>
      <td>126.993759</td>
      <td>37.544906</td>
    </tr>
    <tr>
      <th>std</th>
      <td>426.373510</td>
      <td>259.077055</td>
      <td>0.083937</td>
      <td>0.049022</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>126.768169</td>
      <td>37.434081</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>102.000000</td>
      <td>19.000000</td>
      <td>126.922367</td>
      <td>37.504588</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>301.000000</td>
      <td>46.000000</td>
      <td>127.009557</td>
      <td>37.542195</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>644.000000</td>
      <td>154.000000</td>
      <td>127.056107</td>
      <td>37.572518</td>
    </tr>
    <tr>
      <th>max</th>
      <td>9999.000000</td>
      <td>3581.000000</td>
      <td>127.182588</td>
      <td>37.690787</td>
    </tr>
  </tbody>
</table>
</div>

```python
sales.describe(include = 'object')
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
      <th>상호명</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류명</th>
      <th>시도명</th>
      <th>시군구명</th>
      <th>행정동명</th>
      <th>법정동명</th>
      <th>대지구분명</th>
      <th>지번주소</th>
      <th>도로명</th>
      <th>도로명주소</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
      <td>361490</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>263524</td>
      <td>8</td>
      <td>89</td>
      <td>677</td>
      <td>1</td>
      <td>25</td>
      <td>425</td>
      <td>463</td>
      <td>2</td>
      <td>134165</td>
      <td>12408</td>
      <td>133359</td>
    </tr>
    <tr>
      <th>top</th>
      <td>CU</td>
      <td>음식</td>
      <td>한식</td>
      <td>한식/백반/한정식</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>역삼1동</td>
      <td>역삼동</td>
      <td>대지</td>
      <td>서울특별시 종로구 종로6가 262-1</td>
      <td>서울특별시 종로구 종로</td>
      <td>서울특별시 종로구 종로 266, (종로6가)</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1702</td>
      <td>121534</td>
      <td>39624</td>
      <td>29155</td>
      <td>361490</td>
      <td>35511</td>
      <td>6628</td>
      <td>8292</td>
      <td>361232</td>
      <td>892</td>
      <td>2263</td>
      <td>898</td>
    </tr>
  </tbody>
</table>
</div>

### 3.1 히스토그램으로 수치 데이터의 분포 한눈에 확인하기

- **히스토그램(histogram)** : 수치형 데이터의 구간별 빈도수를 나타내는 그래프

지번본번지, 건물본번지, 경도, 위도

```python
sales[['지번본번지', '건물본번지', '경도', '위도']].hist(figsize = (10, 6))
```

```
array([[<AxesSubplot:title={'center':'지번본번지'}>,
        <AxesSubplot:title={'center':'건물본번지'}>],
       [<AxesSubplot:title={'center':'경도'}>,
        <AxesSubplot:title={'center':'위도'}>]], dtype=object)
```

![image](https://user-images.githubusercontent.com/84713532/204099342-15531a25-542e-4b04-be98-e2c466af67b1.png)


### 3.2 상관 계수로 두 변량간의 관계 파악하기

```python
sales.corr()
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
      <th>지번본번지</th>
      <th>건물본번지</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>지번본번지</th>
      <td>1.000000</td>
      <td>0.079527</td>
      <td>-0.143662</td>
      <td>-0.215020</td>
    </tr>
    <tr>
      <th>건물본번지</th>
      <td>0.079527</td>
      <td>1.000000</td>
      <td>0.061893</td>
      <td>-0.005848</td>
    </tr>
    <tr>
      <th>경도</th>
      <td>-0.143662</td>
      <td>0.061893</td>
      <td>1.000000</td>
      <td>0.155010</td>
    </tr>
    <tr>
      <th>위도</th>
      <td>-0.215020</td>
      <td>-0.005848</td>
      <td>0.155010</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>

```python
corr = df.corr()
```

```python
sns.heatmap(corr, annot=True, fmt='.2f', linewidths=0.5, cmap='YlGnBu')
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/204099376-a17ac641-52d4-4a34-9591-8bcd5c694e2e.png)


```python
df.plot(kind='scatter', x='경도', y='위도', alpha=0.1) 
```

```
<AxesSubplot:xlabel='경도', ylabel='위도'>
```

![image](https://user-images.githubusercontent.com/84713532/204099394-e22c2a2d-dac5-4268-8447-63cf6a558951.png)


- [컬러맵 정보](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

### 3.3 문자열 데이터에 대한 요약

- 상권업종대분류명 요약

```python
sales['상권업종대분류명'].describe()
```

```
count     361490
unique         8
top           음식
freq      121534
Name: 상권업종대분류명, dtype: object
```

- 상권업종대분류명 의 unique 값

```python
sales['상권업종대분류명'].unique()
```

```
array(['소매', '학문/교육', '음식', '부동산', '생활서비스', '관광/여가/오락', '숙박', '스포츠'],
      dtype=object)
```

- 상권업종대분류명 의 unique 값의 갯수

```python
sales['상권업종대분류명'].nunique()
```

```
8
```

- 상권업종대분류명 의 최빈값

```python
sales['상권업종대분류명'].mode()
```

```
0    음식
Name: 상권업종대분류명, dtype: object
```

- 상권업종대분류명 의 빈도수

```python
sales['상권업종대분류명'].value_counts()
```

```
음식          121534
소매          103889
생활서비스        74450
학문/교육        26193
부동산          18600
관광/여가/오락      9167
스포츠           5290
숙박            2367
Name: 상권업종대분류명, dtype: int64
```

### 3.4 구별 음식점 업종 비교하기

#### (1) 서초구에는 어떤 음식점 업종이 많을까?

- 서초구에서 상권업종대분류명이 음식인 데이터만 가져오기

```python
a = sales[(sales['상권업종대분류명'] == '음식') & (sales['시군구명'] == '서초구')]
a
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
      <th>상가업소번호</th>
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도코드</th>
      <th>시도명</th>
      <th>시군구코드</th>
      <th>시군구명</th>
      <th>행정동코드</th>
      <th>행정동명</th>
      <th>법정동코드</th>
      <th>법정동명</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>지번주소</th>
      <th>도로명코드</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>동정보</th>
      <th>층정보</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>17174175</td>
      <td>비지트</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165062100</td>
      <td>방배4동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100108540018</td>
      <td>1</td>
      <td>대지</td>
      <td>854</td>
      <td>18.0</td>
      <td>서울특별시 서초구 방배동 854-18</td>
      <td>116504163117</td>
      <td>서울특별시 서초구 동광로18길</td>
      <td>82</td>
      <td>NaN</td>
      <td>1165010100108540018009586</td>
      <td>상랑의빌딩</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
      <td>137837</td>
      <td>6572</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.991394</td>
      <td>37.488375</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17174040</td>
      <td>다향</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165053000</td>
      <td>서초3동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800114850003</td>
      <td>1</td>
      <td>대지</td>
      <td>1485</td>
      <td>3.0</td>
      <td>서울특별시 서초구 서초동 1485-3</td>
      <td>116503121021</td>
      <td>서울특별시 서초구 효령로</td>
      <td>230</td>
      <td>NaN</td>
      <td>1165010800114850004022127</td>
      <td>NaN</td>
      <td>서울특별시 서초구 효령로 230, (서초동)</td>
      <td>137869</td>
      <td>6709</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.009382</td>
      <td>37.483436</td>
    </tr>
    <tr>
      <th>24</th>
      <td>28478395</td>
      <td>장수식당</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165054000</td>
      <td>잠원동</td>
      <td>1165010600</td>
      <td>잠원동</td>
      <td>1165010600100290003</td>
      <td>1</td>
      <td>대지</td>
      <td>29</td>
      <td>3.0</td>
      <td>서울특별시 서초구 잠원동 29-3</td>
      <td>116504163039</td>
      <td>서울특별시 서초구 강남대로95길</td>
      <td>17</td>
      <td>NaN</td>
      <td>1165010600100290003019323</td>
      <td>아람빌딩</td>
      <td>서울특별시 서초구 강남대로95길 17, (잠원동)</td>
      <td>137904</td>
      <td>6530</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.018983</td>
      <td>37.513638</td>
    </tr>
    <tr>
      <th>32</th>
      <td>28503146</td>
      <td>북경깐풍기</td>
      <td>강남점</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q02</td>
      <td>중식</td>
      <td>Q02A00</td>
      <td>중국음식/중국집</td>
      <td>I56112</td>
      <td>중식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165053100</td>
      <td>서초4동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800113070018</td>
      <td>1</td>
      <td>대지</td>
      <td>1307</td>
      <td>18.0</td>
      <td>서울특별시 서초구 서초동 1307-18</td>
      <td>116504163029</td>
      <td>서울특별시 서초구 강남대로65길</td>
      <td>7</td>
      <td>NaN</td>
      <td>1165010800113070018027310</td>
      <td>피렌체타워</td>
      <td>서울특별시 서초구 강남대로65길 7, (서초동)</td>
      <td>137856</td>
      <td>6614</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.025310</td>
      <td>37.500247</td>
    </tr>
    <tr>
      <th>60</th>
      <td>28490126</td>
      <td>라이브존레스토랑</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q06</td>
      <td>양식</td>
      <td>Q06A05</td>
      <td>패밀리레스토랑</td>
      <td>I56114</td>
      <td>서양식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165058100</td>
      <td>반포4동</td>
      <td>1165010700</td>
      <td>반포동</td>
      <td>1165010700100830016</td>
      <td>1</td>
      <td>대지</td>
      <td>83</td>
      <td>16.0</td>
      <td>서울특별시 서초구 반포동 83-16</td>
      <td>116504163135</td>
      <td>서울특별시 서초구 동광로49길</td>
      <td>7</td>
      <td>NaN</td>
      <td>1165010700100830016017148</td>
      <td>양지빌딩</td>
      <td>서울특별시 서초구 동광로49길 7, (반포동)</td>
      <td>137805</td>
      <td>6580</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.001978</td>
      <td>37.493519</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>361185</th>
      <td>18756327</td>
      <td>마실</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q09</td>
      <td>유흥주점</td>
      <td>Q09A03</td>
      <td>꼬치구이전문점</td>
      <td>I56219</td>
      <td>기타 주점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165056000</td>
      <td>반포1동</td>
      <td>1165010700</td>
      <td>반포동</td>
      <td>1165010700107050007</td>
      <td>1</td>
      <td>대지</td>
      <td>705</td>
      <td>7.0</td>
      <td>서울특별시 서초구 반포동 705-7</td>
      <td>116503121017</td>
      <td>서울특별시 서초구 신반포로</td>
      <td>326</td>
      <td>13.0</td>
      <td>1165010700107050007018441</td>
      <td>NaN</td>
      <td>서울특별시 서초구 신반포로 326-13, (반포동)</td>
      <td>137808</td>
      <td>6534</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.019767</td>
      <td>37.509869</td>
    </tr>
    <tr>
      <th>361258</th>
      <td>18751482</td>
      <td>커피앤와플타임</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165052000</td>
      <td>서초2동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800113600006</td>
      <td>1</td>
      <td>대지</td>
      <td>1360</td>
      <td>6.0</td>
      <td>서울특별시 서초구 서초동 1360-6</td>
      <td>116504163084</td>
      <td>서울특별시 서초구 남부순환로347길</td>
      <td>48</td>
      <td>7.0</td>
      <td>1165010800113600006022817</td>
      <td>NaN</td>
      <td>서울특별시 서초구 남부순환로347길 48-7, (서초동)</td>
      <td>137863</td>
      <td>6730</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.031458</td>
      <td>37.486619</td>
    </tr>
    <tr>
      <th>361302</th>
      <td>18749956</td>
      <td>클립커피</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165056000</td>
      <td>반포1동</td>
      <td>1165010700</td>
      <td>반포동</td>
      <td>1165010700107050007</td>
      <td>1</td>
      <td>대지</td>
      <td>705</td>
      <td>7.0</td>
      <td>서울특별시 서초구 반포동 705-7</td>
      <td>116503121017</td>
      <td>서울특별시 서초구 신반포로</td>
      <td>326</td>
      <td>13.0</td>
      <td>1165010700107050007018441</td>
      <td>NaN</td>
      <td>서울특별시 서초구 신반포로 326-13, (반포동)</td>
      <td>137808</td>
      <td>6534</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.019767</td>
      <td>37.509869</td>
    </tr>
    <tr>
      <th>361304</th>
      <td>18769884</td>
      <td>서래셀부루</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q09</td>
      <td>유흥주점</td>
      <td>Q09A10</td>
      <td>룸살롱/단란주점</td>
      <td>I56211</td>
      <td>일반유흥 주점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165062100</td>
      <td>방배4동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100108130007</td>
      <td>1</td>
      <td>대지</td>
      <td>813</td>
      <td>7.0</td>
      <td>서울특별시 서초구 방배동 813-7</td>
      <td>116503121004</td>
      <td>서울특별시 서초구 동광로</td>
      <td>70</td>
      <td>NaN</td>
      <td>1165010100108130007008789</td>
      <td>NaN</td>
      <td>서울특별시 서초구 동광로 70, (방배동)</td>
      <td>137832</td>
      <td>6562</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.990252</td>
      <td>37.492591</td>
    </tr>
    <tr>
      <th>361486</th>
      <td>18773993</td>
      <td>챔프컴퍼니</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165060000</td>
      <td>방배1동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100109380024</td>
      <td>1</td>
      <td>대지</td>
      <td>938</td>
      <td>24.0</td>
      <td>서울특별시 서초구 방배동 938-24</td>
      <td>116504163259</td>
      <td>서울특별시 서초구 방배로23길</td>
      <td>32</td>
      <td>4.0</td>
      <td>1165010100109380024014572</td>
      <td>NaN</td>
      <td>서울특별시 서초구 방배로23길 32-4, (방배동)</td>
      <td>137844</td>
      <td>6673</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.992590</td>
      <td>37.486042</td>
    </tr>
  </tbody>
</table>
<p>6118 rows × 39 columns</p>
</div>

```python
a.describe(include = 'object')
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
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도명</th>
      <th>시군구명</th>
      <th>행정동명</th>
      <th>법정동명</th>
      <th>대지구분명</th>
      <th>지번주소</th>
      <th>도로명</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>동정보</th>
      <th>층정보</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6118</td>
      <td>1771</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6103</td>
      <td>6103</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>6118</td>
      <td>3963</td>
      <td>6118</td>
      <td>365</td>
      <td>4684</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>5406</td>
      <td>559</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>14</td>
      <td>99</td>
      <td>99</td>
      <td>16</td>
      <td>16</td>
      <td>1</td>
      <td>1</td>
      <td>18</td>
      <td>10</td>
      <td>1</td>
      <td>3064</td>
      <td>450</td>
      <td>3046</td>
      <td>1471</td>
      <td>3048</td>
      <td>73</td>
      <td>33</td>
    </tr>
    <tr>
      <th>top</th>
      <td>카페</td>
      <td>서초점</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>서울특별시</td>
      <td>서초구</td>
      <td>서초3동</td>
      <td>서초동</td>
      <td>대지</td>
      <td>서울특별시 서초구 반포동 19-3</td>
      <td>서울특별시 서초구 신반포로</td>
      <td>1165010700100190003000001</td>
      <td>강남고속버스터미널</td>
      <td>서울특별시 서초구 신반포로 176, (반포동)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>43</td>
      <td>143</td>
      <td>6118</td>
      <td>6118</td>
      <td>1966</td>
      <td>1966</td>
      <td>1511</td>
      <td>1511</td>
      <td>2296</td>
      <td>2296</td>
      <td>6118</td>
      <td>6118</td>
      <td>843</td>
      <td>2199</td>
      <td>6118</td>
      <td>109</td>
      <td>349</td>
      <td>109</td>
      <td>61</td>
      <td>109</td>
      <td>118</td>
      <td>3544</td>
    </tr>
  </tbody>
</table>
</div>

```python
a["상권업종중분류명"].value_counts()
```

```
한식         1966
커피점/카페     1205
분식          520
유흥주점        452
일식/수산물      449
양식          407
패스트푸드       277
제과제빵떡케익     260
닭/오리요리      213
중식          183
별식/퓨전요리     141
기타음식업        23
부페           17
음식배달서비스       5
Name: 상권업종중분류명, dtype: int64
```

```python
a["상권업종중분류명"].value_counts().plot(kind='barh', figsize=(6, 6))
```

```
<AxesSubplot:>
```

![image](https://user-images.githubusercontent.com/84713532/204099453-77371900-ae0e-4052-b727-6618c506ceca.png)


**분석결과** : 한식집이 가장 많다.

#### (2) 구별 업종(상권업종중분류명 기준) 분포 비교하기

- 상권업종대분류명 이 음식인 데이터 준비

```python
s = sales[(sales['상권업종대분류명'] == '음식')]
s
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
      <th>상가업소번호</th>
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도코드</th>
      <th>시도명</th>
      <th>시군구코드</th>
      <th>시군구명</th>
      <th>행정동코드</th>
      <th>행정동명</th>
      <th>법정동코드</th>
      <th>법정동명</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>지번주소</th>
      <th>도로명코드</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>동정보</th>
      <th>층정보</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>17174175</td>
      <td>비지트</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165062100</td>
      <td>방배4동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100108540018</td>
      <td>1</td>
      <td>대지</td>
      <td>854</td>
      <td>18.0</td>
      <td>서울특별시 서초구 방배동 854-18</td>
      <td>116504163117</td>
      <td>서울특별시 서초구 동광로18길</td>
      <td>82</td>
      <td>NaN</td>
      <td>1165010100108540018009586</td>
      <td>상랑의빌딩</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
      <td>137837</td>
      <td>6572</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.991394</td>
      <td>37.488375</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17174119</td>
      <td>쓰리에프</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11590</td>
      <td>동작구</td>
      <td>1159063000</td>
      <td>사당2동</td>
      <td>1159010700</td>
      <td>사당동</td>
      <td>1159010700101390072</td>
      <td>1</td>
      <td>대지</td>
      <td>139</td>
      <td>72.0</td>
      <td>서울특별시 동작구 사당동 139-72</td>
      <td>115904157119</td>
      <td>서울특별시 동작구 동작대로27가길</td>
      <td>12</td>
      <td>NaN</td>
      <td>1159010700101390073009536</td>
      <td>NaN</td>
      <td>서울특별시 동작구 동작대로27가길 12, (사당동)</td>
      <td>156816</td>
      <td>7008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.980952</td>
      <td>37.487105</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17174040</td>
      <td>다향</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165053000</td>
      <td>서초3동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800114850003</td>
      <td>1</td>
      <td>대지</td>
      <td>1485</td>
      <td>3.0</td>
      <td>서울특별시 서초구 서초동 1485-3</td>
      <td>116503121021</td>
      <td>서울특별시 서초구 효령로</td>
      <td>230</td>
      <td>NaN</td>
      <td>1165010800114850004022127</td>
      <td>NaN</td>
      <td>서울특별시 서초구 효령로 230, (서초동)</td>
      <td>137869</td>
      <td>6709</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.009382</td>
      <td>37.483436</td>
    </tr>
    <tr>
      <th>7</th>
      <td>25530299</td>
      <td>고향생막걸리</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q09</td>
      <td>유흥주점</td>
      <td>Q09A04</td>
      <td>민속주점</td>
      <td>I56219</td>
      <td>기타 주점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11680</td>
      <td>강남구</td>
      <td>1168054500</td>
      <td>압구정동</td>
      <td>1168010700</td>
      <td>신사동</td>
      <td>1168010700106150001</td>
      <td>1</td>
      <td>대지</td>
      <td>615</td>
      <td>1.0</td>
      <td>서울특별시 강남구 신사동 615-1</td>
      <td>116803122007</td>
      <td>서울특별시 강남구 압구정로</td>
      <td>216</td>
      <td>NaN</td>
      <td>1168010700106150001009703</td>
      <td>코끼리상가</td>
      <td>서울특별시 강남구 압구정로 216, (신사동)</td>
      <td>135894</td>
      <td>6023</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.031012</td>
      <td>37.528073</td>
    </tr>
    <tr>
      <th>12</th>
      <td>17163092</td>
      <td>도전최강달인왕만두</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11740</td>
      <td>강동구</td>
      <td>1174056000</td>
      <td>고덕2동</td>
      <td>1174010200</td>
      <td>고덕동</td>
      <td>1174010200106930000</td>
      <td>1</td>
      <td>대지</td>
      <td>693</td>
      <td>NaN</td>
      <td>서울특별시 강동구 고덕동 693</td>
      <td>117403124001</td>
      <td>서울특별시 강동구 고덕로</td>
      <td>333</td>
      <td>NaN</td>
      <td>1174010200102170000018014</td>
      <td>고덕그라시움</td>
      <td>서울특별시 강동구 고덕로 333, (고덕동, 고덕그라시움아파트)</td>
      <td>134082</td>
      <td>5224</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.159471</td>
      <td>37.556197</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>361472</th>
      <td>18760226</td>
      <td>댄싱컵</td>
      <td>가재울점</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11410</td>
      <td>서대문구</td>
      <td>1141070000</td>
      <td>남가좌2동</td>
      <td>1141012000</td>
      <td>남가좌동</td>
      <td>1141012000103900000</td>
      <td>1</td>
      <td>대지</td>
      <td>390</td>
      <td>NaN</td>
      <td>서울특별시 서대문구 남가좌동 390</td>
      <td>114103112003</td>
      <td>서울특별시 서대문구 거북골로</td>
      <td>100</td>
      <td>NaN</td>
      <td>1141012000101750000005766</td>
      <td>래미안루센티아</td>
      <td>서울특별시 서대문구 거북골로 100, (남가좌동, 래미안루센티아)</td>
      <td>120122</td>
      <td>3689</td>
      <td>상가</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.918228</td>
      <td>37.575633</td>
    </tr>
    <tr>
      <th>361480</th>
      <td>18759187</td>
      <td>플랫카페</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11215</td>
      <td>광진구</td>
      <td>1121585000</td>
      <td>구의1동</td>
      <td>1121510300</td>
      <td>구의동</td>
      <td>1121510300106350002</td>
      <td>1</td>
      <td>대지</td>
      <td>635</td>
      <td>2.0</td>
      <td>서울특별시 광진구 구의동 635-2</td>
      <td>112154112427</td>
      <td>서울특별시 광진구 자양로23길</td>
      <td>73</td>
      <td>NaN</td>
      <td>1121510300106350002010237</td>
      <td>에프앤빌딩(F&BUILDING)</td>
      <td>서울특별시 광진구 자양로23길 73, (구의동)</td>
      <td>143835</td>
      <td>5023</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.083681</td>
      <td>37.543595</td>
    </tr>
    <tr>
      <th>361483</th>
      <td>18760042</td>
      <td>산마을쌈밥집</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11380</td>
      <td>은평구</td>
      <td>1138053000</td>
      <td>불광2동</td>
      <td>1138010300</td>
      <td>불광동</td>
      <td>1138010300101570001</td>
      <td>1</td>
      <td>대지</td>
      <td>157</td>
      <td>1.0</td>
      <td>서울특별시 은평구 불광동 157-1</td>
      <td>113803111004</td>
      <td>서울특별시 은평구 불광로</td>
      <td>181</td>
      <td>NaN</td>
      <td>1138010300101570001036927</td>
      <td>NaN</td>
      <td>서울특별시 은평구 불광로 181, (불광동)</td>
      <td>122852</td>
      <td>3346</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>126.930927</td>
      <td>37.622557</td>
    </tr>
    <tr>
      <th>361484</th>
      <td>18757537</td>
      <td>달래해장종각점1호</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A05</td>
      <td>해장국/감자탕</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11110</td>
      <td>종로구</td>
      <td>1111061500</td>
      <td>종로1.2.3.4가동</td>
      <td>1111013500</td>
      <td>관철동</td>
      <td>1111013500100180003</td>
      <td>1</td>
      <td>대지</td>
      <td>18</td>
      <td>3.0</td>
      <td>서울특별시 종로구 관철동 18-3</td>
      <td>111104100214</td>
      <td>서울특별시 종로구 우정국로2길</td>
      <td>41</td>
      <td>NaN</td>
      <td>1111013500100180003000001</td>
      <td>NaN</td>
      <td>서울특별시 종로구 우정국로2길 41, (관철동)</td>
      <td>110111</td>
      <td>3189</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.985375</td>
      <td>37.569661</td>
    </tr>
    <tr>
      <th>361486</th>
      <td>18773993</td>
      <td>챔프컴퍼니</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165060000</td>
      <td>방배1동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100109380024</td>
      <td>1</td>
      <td>대지</td>
      <td>938</td>
      <td>24.0</td>
      <td>서울특별시 서초구 방배동 938-24</td>
      <td>116504163259</td>
      <td>서울특별시 서초구 방배로23길</td>
      <td>32</td>
      <td>4.0</td>
      <td>1165010100109380024014572</td>
      <td>NaN</td>
      <td>서울특별시 서초구 방배로23길 32-4, (방배동)</td>
      <td>137844</td>
      <td>6673</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.992590</td>
      <td>37.486042</td>
    </tr>
  </tbody>
</table>
<p>121534 rows × 39 columns</p>
</div>

```python
s.shape
```

```
(121534, 39)
```

- 시군구명, 상권업종중분류명 으로 그룹화 해서 상점수 개수 구하기

```python
ss = s.groupby(["시군구명", "상권업종중분류명"])["상호명"].count()
ss
```

```
시군구명  상권업종중분류명
강남구   기타음식업         49
      닭/오리요리       340
      별식/퓨전요리      224
      부페            47
      분식           751
                  ... 
중랑구   제과제빵떡케익      180
      중식            80
      커피점/카페       511
      패스트푸드        178
      한식          1247
Name: 상호명, Length: 348, dtype: int64
```

```python
food = ss.reset_index()
food = food.rename(columns={"상호명":"상호수"})
food
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
      <th>시군구명</th>
      <th>상권업종중분류명</th>
      <th>상호수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>강남구</td>
      <td>기타음식업</td>
      <td>49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>강남구</td>
      <td>닭/오리요리</td>
      <td>340</td>
    </tr>
    <tr>
      <th>2</th>
      <td>강남구</td>
      <td>별식/퓨전요리</td>
      <td>224</td>
    </tr>
    <tr>
      <th>3</th>
      <td>강남구</td>
      <td>부페</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>강남구</td>
      <td>분식</td>
      <td>751</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>343</th>
      <td>중랑구</td>
      <td>제과제빵떡케익</td>
      <td>180</td>
    </tr>
    <tr>
      <th>344</th>
      <td>중랑구</td>
      <td>중식</td>
      <td>80</td>
    </tr>
    <tr>
      <th>345</th>
      <td>중랑구</td>
      <td>커피점/카페</td>
      <td>511</td>
    </tr>
    <tr>
      <th>346</th>
      <td>중랑구</td>
      <td>패스트푸드</td>
      <td>178</td>
    </tr>
    <tr>
      <th>347</th>
      <td>중랑구</td>
      <td>한식</td>
      <td>1247</td>
    </tr>
  </tbody>
</table>
<p>348 rows × 3 columns</p>
</div>

- 전체 업종별 평균 시각화하기

```python
aaa = ss.groupby(['상권업종중분류명']).mean()
aaa
```

```
상권업종중분류명
기타음식업        18.200000
닭/오리요리      227.040000
별식/퓨전요리     104.680000
부페           16.440000
분식          397.800000
양식          281.920000
유흥주점        465.520000
음식배달서비스       3.565217
일식/수산물      329.240000
제과제빵떡케익     215.600000
중식          147.600000
커피점/카페      833.680000
패스트푸드       235.400000
한식         1584.960000
Name: 상호명, dtype: float64
```

```python
plt.figure(figsize=(12, 6))
sns.barplot(data=food, x="상권업종중분류명", y="상호수")
```

```
<AxesSubplot:xlabel='상권업종중분류명', ylabel='상호수'>
```

![image](https://user-images.githubusercontent.com/84713532/204099487-86d87d91-be63-4e94-96fa-02e12a788cfd.png)


- 상권업종중분류명에 따른 상호수를 시각화하되 시군구명별로 모두 표시 (sns.catplot 이용)

```python
sns.catplot(data=food, y="상권업종중분류명", x="상호수",
            col='시군구명', kind='bar', col_wrap=3, sharex=False)
```

```
<seaborn.axisgrid.FacetGrid at 0x287501ca0a0>
```

![image](https://user-images.githubusercontent.com/84713532/204099994-d21b8eb2-5857-4326-bd65-b86c28dad728.png)
![image](https://user-images.githubusercontent.com/84713532/204100018-12cf72c3-2050-4365-9d92-3e73cbf83dff.png)
![image](https://user-images.githubusercontent.com/84713532/204100036-31792ad0-9a3a-408f-b0db-2339e78f9328.png)
![image](https://user-images.githubusercontent.com/84713532/204100049-4acb0874-ce35-4d75-acea-e146e4ca004a.png)
![image](https://user-images.githubusercontent.com/84713532/204100066-d3f9de62-c39c-41e2-a7d4-bb00d6158c8c.png)
![image](https://user-images.githubusercontent.com/84713532/204100070-99498a18-6593-4d75-9d2b-a7e46fcb1291.png)
![image](https://user-images.githubusercontent.com/84713532/204100080-0f1fadf7-de34-4b45-98d6-d06adb072423.png)
![image](https://user-images.githubusercontent.com/84713532/204100091-9ac0ee41-1b2f-4028-ba4a-3016e2ed0e3c.png)
![image](https://user-images.githubusercontent.com/84713532/204100110-a967d5fc-c06c-47f2-8ca1-c7ab359c05a9.png)

```
분석결과 : 대부분의 구에서 한식->커피점/카페->유흥주점 순으로 상점수가 
많으나 강남구와 중구의 경우 유흥주점보다 양식 업종이 더 많았으며 송파구의 경우에도 유흥주점보다 분식 업종이 더 많음
```

```python
plt.figure(figsize = (24,16))
sns.catplot(data = s, y = '시군구명', x = '상권업종중분류명')
```

```
<seaborn.axisgrid.FacetGrid at 0x208c02f7a30>


<Figure size 1728x1152 with 0 Axes>
```

![image](https://user-images.githubusercontent.com/84713532/204099924-fa289bb0-6b2d-471b-92ca-36c24e0ac868.png)


**분석결과** : 이게 뭐꼬

### 3.5 구별 학원수 비교하기

#### (1) 어느 구에 학원수가 많을까?

- 상권업종대분류명의 unique 값

```python
sales['상권업종대분류명'].unique()
```

```
array(['소매', '학문/교육', '음식', '부동산', '생활서비스', '관광/여가/오락', '숙박', '스포츠'],
      dtype=object)
```

- 상권업종대분류명이 학문/교육인 데이터 가져오기

```python
a = sales[(sales['상권업종대분류명'] == '학문/교육')].copy()
a
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
      <th>상가업소번호</th>
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도코드</th>
      <th>시도명</th>
      <th>시군구코드</th>
      <th>시군구명</th>
      <th>행정동코드</th>
      <th>행정동명</th>
      <th>법정동코드</th>
      <th>법정동명</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>지번주소</th>
      <th>도로명코드</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>동정보</th>
      <th>층정보</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>15554136</td>
      <td>김선희꼼꼼국어교습소</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R01</td>
      <td>학원-보습교습입시</td>
      <td>R01A01</td>
      <td>학원-입시</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11710</td>
      <td>송파구</td>
      <td>1171056100</td>
      <td>방이1동</td>
      <td>1171011100</td>
      <td>방이동</td>
      <td>1171011100101970003</td>
      <td>1</td>
      <td>대지</td>
      <td>197</td>
      <td>3.0</td>
      <td>서울특별시 송파구 방이동 197-3</td>
      <td>117104169448</td>
      <td>서울특별시 송파구 위례성대로12길</td>
      <td>31</td>
      <td>NaN</td>
      <td>1171011100101970003017195</td>
      <td>NaN</td>
      <td>서울특별시 송파구 위례성대로12길 31, (방이동)</td>
      <td>138834</td>
      <td>5640</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>127.121520</td>
      <td>37.510967</td>
    </tr>
    <tr>
      <th>8</th>
      <td>21938782</td>
      <td>무비디자인</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R02</td>
      <td>학원-창업취업취미</td>
      <td>R02A12</td>
      <td>학원-디자인</td>
      <td>P85659</td>
      <td>기타 기술 및 직업훈련학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11440</td>
      <td>마포구</td>
      <td>1144060000</td>
      <td>대흥동</td>
      <td>1144011000</td>
      <td>노고산동</td>
      <td>1144011000101070017</td>
      <td>1</td>
      <td>대지</td>
      <td>107</td>
      <td>17.0</td>
      <td>서울특별시 마포구 노고산동 107-17</td>
      <td>114403005016</td>
      <td>서울특별시 마포구 백범로</td>
      <td>8</td>
      <td>NaN</td>
      <td>1144011000101070017018922</td>
      <td>우정마샹스오피스텔</td>
      <td>서울특별시 마포구 백범로 8, (노고산동)</td>
      <td>121807</td>
      <td>4100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.936717</td>
      <td>37.553996</td>
    </tr>
    <tr>
      <th>18</th>
      <td>24676721</td>
      <td>힐리빙텔</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R10</td>
      <td>도서관/독서실</td>
      <td>R10A01</td>
      <td>독서실</td>
      <td>R90212</td>
      <td>독서실 운영업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11410</td>
      <td>서대문구</td>
      <td>1141058500</td>
      <td>신촌동</td>
      <td>1141011200</td>
      <td>대현동</td>
      <td>1141011200100370069</td>
      <td>1</td>
      <td>대지</td>
      <td>37</td>
      <td>69.0</td>
      <td>서울특별시 서대문구 대현동 37-69</td>
      <td>114104136319</td>
      <td>서울특별시 서대문구 이화여대5길</td>
      <td>28</td>
      <td>NaN</td>
      <td>1141011200100370069023867</td>
      <td>NaN</td>
      <td>서울특별시 서대문구 이화여대5길 28, (대현동)</td>
      <td>120808</td>
      <td>3766</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.944057</td>
      <td>37.558414</td>
    </tr>
    <tr>
      <th>19</th>
      <td>24462056</td>
      <td>김샘수학교습소</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R01</td>
      <td>학원-보습교습입시</td>
      <td>R01A01</td>
      <td>학원-입시</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11140</td>
      <td>중구</td>
      <td>1114065000</td>
      <td>신당5동</td>
      <td>1114016200</td>
      <td>신당동</td>
      <td>1114016200108510000</td>
      <td>1</td>
      <td>대지</td>
      <td>851</td>
      <td>NaN</td>
      <td>서울특별시 중구 신당동 851</td>
      <td>111404103396</td>
      <td>서울특별시 중구 퇴계로90길</td>
      <td>74</td>
      <td>NaN</td>
      <td>1114016200100610043000001</td>
      <td>래미안신당하이베르</td>
      <td>서울특별시 중구 퇴계로90길 74, (신당동, 래미안하이베르아파트)</td>
      <td>100455</td>
      <td>4582</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.020965</td>
      <td>37.560996</td>
    </tr>
    <tr>
      <th>43</th>
      <td>24523198</td>
      <td>노바수학학원</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R01</td>
      <td>학원-보습교습입시</td>
      <td>R01A01</td>
      <td>학원-입시</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11680</td>
      <td>강남구</td>
      <td>1168074000</td>
      <td>일원2동</td>
      <td>1168010300</td>
      <td>개포동</td>
      <td>1168010300100120004</td>
      <td>1</td>
      <td>대지</td>
      <td>12</td>
      <td>4.0</td>
      <td>서울특별시 강남구 개포동 12-4</td>
      <td>116803122001</td>
      <td>서울특별시 강남구 개포로</td>
      <td>615</td>
      <td>NaN</td>
      <td>1168010300100120004019079</td>
      <td>석탑프라자</td>
      <td>서울특별시 강남구 개포로 615, (개포동)</td>
      <td>135939</td>
      <td>6335</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.075573</td>
      <td>37.492649</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>361396</th>
      <td>18760577</td>
      <td>발돋움국어</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R04</td>
      <td>학원-어학</td>
      <td>R04A01</td>
      <td>학원-외국어/어학</td>
      <td>P85502</td>
      <td>외국어학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11230</td>
      <td>동대문구</td>
      <td>1123072000</td>
      <td>휘경1동</td>
      <td>1123010900</td>
      <td>휘경동</td>
      <td>1123010900101830128</td>
      <td>1</td>
      <td>대지</td>
      <td>183</td>
      <td>128.0</td>
      <td>서울특별시 동대문구 휘경동 183-128</td>
      <td>112304115704</td>
      <td>서울특별시 동대문구 회기로29길</td>
      <td>12</td>
      <td>NaN</td>
      <td>1123010900101830128010104</td>
      <td>NaN</td>
      <td>서울특별시 동대문구 회기로29길 12, (휘경동)</td>
      <td>130876</td>
      <td>2444</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.058136</td>
      <td>37.590654</td>
    </tr>
    <tr>
      <th>361408</th>
      <td>18751729</td>
      <td>길동리드인독서논술교습소</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R09</td>
      <td>학원기타</td>
      <td>R09A01</td>
      <td>학원(종합)</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11740</td>
      <td>강동구</td>
      <td>1174068500</td>
      <td>길동</td>
      <td>1174010500</td>
      <td>길동</td>
      <td>1174010500101250008</td>
      <td>1</td>
      <td>대지</td>
      <td>125</td>
      <td>8.0</td>
      <td>서울특별시 강동구 길동 125-8</td>
      <td>117403124002</td>
      <td>서울특별시 강동구 명일로</td>
      <td>212</td>
      <td>NaN</td>
      <td>1174010500101250008002448</td>
      <td>앙페르빌딩</td>
      <td>서울특별시 강동구 명일로 212, (길동)</td>
      <td>134809</td>
      <td>5345</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.146159</td>
      <td>37.537513</td>
    </tr>
    <tr>
      <th>361414</th>
      <td>18762535</td>
      <td>공방순수</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R09</td>
      <td>학원기타</td>
      <td>R09A11</td>
      <td>학원-기타</td>
      <td>P85699</td>
      <td>그외 기타 분류안된 교육기관</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11620</td>
      <td>관악구</td>
      <td>1162060500</td>
      <td>은천동</td>
      <td>1162010100</td>
      <td>봉천동</td>
      <td>1162010100117180000</td>
      <td>1</td>
      <td>대지</td>
      <td>1718</td>
      <td>NaN</td>
      <td>서울특별시 관악구 봉천동 1718</td>
      <td>116203120009</td>
      <td>서울특별시 관악구 은천로</td>
      <td>93</td>
      <td>NaN</td>
      <td>1162010100117180000027810</td>
      <td>벽산블루밍아파트</td>
      <td>서울특별시 관악구 은천로 93, (봉천동, 벽산블루밍아파트)</td>
      <td>151778</td>
      <td>8715</td>
      <td>501</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.945884</td>
      <td>37.487337</td>
    </tr>
    <tr>
      <th>361467</th>
      <td>18778038</td>
      <td>수학교습소</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R01</td>
      <td>학원-보습교습입시</td>
      <td>R01A01</td>
      <td>학원-입시</td>
      <td>P85501</td>
      <td>일반 교과 학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11680</td>
      <td>강남구</td>
      <td>1168063000</td>
      <td>대치4동</td>
      <td>1168010600</td>
      <td>대치동</td>
      <td>1168010600109310001</td>
      <td>1</td>
      <td>대지</td>
      <td>931</td>
      <td>1.0</td>
      <td>서울특별시 강남구 대치동 931-1</td>
      <td>116804166420</td>
      <td>서울특별시 강남구 삼성로67길</td>
      <td>3</td>
      <td>NaN</td>
      <td>1168010600109310001013263</td>
      <td>NaN</td>
      <td>서울특별시 강남구 삼성로67길 3, (대치동)</td>
      <td>135998</td>
      <td>6203</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.059093</td>
      <td>37.501097</td>
    </tr>
    <tr>
      <th>361474</th>
      <td>18770562</td>
      <td>현매니지먼트</td>
      <td>NaN</td>
      <td>R</td>
      <td>학문/교육</td>
      <td>R04</td>
      <td>학원-어학</td>
      <td>R04A01</td>
      <td>학원-외국어/어학</td>
      <td>P85502</td>
      <td>외국어학원</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11680</td>
      <td>강남구</td>
      <td>1168053100</td>
      <td>논현2동</td>
      <td>1168010800</td>
      <td>논현동</td>
      <td>1168010800101130020</td>
      <td>1</td>
      <td>대지</td>
      <td>113</td>
      <td>20.0</td>
      <td>서울특별시 강남구 논현동 113-20</td>
      <td>116804166576</td>
      <td>서울특별시 강남구 언주로134길</td>
      <td>35</td>
      <td>NaN</td>
      <td>1168010800101130020005912</td>
      <td>NaN</td>
      <td>서울특별시 강남구 언주로134길 35, (논현동)</td>
      <td>135821</td>
      <td>6059</td>
      <td>NaN</td>
      <td>5</td>
      <td>NaN</td>
      <td>127.038392</td>
      <td>37.517267</td>
    </tr>
  </tbody>
</table>
<p>26193 rows × 39 columns</p>
</div>

- 시군구명으로 빈도수 구하기

```python
aaa = a['시군구명'].value_counts()
aaa
```

```
강남구     2586
송파구     1755
서초구     1699
양천구     1609
노원구     1495
강서구     1357
강동구     1341
은평구     1105
성북구     1102
마포구     1081
광진구     1059
관악구     1015
구로구     1010
동작구      998
영등포구     795
동대문구     779
중랑구      776
도봉구      759
서대문구     717
성동구      711
금천구      555
강북구      540
종로구      533
용산구      465
중구       351
Name: 시군구명, dtype: int64
```

- 빈도수 시각화하기

```python
plt.figure(figsize = (15,8))
sns.countplot(data = a, x = '시군구명')
```

```
<AxesSubplot:xlabel='시군구명', ylabel='count'>
```

![image](https://user-images.githubusercontent.com/84713532/204099562-0aa0ae62-1bfd-4bb7-9800-668bfaedf46c.png)


**분석 결과** : 역시 강남

#### (2) 구별 학원의 세부 업종 (상권업종소분류명 기준) 분포 비교하기

- 상권업종소분류명으로 빈도수를 구하기

```python
x = a['상권업종소분류명'].value_counts()
x
```

```
학원-입시        4858
학원-외국어/어학    3372
학원(종합)       3220
학원-기타        2606
어린이집         2429
             ... 
예절지도            1
학원-경찰           1
학원-용접기술         1
학원-텔렉스/통신       1
학원-자동차정비        1
Name: 상권업종소분류명, Length: 100, dtype: int64
```

- 상권업종소분류명 빈도수 기준 상위 4개만 가져오기

```python
x.iloc[0:4]
```

```
학원-입시        4858
학원-외국어/어학    3372
학원(종합)       3220
학원-기타        2606
Name: 상권업종소분류명, dtype: int64
```

```python
academy_top4 = a["상권업종소분류명"].value_counts().head(4)
academy_top4
```

```
학원-입시        4858
학원-외국어/어학    3372
학원(종합)       3220
학원-기타        2606
Name: 상권업종소분류명, dtype: int64
```

- 위에서 구한 상위 4개 업종으로만 데이터 가져오기

```python
y = sales[(sales['상권업종소분류명'] == '한식/백반/한정식') | (sales['상권업종소분류명'] == '커피전문점/카페/다방') | 
      (sales['상권업종소분류명'] == '부동산중개') | (sales['상권업종소분류명'] == '여성미용실')]
y
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
      <th>상가업소번호</th>
      <th>상호명</th>
      <th>지점명</th>
      <th>상권업종대분류코드</th>
      <th>상권업종대분류명</th>
      <th>상권업종중분류코드</th>
      <th>상권업종중분류명</th>
      <th>상권업종소분류코드</th>
      <th>상권업종소분류명</th>
      <th>표준산업분류코드</th>
      <th>표준산업분류명</th>
      <th>시도코드</th>
      <th>시도명</th>
      <th>시군구코드</th>
      <th>시군구명</th>
      <th>행정동코드</th>
      <th>행정동명</th>
      <th>법정동코드</th>
      <th>법정동명</th>
      <th>지번코드</th>
      <th>대지구분코드</th>
      <th>대지구분명</th>
      <th>지번본번지</th>
      <th>지번부번지</th>
      <th>지번주소</th>
      <th>도로명코드</th>
      <th>도로명</th>
      <th>건물본번지</th>
      <th>건물부번지</th>
      <th>건물관리번호</th>
      <th>건물명</th>
      <th>도로명주소</th>
      <th>구우편번호</th>
      <th>신우편번호</th>
      <th>동정보</th>
      <th>층정보</th>
      <th>호정보</th>
      <th>경도</th>
      <th>위도</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>17174175</td>
      <td>비지트</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165062100</td>
      <td>방배4동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100108540018</td>
      <td>1</td>
      <td>대지</td>
      <td>854</td>
      <td>18.0</td>
      <td>서울특별시 서초구 방배동 854-18</td>
      <td>116504163117</td>
      <td>서울특별시 서초구 동광로18길</td>
      <td>82</td>
      <td>NaN</td>
      <td>1165010100108540018009586</td>
      <td>상랑의빌딩</td>
      <td>서울특별시 서초구 동광로18길 82, (방배동)</td>
      <td>137837</td>
      <td>6572</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.991394</td>
      <td>37.488375</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17174119</td>
      <td>쓰리에프</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11590</td>
      <td>동작구</td>
      <td>1159063000</td>
      <td>사당2동</td>
      <td>1159010700</td>
      <td>사당동</td>
      <td>1159010700101390072</td>
      <td>1</td>
      <td>대지</td>
      <td>139</td>
      <td>72.0</td>
      <td>서울특별시 동작구 사당동 139-72</td>
      <td>115904157119</td>
      <td>서울특별시 동작구 동작대로27가길</td>
      <td>12</td>
      <td>NaN</td>
      <td>1159010700101390073009536</td>
      <td>NaN</td>
      <td>서울특별시 동작구 동작대로27가길 12, (사당동)</td>
      <td>156816</td>
      <td>7008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.980952</td>
      <td>37.487105</td>
    </tr>
    <tr>
      <th>6</th>
      <td>17174040</td>
      <td>다향</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165053000</td>
      <td>서초3동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800114850003</td>
      <td>1</td>
      <td>대지</td>
      <td>1485</td>
      <td>3.0</td>
      <td>서울특별시 서초구 서초동 1485-3</td>
      <td>116503121021</td>
      <td>서울특별시 서초구 효령로</td>
      <td>230</td>
      <td>NaN</td>
      <td>1165010800114850004022127</td>
      <td>NaN</td>
      <td>서울특별시 서초구 효령로 230, (서초동)</td>
      <td>137869</td>
      <td>6709</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.009382</td>
      <td>37.483436</td>
    </tr>
    <tr>
      <th>10</th>
      <td>22370147</td>
      <td>연세공인중개사사무소</td>
      <td>NaN</td>
      <td>L</td>
      <td>부동산</td>
      <td>L01</td>
      <td>부동산중개</td>
      <td>L01A01</td>
      <td>부동산중개</td>
      <td>L68221</td>
      <td>부동산 자문 및 중개업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11380</td>
      <td>은평구</td>
      <td>1138062500</td>
      <td>역촌동</td>
      <td>1138010800</td>
      <td>역촌동</td>
      <td>1138010800100170015</td>
      <td>1</td>
      <td>대지</td>
      <td>17</td>
      <td>15.0</td>
      <td>서울특별시 은평구 역촌동 17-15</td>
      <td>113803100020</td>
      <td>서울특별시 은평구 진흥로</td>
      <td>101</td>
      <td>NaN</td>
      <td>1138010800100170015017646</td>
      <td>NaN</td>
      <td>서울특별시 은평구 진흥로 101, (역촌동)</td>
      <td>122896</td>
      <td>3404</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.922332</td>
      <td>37.605891</td>
    </tr>
    <tr>
      <th>12</th>
      <td>17163092</td>
      <td>도전최강달인왕만두</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11740</td>
      <td>강동구</td>
      <td>1174056000</td>
      <td>고덕2동</td>
      <td>1174010200</td>
      <td>고덕동</td>
      <td>1174010200106930000</td>
      <td>1</td>
      <td>대지</td>
      <td>693</td>
      <td>NaN</td>
      <td>서울특별시 강동구 고덕동 693</td>
      <td>117403124001</td>
      <td>서울특별시 강동구 고덕로</td>
      <td>333</td>
      <td>NaN</td>
      <td>1174010200102170000018014</td>
      <td>고덕그라시움</td>
      <td>서울특별시 강동구 고덕로 333, (고덕동, 고덕그라시움아파트)</td>
      <td>134082</td>
      <td>5224</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>127.159471</td>
      <td>37.556197</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>361472</th>
      <td>18760226</td>
      <td>댄싱컵</td>
      <td>가재울점</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11410</td>
      <td>서대문구</td>
      <td>1141070000</td>
      <td>남가좌2동</td>
      <td>1141012000</td>
      <td>남가좌동</td>
      <td>1141012000103900000</td>
      <td>1</td>
      <td>대지</td>
      <td>390</td>
      <td>NaN</td>
      <td>서울특별시 서대문구 남가좌동 390</td>
      <td>114103112003</td>
      <td>서울특별시 서대문구 거북골로</td>
      <td>100</td>
      <td>NaN</td>
      <td>1141012000101750000005766</td>
      <td>래미안루센티아</td>
      <td>서울특별시 서대문구 거북골로 100, (남가좌동, 래미안루센티아)</td>
      <td>120122</td>
      <td>3689</td>
      <td>상가</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>126.918228</td>
      <td>37.575633</td>
    </tr>
    <tr>
      <th>361473</th>
      <td>18757169</td>
      <td>모수</td>
      <td>NaN</td>
      <td>L</td>
      <td>부동산</td>
      <td>L01</td>
      <td>부동산중개</td>
      <td>L01A01</td>
      <td>부동산중개</td>
      <td>L68221</td>
      <td>부동산 자문 및 중개업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165053000</td>
      <td>서초3동</td>
      <td>1165010800</td>
      <td>서초동</td>
      <td>1165010800115540009</td>
      <td>1</td>
      <td>대지</td>
      <td>1554</td>
      <td>9.0</td>
      <td>서울특별시 서초구 서초동 1554-9</td>
      <td>116504163239</td>
      <td>서울특별시 서초구 반포대로30길</td>
      <td>43</td>
      <td>NaN</td>
      <td>1165010800115540009020484</td>
      <td>알바트로스빌딩</td>
      <td>서울특별시 서초구 반포대로30길 43, (서초동)</td>
      <td>137873</td>
      <td>6646</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>127.010894</td>
      <td>37.492279</td>
    </tr>
    <tr>
      <th>361480</th>
      <td>18759187</td>
      <td>플랫카페</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q12</td>
      <td>커피점/카페</td>
      <td>Q12A01</td>
      <td>커피전문점/카페/다방</td>
      <td>I56220</td>
      <td>비알콜 음료점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11215</td>
      <td>광진구</td>
      <td>1121585000</td>
      <td>구의1동</td>
      <td>1121510300</td>
      <td>구의동</td>
      <td>1121510300106350002</td>
      <td>1</td>
      <td>대지</td>
      <td>635</td>
      <td>2.0</td>
      <td>서울특별시 광진구 구의동 635-2</td>
      <td>112154112427</td>
      <td>서울특별시 광진구 자양로23길</td>
      <td>73</td>
      <td>NaN</td>
      <td>1121510300106350002010237</td>
      <td>에프앤빌딩(F&BUILDING)</td>
      <td>서울특별시 광진구 자양로23길 73, (구의동)</td>
      <td>143835</td>
      <td>5023</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>127.083681</td>
      <td>37.543595</td>
    </tr>
    <tr>
      <th>361483</th>
      <td>18760042</td>
      <td>산마을쌈밥집</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11380</td>
      <td>은평구</td>
      <td>1138053000</td>
      <td>불광2동</td>
      <td>1138010300</td>
      <td>불광동</td>
      <td>1138010300101570001</td>
      <td>1</td>
      <td>대지</td>
      <td>157</td>
      <td>1.0</td>
      <td>서울특별시 은평구 불광동 157-1</td>
      <td>113803111004</td>
      <td>서울특별시 은평구 불광로</td>
      <td>181</td>
      <td>NaN</td>
      <td>1138010300101570001036927</td>
      <td>NaN</td>
      <td>서울특별시 은평구 불광로 181, (불광동)</td>
      <td>122852</td>
      <td>3346</td>
      <td>NaN</td>
      <td>2</td>
      <td>NaN</td>
      <td>126.930927</td>
      <td>37.622557</td>
    </tr>
    <tr>
      <th>361486</th>
      <td>18773993</td>
      <td>챔프컴퍼니</td>
      <td>NaN</td>
      <td>Q</td>
      <td>음식</td>
      <td>Q01</td>
      <td>한식</td>
      <td>Q01A01</td>
      <td>한식/백반/한정식</td>
      <td>I56111</td>
      <td>한식 음식점업</td>
      <td>11</td>
      <td>서울특별시</td>
      <td>11650</td>
      <td>서초구</td>
      <td>1165060000</td>
      <td>방배1동</td>
      <td>1165010100</td>
      <td>방배동</td>
      <td>1165010100109380024</td>
      <td>1</td>
      <td>대지</td>
      <td>938</td>
      <td>24.0</td>
      <td>서울특별시 서초구 방배동 938-24</td>
      <td>116504163259</td>
      <td>서울특별시 서초구 방배로23길</td>
      <td>32</td>
      <td>4.0</td>
      <td>1165010100109380024014572</td>
      <td>NaN</td>
      <td>서울특별시 서초구 방배로23길 32-4, (방배동)</td>
      <td>137844</td>
      <td>6673</td>
      <td>NaN</td>
      <td>1</td>
      <td>NaN</td>
      <td>126.992590</td>
      <td>37.486042</td>
    </tr>
  </tbody>
</table>
<p>80682 rows × 39 columns</p>
</div>

```python
df_academy_top4 = a[a["상권업종소분류명"].isin(academy_top4.index)].copy()
df_academy_top4.shape
```

```
(14056, 39)
```

```python
df_academy_top4["상권업종소분류명"].value_counts()
```

```
학원-입시        4858
학원-외국어/어학    3372
학원(종합)       3220
학원-기타        2606
Name: 상권업종소분류명, dtype: int64
```

- 상권업종소분류명, 시군구명으로 그룹화를 해서 빈도수 구하기

```python
academy_groupby = df_academy_top4.groupby(["상권업종소분류명", "시군구명"])["상호명"].count()
academy_groupby
```

```
상권업종소분류명  시군구명
학원(종합)    강남구     292
          강동구     148
          강북구      78
          강서구     187
          관악구      89
                 ... 
학원-입시     용산구      55
          은평구     223
          종로구      58
          중구       45
          중랑구     127
Name: 상호명, Length: 100, dtype: int64
```

```python
academy = academy_groupby.reset_index()
academy = academy.rename(columns={"상호명":"상호수"})
academy
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
      <th>상권업종소분류명</th>
      <th>시군구명</th>
      <th>상호수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>학원(종합)</td>
      <td>강남구</td>
      <td>292</td>
    </tr>
    <tr>
      <th>1</th>
      <td>학원(종합)</td>
      <td>강동구</td>
      <td>148</td>
    </tr>
    <tr>
      <th>2</th>
      <td>학원(종합)</td>
      <td>강북구</td>
      <td>78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>학원(종합)</td>
      <td>강서구</td>
      <td>187</td>
    </tr>
    <tr>
      <th>4</th>
      <td>학원(종합)</td>
      <td>관악구</td>
      <td>89</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>학원-입시</td>
      <td>용산구</td>
      <td>55</td>
    </tr>
    <tr>
      <th>96</th>
      <td>학원-입시</td>
      <td>은평구</td>
      <td>223</td>
    </tr>
    <tr>
      <th>97</th>
      <td>학원-입시</td>
      <td>종로구</td>
      <td>58</td>
    </tr>
    <tr>
      <th>98</th>
      <td>학원-입시</td>
      <td>중구</td>
      <td>45</td>
    </tr>
    <tr>
      <th>99</th>
      <td>학원-입시</td>
      <td>중랑구</td>
      <td>127</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 3 columns</p>
</div>

```python
sns.catplot(data=academy, x="상권업종소분류명", y="상호수", kind="bar", 
            col="시군구명", col_wrap=6, sharey=False)
```

```
<seaborn.axisgrid.FacetGrid at 0x2876704d9a0>
```

![image](https://user-images.githubusercontent.com/84713532/204099596-a809aa0e-e431-4d0c-8dd9-a66c47c6229d.png)


#### (3) 위치 정보 시각화하기

- 위에서 구한 데이터를 구별로 시각화

```python
plt.figure(figsize=(16, 10))
sns.scatterplot(data=df_academy_top4, x="경도", y="위도", hue="시군구명")
```

```
<AxesSubplot:xlabel='경도', ylabel='위도'>
```

![image](https://user-images.githubusercontent.com/84713532/204099622-a6357c79-72f9-45b6-8418-8632b61b88e1.png)


```python
plt.figure(figsize = (15,8))
sns.countplot(data = y, x = '시군구명')
```

```
<AxesSubplot:xlabel='시군구명', ylabel='count'>
```

![image](https://user-images.githubusercontent.com/84713532/204099635-22e971c8-99b2-4bcf-9772-a5e850a74282.png)


- 학원-입시 업종만 시각화

```python
plt.figure(figsize=(16, 10))
sns.scatterplot(
    data=df_academy_top4[df_academy_top4["상권업종소분류명"] == "학원-입시"], 
                x="경도", y="위도", hue="시군구명")
```

```
<AxesSubplot:xlabel='경도', ylabel='위도'>
```

![image](https://user-images.githubusercontent.com/84713532/204099652-55aaf074-c587-47fa-965d-9192842e3f2c.png)


- 강남구에 대해서만 시각화

```python
plt.figure(figsize=(10, 7))
sns.scatterplot(
    data=df_academy_top4[df_academy_top4["시군구명"] == "강남구"], 
                x="경도", y="위도", hue='법정동명')
```

```
<AxesSubplot:xlabel='경도', ylabel='위도'>
```

![image](https://user-images.githubusercontent.com/84713532/204099667-0e7513b1-5677-48d6-bedc-8fec0d73bab3.png)


- 관심 동네 비교해보기

```python
df_academy_top4.loc[
    df_academy_top4["법정동명"] == "대치동", 
    "상권업종소분류명"].value_counts()
```

```
학원-입시        313
학원-외국어/어학    117
학원-기타         95
학원(종합)        73
Name: 상권업종소분류명, dtype: int64
```

```python
df_academy_top4.loc[
    df_academy_top4["법정동명"] == "세곡동", 
    "상권업종소분류명"].value_counts()
```

```
학원(종합)       10
학원-입시         8
학원-기타         4
학원-외국어/어학     4
Name: 상권업종소분류명, dtype: int64
```

```python
df_academy_top4.loc[
    df_academy_top4["법정동명"] == "자곡동", 
    "상권업종소분류명"].value_counts()
```

```
학원-기타        12
학원-외국어/어학     4
학원(종합)        3
학원-입시         1
Name: 상권업종소분류명, dtype: int64
```
