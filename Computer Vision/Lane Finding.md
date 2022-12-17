# 차선인식

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
```

## 1. Lane Finding (white lane)

```python
image = mpimg.imread('./data/test.jpg')
plt.imshow(image)
```

```
<matplotlib.image.AxesImage at 0x283587c9af0>
```

![image](https://user-images.githubusercontent.com/84713532/208243861-f07207e5-0f06-4810-ac59-b68ec74580dd.png)


## Color Selection

Color Picker Tool로 해당 이미지 색상의 RGB 코드값 얻어오기
https://annystudio.com/software/colorpicker/#download

```python
color_select = np.copy(image)

red_threshold = 237
green_threshold = 237
blue_threshold = 237


color_threshold = ((image[:, :, 0] < red_threshold) |
                   (image[:, :, 1] < green_threshold) |
                   (image[:, :, 2] < blue_threshold))

color_select[color_threshold] = [0, 0, 0]
plt.imshow(color_select)
```

```
<matplotlib.image.AxesImage at 0x28358ae43a0>
```

![image](https://user-images.githubusercontent.com/84713532/208243873-8d419636-8068-43ef-b2be-6d214dce9b24.png)


## Region Selection

```python
region_select = np.copy(image)

# todo
left_bottom = [0, 539]
right_bottom = [900, 539]
apex = [475, 320]

pts = np.array([left_bottom, right_bottom, apex])
cv2.fillPoly(region_select, [pts], color=[0, 0, 255])
plt.imshow(region_select)
```

```
<matplotlib.image.AxesImage at 0x28359295b50>
```

![image](https://user-images.githubusercontent.com/84713532/208243883-63e267fa-8fd2-4beb-966b-bf1c898e463d.png)


## Color and Region Selection

```python
image.shape
```

```
(540, 960, 3)
```

```python
color_select = np.copy(image)

red_threshold = 237
green_threshold = 237
blue_threshold = 237


color_threshold = ((image[:, :, 0] < red_threshold) |
                   (image[:, :, 1] < green_threshold) |
                   (image[:, :, 2] < blue_threshold))

color_select[color_threshold] = [0, 0, 0]

# 2. Region Selection
region_select = np.copy(image)

left_button = [0, 540]
right_button = [960, 540]
apex = [475, 330]

pts = np.array([left_button, right_button, apex])
cv2.fillPoly(region_select, [pts], color = [0, 0, 255])

region_threshold = ((region_select[:, :, 0] == 0) &    # R channel
                    (region_select[:, :, 1] == 0) &    # G channel
                    (region_select[:, :, 2] == 255))   # B channel


# 3 Color Selection + Region Selection
# color_threshold: 차선(흰색)이 아닌 부분 True 설정
# region_threshold: 관심영역(region of interes, roi)에만 True 설정
lane_select = np.copy(image)
lane_select[~color_threshold > 0] = [255, 0, 0]

plt.imshow(lane_select)
```

```
<matplotlib.image.AxesImage at 0x283598f8760>
```

![image](https://user-images.githubusercontent.com/84713532/208243901-87da0120-1628-4070-bfdc-529d32552a5c.png)


```python
~color_threshold
```

```
array([[False, False, False, ..., False, False, False],
       [False, False, False, ..., False, False, False],
       [False, False, False, ..., False, False, False],
       ...,
       [False, False, False, ..., False, False, False],
       [False, False, False, ..., False, False, False],
       [False, False, False, ..., False, False, False]])
