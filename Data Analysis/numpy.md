## Numpy(넘파이) 개요
- Numpy는 Numerical Python의 줄임말
- 파이썬에서 산술 계산을 위한 가장 중요한 필수 패키지
- 효율적인 다차원 배열 ndarray는 빠른 배열 계산 지원
- 유연한 브로드캐스팅 기능 제공
- 반복문을 작성할 필요 없이 전체 데이터 배열을 빠르게 계산

## 0. Numpy 성능
```py
import numpy as np
```

```py
np.__version__
```

### 파이썬 리스트
```py
py_list = list(range(1000000))
```
### 넘파이 array
```py
np_array = np.arange(1000000)
```
```py
# result = []
# for a in py_list:
#   a2 = a * 2
#   result.append(a2)
```

```py
%timeit py_list2 = [a*2 for a in py_list] # 리스트 표기식
```

```py
%timeit np_array2 = np_array * 2 # 넘파이의 브로드캐스팅
```

## 1. Numpy ndarray (다차원 배열 객체)

### 1.1 ndarray 생성하기
```py
from IPython.display import Image
Image('./images/image1.PNG')
```

```py
data1 = [1.1, 2, 3, 4]
data1
```
```py
arr1 = np.array(data1)
arr1
```
```py
type(arr1)
```
data2 = [[1, 2, 3], [1, 2, 3]]
data2
```py
arr2 = np.array(data2)
arr2
```
```py
type(arr2)
```
```py
np.zeros(10)
```
```py
np.ones(10)
```
```py
np.empty(10)
```
```py
np.empty((2, 3))
```
```py
np.zeros((2, 3))
```
```py
np.arange(10)
```
```py
arr1, arr2
```
```py
# type 확인
type(arr1), type(arr2)
```
```py
# shape(형상) 확인
arr1.shape, arr2.shape
```
```py
# ndim(차원) 확인
arr1.ndim, arr2.ndim
```
```py
# 개별 원소들의 타입
arr1.dtype
```
```py
arr2.dtype
```

### 1.2 ndarray의 dtype
```py
Image('./images/image2.PNG')

arr1 = np.array([1, 2, 3], dtype=np.float64)
arr1.dtype
```
```py
int_arr = arr1.astype(np.int64)
int_arr.dtype
```
### 1.3 Numpy 배열의 산술 연산
```py
arr = np.array([[1., 2., 3.], [4., 5., 6.]])
arr
```
```py
arr.dtype
```
```py
arr * arr
```
```py
arr - arr
```
```py
arr * 2 # broadcasting 기능의 예
```
```py
arr2 = np.array([[2., 3., 4.], [5., 6., 7.]])
arr2
```
```py
arr < arr2
```

### 1.4 색인과 슬라이싱
```py
arr = np.arange(10) + 10
arr
```
```py
# 1차원 데이터 색인
arr[5]
```
```py
# 1차원 데이터 슬라이싱
arr[5:8] # 5번째에서 7번째까지만 가져오고, 8번째는 포함되지 않음
```
```py
arr[5:8] = 100
arr
```
```py
arr = np.arange(10) + 10
arr
```
```py
brr = arr[5:8]
brr
```
```py
arr[5:8] = 100
```
```py
arr
```
```py
brr # brr가 arr[5:8] 와 같은 메모리를 공유하고 있어서 arr[5:8] 의 수정사항이 brr에도 반영
```
```py
arr3 = np.array([1, 2, 3])
arr4 = np.array([10, 11, 12])
```
```py
arr4 - arr3
```
```py
arr2d = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
arr2d
```
### add2d를 만드는 또다른 방법
```py
arr = np.arange(1, 10)    # range() 함수와 똑같다
arr.reshape(3, 3)
```
```py
arr2d.ndim, arr2d.shape
```
### 2차원 데이터의 색인
```py
arr2d[2]
```
```py
arr2d[2][2]
```
```py
arr2d[2, 2]
```
```py
Image('./images/image3.PNG')
```

