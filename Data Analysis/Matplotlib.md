# matplotlib API 개요

- 정보 시각화는 데이터 분석에서 무척 중요
- 시각화는 특잇값을 찾아내거나, 데이터 변형이 필요한지 알아보거나, 모델에 대한 아이디어를 찾기 위한 과정의 일부
- 파이썬 시각화 도구로 matplotlib 활용

- 공식 사이트
https://matplotlib.org/
```py
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
```
```py
plt.plot([1, 2, 3], [4, 5, 6]) # 각각의 리스트가 x축, y축으로 전달되어서 선그래프
plt.show()  # 주피터 노트북에서는 plt.show()를 안해줘도 그림이 표시가 되지만, .py같은 스크립트 작성시에는 필요
```
### Figure와 Axes 
```py
from IPython.display import Image
Image('./images/figure_axes.png')
```
**Figure**
- 그림을 그리기 위한 도화지의 역할, 그림판의 크기 등을 조절함 

**Axes**
- 실제 그림을 그리는 메서드들과 x축, y축, title 등의 속성을 가짐

```
plt.plot([1, 2, 3], [4, 5, 6]) # 기본 설정값의 Figure가 만들어진 후, 내부적으로 Axses.plot() 호출
plt.title("Hello Plot") # Axses.set_title() 호출
plt.show() # Figure.show 호출
```
```py
plt.figure(figsize = (10, 4)) # 가로가 10, 세로가 4인 Figure 객체를 생성해서 반환
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Hello plot")
plt.show()
```
```py
plt.figure(facecolor = 'Red', figsize=(10, 4)) # 가로가 10, 세로가 4인 Figure 객체를 생성해서 반환
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Hello plot")
plt.show()
```
```py
# Figure를 가져옴
plt.figure()
```
```py
# Axes를 가져옴
plt.axes()
```
```py
# Figure와 Axes를 함께 가져옴 (기본적으로 한개의 Axes를 설정)
fig, axes = plt.subplots()
print(type(fig), type(axes))
```
```py
# Figure와 Axes를 함께 가져옴 (여러개의 Axes를 가지는 figure 설정)
fig, axes = plt.subplots(nrows = 1, ncols = 2, figsize = (10, 4))
print(type(fig), type(axes))
```
### plot 함수 안에 올 수 있는 데이터
```py
plt.plot([1, 2, 3], [4, 5, 6])
```
```py
# np.array
plt.plot(np.array([1, 2, 3]), np.array([4, 5, 6]))
```
```py
# Series
plt.plot(pd.Series([1, 2, 3], pd.Series([4, 5, 6])))
```
### 색상, 마커, 라인스타일 등 변경
```py
Image('./images/plot.png')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'green')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], 'g')  # 색상 변경(축약형)
```
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'g', marker = 'o')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], 'co-')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'g', marker = 'o', linestyle = 'dashed')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], 'co--')
```
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'magenta', marker = 'o', linestyle = 'dashed', linewidth = 3, markersize = 10)
```
### x축, y축에 축명을 텍스트로 할당. xlabel, ylabel 적용
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'magenta', marker = 'o', linestyle = 'dashed', linewidth = 3, markersize = 10)
plt.xlabel('x axis')
plt.ylabel('y axis')
```
### x축, y축 틱값 표기
```py
plt.plot([1, 2, 3], [4, 5, 6], color = 'magenta', marker = 'o', linestyle = 'dashed', linewidth = 3, markersize = 10)
plt.xlabel('x axis')
plt.ylabel('y axis')
plt.xticks([1, 2, 3]) # x축 눈금
plt.yticks([4, 5, 6]) # y축 눈금
```
### x축, y축 틱값을 표현을 회전해서 보여줌
```py
plt.plot(['hello', 'python', 'world'], [4, 5, 6], color = 'magenta', marker = 'o', linestyle = 'dashed', linewidth = 3, markersize = 10)
plt.xlabel('x axis')
plt.ylabel('y axis')

plt.xticks(rotation = 30) # x축 눈금
plt.yticks([4, 5, 6]) # y축 눈금
```