```

## 2. Lane Finding (white and yellow)

```python
image = mpimg.imread('./data/exit-ramp.jpg')
plt.imshow(image)
```

```
<matplotlib.image.AxesImage at 0x283592efdf0>
```

![image](https://user-images.githubusercontent.com/84713532/208243910-06e8e71f-ea53-4b81-99c4-e355eade5f42.png)


### Step 1: gray scale 변환

```python
gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
plt.imshow(gray, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x28358bb82b0>
```

![image](https://user-images.githubusercontent.com/84713532/208243924-4a16a8c8-08b5-4ff2-a5bb-0cb19b2a7c7d.png)


### Step 2: Gaussian blurring (option)

```python
kernel_size = 5
blur_gray = cv2.GaussianBlur(gray, (kernel_size, kernel_size), 0)
plt.imshow(blur_gray, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x28358c0fe80>
```

![image](https://user-images.githubusercontent.com/84713532/208243946-abf8cf52-92d2-4a32-989a-a207bf23732c.png)


## ROI Selection

### Step 3: edge detect

```python
low_threshold = 50
high_threshold = 150  # low:high의 비율 1:2 or 1:3
edges = cv2.Canny(blur_gray, low_threshold, high_threshold)
plt.imshow(edges, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x2835acd26a0>
```

![image](https://user-images.githubusercontent.com/84713532/208243952-9c57f3b1-9f38-4bbe-9bae-24d74e2ac748.png)


### Step 4: roi selection (region of interest)

```python
edges.shape
```

```
(540, 960)
```

```python
pts = np.array([[60, 539], [900, 539], [490, 280], [460, 280]])
mask = np.zeros(edges.shape, edges.dtype)
cv2.fillPoly(mask, [pts], color=[255, 255, 255])
plt.imshow(mask, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x2835d522580>
```

![image](https://user-images.githubusercontent.com/84713532/208243960-a8a9cef8-cffb-428d-8d42-ae4a2914a6ef.png)


```python
height = edges.shape[0]
width = edges.shape[1]
```

```python
# 관심 영역의 mask 준비

pts = np.array([[0, height - 1], [1, 539], [490, 280], [width - 1, height - 1]])
mask = np.zeros(edges.shape, edges.dtype)
cv2.fillPoly(mask, [pts], color=[255, 255, 255])
plt.imshow(mask, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x2835d4bdc10>
```

![image](https://user-images.githubusercontent.com/84713532/208243975-7ee93ff1-de3e-4796-8190-61c06becde31.png)


```python
# 위에서 준비한 mask와 edges를 bitwise_and
masked_edges = cv2.bitwise_and(edges, mask)
plt.imshow(masked_edges, cmap='gray')
```

```
<matplotlib.image.AxesImage at 0x2835ad9bf70>
```

![image](https://user-images.githubusercontent.com/84713532/208243985-6e1c04a0-f813-4edd-bfa9-d43331ac81aa.png)


### Step 5: line detect (with hough transform)

```python
rho = 1
theta = np.pi / 180
threshold = 35
minLineLength = 40
maxLineGap = 50

lines = cv2.HoughLinesP(masked_edges, rho, theta, threshold,
                        minLineLength=minLineLength, maxLineGap=maxLineGap)

# (참고) 1차원 데이터를 3차원으로 확장하는 방법
# dst = cv2.cvtColor(masked_edges, cv2.COLOR_GRAY2BGR)  # 직선을 그릴 도화지 (3 채널 도화지)  option 1
# dst = cv2.merge([masked_edges, masked_edges, masked_edges]) option 2
# dst = np.dstack((masked_edges, masked_edges, masked_edges)) option 3
dst = np.dstack((masked_edges, masked_edges, masked_edges))

if lines is not None:
    for i in range(len(lines)):
        line = lines[i][0]
        pt1 = line[0], line[1]
        pt2 = line[2], line[3]
        cv2.line(dst, pt1, pt2, (255, 0, 0), 2, cv2.LINE_AA)

plt.imshow(dst)
```

```
<matplotlib.image.AxesImage at 0x2836125bca0>
```

![image](https://user-images.githubusercontent.com/84713532/208243992-41ca6174-9be3-46f3-9996-fd8ee2e9e69e.png)


## Pipeline (Step 1 ~ Step 5)

- Canny Detection -> ROI Selection -> Hough Transform

```python
## Step 1: gray scale 변환

gray = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)



## Step 2: Gaussian blurring (option)

kernel_size = 5
blur_gray = cv2.GaussianBlur(gray, (kernel_size, kernel_size), 0)



# ROI Selection
## Step 3: edge detect

low_threshold = 50
high_threshold = 150  # low:high의 비율 1:2 or 1:3
edges = cv2.Canny(blur_gray, low_threshold, high_threshold)



## Step 4: roi selection (region of interest)

pts = np.array([[60, 539], [900, 539], [490, 280], [460, 280]])
mask = np.zeros(edges.shape, edges.dtype)
cv2.fillPoly(mask, [pts], color=[255, 255, 255])
plt.imshow(mask, cmap='gray')

# 위에서 준비한 mask와 edges를 bitwise_and
masked_edges = cv2.bitwise_and(edges, mask)



## Step 5: line detect (with hough transform)

rho = 1
theta = np.pi / 180
threshold = 35
minLineLength = 40
maxLineGap = 50

lines = cv2.HoughLinesP(masked_edges, rho, theta, threshold,
                        minLineLength=minLineLength, maxLineGap=maxLineGap)

# (참고) 1차원 데이터를 3차원으로 확장하는 방법
# dst = cv2.cvtColor(masked_edges, cv2.COLOR_GRAY2BGR)  # 직선을 그릴 도화지 (3 채널 도화지)  option 1
# dst = cv2.merge([masked_edges, masked_edges, masked_edges]) option 2
# dst = np.dstack((masked_edges, masked_edges, masked_edges)) option 3
dst = np.dstack((masked_edges, masked_edges, masked_edges))

if lines is not None:
    for i in range(len(lines)):
        line = lines[i][0]
        pt1 = line[0], line[1]
        pt2 = line[2], line[3]
        cv2.line(dst, pt1, pt2, (255, 0, 0), 2, cv2.LINE_AA)

# result = cv2.add(image, dst)
result = cv2.addWeighted(image, 1, dst, 0.8, 0)   # 비중 조절 가능

plt.imshow(result)
```

```
<matplotlib.image.AxesImage at 0x2836128e580>
```
![image](https://user-images.githubusercontent.com/84713532/208244000-a78499b8-f6b7-49ec-9cde-ce0158d87850.png)