### 2차원 데이터의 슬라이싱
```py
arr2d[0:2] # arr2d의 0번째부터 1번째까지 슬라이싱(arr2d[0], arr2d[1])
```
```py
arr2d[1:3, 1:2]
```
```py
arr2d[0:3, 1:3]   # arr2d[행슬라이싱, 열슬라이싱]
```
```py
arr2d[:3, 1:]
```
```py
arr2d[2] # 2차원 데이터를 색인하면 1차원 데이터
```
```py
arr2d[:2] # 2차원 데이터를 슬라이싱하면 2차원 데이터
```
### 색인과 슬라이싱을 동시에
```py
arr2d[:2, 1]   # 1차원 데이터로 출력
```
```py
arr2d[:2, 1:2] # 슬라이싱만 사용하면 그대로 2차원 데이터
```
### 색인에서는 아래 문법이 동일
```py
arr2d[1][1]
```
```py
arr2d[1, 1]
```
### 슬라이싱에서는 아래 문법이 동일하지 않음
```py
arr2d[1:3][0:2]           # 순차적으로 모두 실행 (or gate)
```
```py
arr2d[1:3, 0:2]           # 동시에 실행 (and gate)
```
```py
Image('./images/image4.png')
```
### Workshop
색인과 슬라이싱
```py
import matplotlib.pyplot as plt

img = plt.imread('./images/psj.png')

print(type(img), img.ndim, img.shape)

plt.imshow(img)
```
```py
img.shape # 원본 이미지의 형상
```
```py
img[0].shape # 3차원 원본 이미지를 색인하면 2차원 데이터
```
```py
img[0, 0].shape # 3차원 원본 이미지를 두 번 색인하면 1차원 데이터
```
```py
img[0, 0] # 좌상단 픽셀 값(R, G, B, alpha)
```
```py
img[0, 364] # 우상단의 픽셀값 (R, G, B, alpha)
```
```py
img[20, 20] = np.array([1, 0, 0, 1])  # 좌상단의 한 픽셀값을 빨간색(1, 0, 0, 1)으로 overwrite
# img[20, 20] = [1, 0, 0, 1]    option 2
```
```py
img[21, 21] = np.array([0, 1, 0, 1])  # 좌상단의 한 픽셀값을 빨간색(1, 0, 0, 1)으로 overwrite
```
```py
img[22, 22] = np.array([0, 0, 1, 1])  # 좌상단의 한 픽셀값을 빨간색(1, 0, 0, 1)으로 overwrite
```
```py
plt.imshow(img)
```
```py
img[20:25, 20:25] = [1, 0, 0, 1] # 좌상단의 5 X 5 픽셀 영역을 빨간색(1, 0, 0, 1)으로 overwrite
```
```py
img[245:250, 245:250] = [1, 1, 0, 1]
```
```py
img[100:105, 100:105] = [1, 0, 1, 1]
```
```py
plt.imshow(img)
```
### broadcasting 과정 
```py
red = np.array([1, 0, 0, 1])
img[0:5, 0:5].shape, red.shape
```
```py
arr3 = np.arange(12).reshape(6, 2)
arr4 = np.array([1, 2])
```
```py
arr3
```
```py
arr4
```
```py
arr3 + arr4  # (6, 2) + (2,) braodcasting이 가능
```
```py
arr5 = np.arange(6)
```
```py
arr5
```
```py
arr3 + arr5 # (6, 2) + (2,) broadcasting이 불가
```
```py
arr3 + 3  # broadcasting이 가능
```
```py
arr6 = np.arange(72).reshape((6, 4, 3))
arr7 = np.arange(12).reshape(4, 3)
```
```py
arr6 + arr7 # broadcasting 가능
```
**10픽셀 굵기로 액자 만들기(색상은 자유)**
```py
img = plt.imread('./images/psj.png')
```
```py
print(type(img), img.ndim, img.shape)
```
```py
plt.imshow(img)
```
```py
img[0:10, :] = [0.5, 0.3, 0.2, 1]  # 위쪽

img[:, 0:10] = [0.1, 0.7, 0.4, 1]  # 왼쪽

img[322:, :] = [0.3, 0.7, 0.1, 1]  # 아래

img[:, 354:] = [0.9, 0.3, 0.6, 1]  # 위쪽

plt.imshow(img)
```
### 1.5 불리안 색인
```py
arr1 = np.arange(10)
arr1
```
```py
arr1 < 5
```
```py
arr1[[ True,  True,  True,  True,  True, False, False, False, False,
       False]]
```
```py
data = np.arange(28).reshape((7, 4))
data
```
```py
data[[True, True, False, False, True, True, True]]
```
```py
names = np.array(['Bob', 'Joe', 'Will', 'Bob', 'Will', 'Joe', 'Joe'])
```
```py
names == 'Bob'    # 1, 4번째만 True인 것을 알 수 있음
```
```py
names == 'Joe'
```
```py
data[names == 'Bob']      # data에서 1, 4번째 인덱스의 값을 가져옴
```
```py
data[names == 'Bob', 2:3] # 행은 불리안 색인, 열은 숫자로 슬라이싱(차원이 그대로 유지)
```
```py
data[names == 'Bob', 2]  # 행은 불리안 색인, 열은 숫자로 색인(색인이라 차원이 1차원으로 줄었음)
```
```py
data
```
```py
data < 10
```
```py
data[data < 10]     # 데이터가 True인 인덱스의 값만 반환
```
### 1.6 팬시 색인(정수 색인)
```py
data
```
```py
data[[0, 5]]
```
```py
data[[-7, -2]]
```
### 2. 유니버설 함수 : 배열의 각 원소를 빠르게 처리
```py
arr = np.arange(10)
arr
```
```py
np.sqrt(arr)
```
```py
np.exp(arr)
```
```py
arr1 = np.arange(10)
arr2 = np.arange(10) + 2
```
```py
np.maximum(arr1, arr2)
```
### Workshop (거리 계산 - numpy 사용)

**거리계산**
- 리스트를 이용하여 점 사이의 거리를 계산 해 보자.
- 직교 좌표 위에서 A는 (1, 1), B는 (3, 2), C는 (5,7)일 때 X(2, 3)와  A/B/C와의 거리를 각각 구하여라.
- 위 코드블럭을 이용하여 distMeasure 함수를 정의하라.

**파이썬 이용한 버전**
```py
import math

def disMeasure(x, y):
    dis = math.sqrt(((x - 2) ** 2) + ((y - 3) ** 2))
    return dis

disMeasure(1, 1)

disMeasure(3, 2)

disMeasure(5, 7)
```
```py
points = [(1, 1), (3, 2), (5, 7)]
X = (2, 3)
```
```py
from math import sqrt
def distMeasure(pointx, X):
    result = []
    for point in points:
        dist = sqrt((point[0] - X[0]) ** 2 + (point[1] - X[1]) ** 2)
        result.append(dist)
    return result

distMeasure(points, X)
```

**넘파이 이용한 버전**
```py
def disMeasure_np(x, y):
    dis = np.sqrt(((x - 2) ** 2) + ((y - 3) ** 2))
    return dis

a = [(1, 1), (3, 2), (5, 7)]
```
```py
np.sqrt(a) + [2, 3]
```
```py
disMeasure_np(1, 1)

disMeasure_np(3, 2)

disMeasure_np(5, 7)

points = [(1, 1), (3, 2), (5, 7)]
X = (2, 3)
```
```py
points_arr = np.array(points)
X_arr = np.array(X)
```
```py
type(points), type(X)
```
```py
type(points_arr), type(X_arr), points_arr.shape, X_arr.shape
```

### 1) 모든 포인트(A, B, C)에 대해서 X축으로의 거리 Y축으로의 거리를 한 번에 구함
```py
(points_arr - X_arr)
```
### 2) 1에서 구한 모든 원소에 대해 제곱
```py
(points_arr - X_arr) ** 2
```
### 3) 2에서 구해진 값을 1번 축으로 더함
```py
np.sum((points_arr - X_arr) ** 2, axis = 1)  # 축의 개념 / axis 써도 되고 안 써도 됨
```
### 4) 3에서 구해진 값에 제곱근 씌우기
```py
np.sqrt(np.sum((points_arr - X_arr) ** 2, axis = 1))
```
## 오늘 배운 numpy 정리

- 임포트
```py
import numpy as np
```
- 객체 생성
```py
a1 = np.array([10, 20, 30])
type(a1)
```
```py
a2 = np.array([[10, 20, 30], [40, 50, 60]])
type(a2)
```
- 모양
```py
a1.shape
```
```py
a2.shape
```
- 개별 원소의 자료형 확인
```py
a1.dtype
```
```py
a2.dtype
```
- 색인(인덱스 번호로 한 지점을 조회)
```py
a1[0]
```
```py
a2[0][0] # a2[0, 0]과 동일
```
- 슬라이싱(연속된 구간의 정보를 조회)
```py
a1[1:]
```
```py
a2[0:1, 1:]  # 2차원 배열이 유지된 상태
```
```py
a2[0, 1:]   # 1차원 배열로 차원 감소(색인을 사용해서)
```
- 불리안 색인
```py
a1
```
```py
a1 < 30
```
```py
a1[a1 < 30]
```
```py
a2
```
```py
(a2 < 30) | (a2 > 50)
```
```py
a2[(a2 < 30) | (a2 > 50)]
```
- 팬시 색인(불연속적으로 가져오거나, 원하는 순서로 색인)
```py
a1
```
```py
a1[[2, 0]]
```
- broadcasting
```py
a1.shape, a2.shape
```
```py
a2 + 1
```
```py
a1 + a2
```
```py
a0 = np.array([10, 20])
a0.shape, a2.shape
```
```py
a0 + a2   # broadcasting 할 수 없는 형상 # 큰 차원의 배열의 말단과 개수가 맞아야 하는데 이 배열들은 서로 같지 않다
```
- 배열의 축
```py
a1
```
```py
np.sum(a1) # 수학/통계 함수
```
```py
np.sum(a2)
```
```py
a2
```
```py
np.sum(a2, axis = 0)  # 열 축을 따라서
```
```py
np.sum(a2, axis = 1)  # 행 축을 따라서
```
```py
import numpy as np
```
## 3. 그 외 기능들

### 3.1 배열 전치
```py
arr = np.arange(15).reshape((3, 5))  # 3행 5열의 행렬이 준비
arr
```
```py
arr.T     # Transpose 전치행렬
```
```py
arr * arr # 개별 원소의 곱셈
```
### 행렬의 곱셈
```py
# arr @ arr 연산은 가능하지 않음 (@은 행렬의 곱셈)
(3, 5) @ (3, 5)
```
#### arr @ arr.T 연산은 가능
#### (3, 5) @ (5, 3) = (3, 3)
```py
arr @ arr.T
```
```py
np.dot(arr, arr.T)
```
### 3.2 배열 연산과 조건절 표현하기
```py
x_list = [1, 2, 3, 4]
y_list = [5, 6, 7, 8]
cond_list = [True, True, False, False]
```
```py
result = []
for x, y, c in zip(x_list, y_list, cond_list):   # 4번 순회
    if c:
        result.append(x)
    else:
        result.append(y)
result
```
```py
x_arr = np.array([1, 2, 3, 4])
y_arr = np.array([5, 6, 7, 8])
cond_list = np.array([True, True, False, False])
```
### np.where(조건, 조건이 참일 때 취할 깂, 조건이 거짓일 때 취할 값)
```py
result = np.where(cond_list, x_list, y_list)
result
```
```py
arr = np.arange(16).reshape((4, 4))
arr
```
```py
arr > 10
```
```py
cond = arr > 10
np.where(cond, 1, -1)
```
```py
arr < 10
```
```py
cond = arr < 10
result = np.where(cond, 1, arr)
result
```
### 3.3 수학 통계 메서드
```py
from IPython.display import Image
Image('./images/image5.PNG')
```
```py
arr = np.arange(20).reshape((5, 4))
arr
```
```py
np.sum(arr)
```
```py
arr.sum()
```
```py
np.sum(arr, axis = 0)   # "0번축(열축)을 따라서" 합 구하기
```
```py
arr.sum(0)
```
```py
np.sum(arr, axis = 1)   # "1번축(행축)을 따라서" 합 구하기
```
```py
np.mean(arr, 0)  # arr.mean(0)
```
```py
arr
```
```py
arr.min()
```
```py
arr.min(0)
```
```py
arr.min(1)
```
```py
arr.max()
```
```py
arr
```
```py
arr.cumsum(0)
```
```py
arr.cumsum(1)
```
```py
np.cumprod(arr, 1)
```
```py
np.cumprod(arr, 0)
```
### 3.4 불리언 배열 메서드
```py
bool_arr = np.array([True, False, True])
bool_arr
```
```py
bool_arr.all()     # 모두 True여야 True 반환
```
```py
bool_arr.any()     # 하나라도 True면 True 반환
```
```py
arr = np.arange(16).reshape((2, 8))
arr
```
```py
bool_arr2 = arr < 8
bool_arr2
```
```py
bool_arr2.all(1)
```
```py
bool_arr2.any(0)
```
### 3.5 정렬
```py
arr = np.random.randn(3, 4)  # np에서 제공하는 표준정규분포를 따르는 무작위수를 지정한 사이즈로 만들어줌
arr
```
```py
np.sort(arr, 1)
```
```py
np.sort(arr, 0)
```
```py
arr.sort(1)
arr
```
```py
arr.sort(0)
arr
```
### 3.6 집합 관련 함수
```py
fruits_list = ["strawberry", "strawberry", "pear", "apple"]  
fruits_list
```
```py
set(fruits_list)     # 파이썬의 집합
```
```py
fruits_array = np.array(["strawberry", "strawberry", "pear", "apple"])
fruits_array
```
```py
np.unique(fruits_array)
```
### 3.7 난수 생성
```py
Image('./images/image6.png')
```
- 정규 분포에서 표본을 추출
```py
samples = np.random.normal(size = 1000, loc = 10, scale = 1)
samples
```
```py
samples.min()
```
```py
samples.max()
```
```py
samples.mean()
```
```py
samples.std()   # 표준편차 구하기
```
```py
import matplotlib.pyplot as plt
```
```py
plt.hist(samples, 100)
```
- 표준 정규분포에서 표본을 추출
```py
samples = np.random.randn(1000)
samples
```
```py
samples.mean(), samples.std()   # 평균 0, 표준편차 1
```
- 최대, 최소 범위에서 난수 생성

### 주사위 던지기 
```py
for i in range(20):
    draw = np.random.randint(1, 7)
    print(draw, end = ' ')
```
### 반복문 없이 주사위 던지기 50회 simulation
```py
np.random.randint(1, 7, 50)

arr = np.arange(1, 17)
p = np.random.permutation(arr)
p.reshape(4, 4)   # 4팀을 무작위로
```
## Workshop 

1~45개의 번호 중 무작위로 6개씩 생성되는 번호 세트를 총 10개 출력하기
```py
arr = np.arange(1, 46)
    
for i in range(10):
    p = np.random.permutation(arr)
    a = p[:6]
    print(a)
```
## Workshop

계단 오르 내리기

- 동전을 던졌을 때 앞이 나오면 계단 1칸 올라가기
- 동전을 던졌을 때 뒤가 나오면 계단 1칸 내려가기
- 현재 위치 position
- 1000번 동전을 던졌을 때의 위치의 히스토리: walk 리스트
```py
import random

position = 0 # 계단 1칸 오르면 +1, 1칸 내려가면 -1
steps = 1000

walk = [position] # [0, 1, 0, -1, -2, -3, -2, -1, 0, -1 , 0, 1]

w = 0

for i in range(steps):
    a = random.randint(0, 1)
    if a == 1:
        w += 1
        walk.append(w)
    elif a == 0:
        w -= 1
        walk.append(w)
walk
```
```py
walk[-1]
```
```py
plt.plot(walk)
```
- 위에서 사용한 파이썬 코드를 사용하지 않고(for문을 사용하지 않고) numpy로 구현
```
np.random.randint(): 동전의 앞뒤 결정
np.where(): 동전의 앞뒤 조건에 따른 step 결정
np.cumsum(): 현재 위치의 히스토리
```
```py
r = np.random.randint(0, 2, 1000)

arr = np.where(r, +1, -1)
c = np.cumsum(arr)
```
```py
plt.plot(c)
```
```py
arr = np.array([1, 100, 20, 30])
```
```py
np.min(arr), np.max(arr)
```
```py
np.argmin(arr), np.argmax(arr)    # 위치를 출력
```
### 처음 위치에서 10계단 이상 올라가는데 걸린 횟수
```py
bool_arr = c >= 10
np.argmax(bool_arr)  # False는 0, True는 1로 간주
                     # argmax() 최댓값(1)이 최초로 등장한 index를 알려줌
                     # 처음 위치에서 10계단 이상 올라가는데 53번의 동전을 던진 것을 확인할 수 있음
```
```py
bool_arr.argmax()
```
