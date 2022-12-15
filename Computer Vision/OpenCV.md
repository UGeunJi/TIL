# 기초 사용법

opencv tutorial : https://docs.opencv.org/4.6.0/d6/d00/tutorial_py_root.html

```python
import cv2
```

```python
cv2.__version__
```

```
'4.6.0'
```

## Hello World

```python
img = cv2.imread('./data/lenna.bmp')

print(type(img), img.shape)

cv2.namedWindow('image')   # 생략 가능
cv2.imshow('image', img)

cv2.waitKey()
cv2.destroyAllWindows()
```

```
<class 'numpy.ndarray'> (512, 512, 3)
```

```python
img.min(), img.max()
```

```
(3, 255)
```

```python
img[0][0]
```

```
array([125, 137, 226], dtype=uint8)
```

## 영상 파일 읽고 화면에 표시하기

```python
# Color Mode로 이미지 읽기
imgColor = cv2.imread('./data/lenna.bmp', cv2.IMREAD_COLOR)

# GrayScale Mode로 이미지 읽기
imgGray = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

# type, shape 출력
print(type(imgColor), type(imgGray), imgColor.shape, imgGray.shape)

# 윈도우에 보여주기
cv2.imshow('image1', imgColor)
cv2.imshow('image2', imgGray)

# 창닫기
cv2.waitKey()
cv2.destroyAllWindows()
```

```
<class 'numpy.ndarray'> <class 'numpy.ndarray'> (512, 512, 3) (512, 512)
```

## 영상 파일 읽고 저장하기

```python
# Color Mode로 이미지 읽기
imgColor = cv2.imread('./data/lena.jpg', cv2.IMREAD_COLOR)
print(type(imgColor), imgColor.shape)

cv2.imwrite('./out/lena.bmp', imgColor)
cv2.imwrite('./out/lena.png', imgColor)

cv2.imwrite('./out/lena2.png', imgColor, [cv2.IMWRITE_PNG_COMPRESSION, 5]) # 숫자가 클수록 압축이 많이 됨(0 ~ 9)
cv2.imwrite('./out/lena2.jpg', imgColor, [cv2.IMWRITE_JPEG_QUALITY, 90]) # 0 ~ 100

cv2.imshow('img color', imgColor)
cv2.waitKey()
cv2.destroyAllWindows()
```

```
<class 'numpy.ndarray'> (512, 512, 3)
```

## matplotlib으로 컬러 영상 표시

```python
import matplotlib.pyplot as plt
```

```python
# matplotlib으로 이미지 읽고 보여주기
img_m = plt.imread('./data/lena.jpg')
plt.imshow(img_m)
```

```
<matplotlib.image.AxesImage at 0x24f6cf72e80>
```

![image](https://user-images.githubusercontent.com/84713532/207256214-aca7746f-ad17-4327-b28d-ec158404caae.png)


```python
img_c = cv2.imread('./data/lena.jpg')
plt.imshow(img_c)
```

```
<matplotlib.image.AxesImage at 0x24f6d6c6640>
```

![image](https://user-images.githubusercontent.com/84713532/207256245-733c532c-a690-47a2-9168-f23781998547.png)


```python
img_m[0][0], img_c[0][0]  # cv2가 이미지를 읽는 순서는 B->G->R, matplotlib은 R->G->B
```

```
(array([225, 138, 128], dtype=uint8), array([128, 138, 225], dtype=uint8))
```

```python
img_c = cv2.imread('./data/lena.jpg')
cv2.imshow('img color', img_c)
cv2.waitKey()
cv2.destroyAllWindows()
```

- (1) cvtColor 함수를 컬러 채널을 변경후 표시

```python
img_bgr = cv2.imread('./data/lena.jpg')   # img_bgr에는 BGR의 순서로 데이터가 준비되어 있음
# 현재 채널 공간(channel space)이 BGR인데 RGB로 바꿈
img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
```

```
<matplotlib.image.AxesImage at 0x24f6e706820>
```

![image](https://user-images.githubusercontent.com/84713532/207256305-d591c2ce-4cd3-492a-bbcd-7570e7c1b584.png)


- (2) numpy ndarray의 색인 문법으로 컬러 채널 순서를 변경

```python
img_bgr = cv2.imread('./data/lena.jpg')   # img_bgr에는 BGR의 순서로 데이터가 준비되어 있음
# 현재 채널 공간(channel space)이 BGR인데 RGB로 바꿈
# option 1
img_rgb = img_bgr.copy()
img_rgb[:, :, [0, 2]] = img_bgr[:, :, [2, 0]]

img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
```

```
<matplotlib.image.AxesImage at 0x24f6e769760>
```

![image](https://user-images.githubusercontent.com/84713532/207256337-ca7e2f38-86a9-4425-8d09-03285e99261d.png)


```python
img_bgr = cv2.imread('./data/lena.jpg')   # img_bgr에는 BGR의 순서로 데이터가 준비되어 있음
# 현재 채널 공간(channel space)이 BGR인데 RGB로 바꿈
# option 2
img_rgb = img_bgr.copy()
img_rgb[:, :, 0] = img_bgr[:, :, 2]
img_rgb[:, :, 2] = img_bgr[:, :, 0]

img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
```

```
<matplotlib.image.AxesImage at 0x24f6e7d04c0>
```

![image](https://user-images.githubusercontent.com/84713532/207256375-f7deeb55-06c9-4ac1-bf28-dea2508a3070.png)


```python
img_bgr = cv2.imread('./data/lena.jpg')   # img_bgr에는 BGR의 순서로 데이터가 준비되어 있음
# 현재 채널 공간(channel space)이 BGR인데 RGB로 바꿈
# option 3
img_rgb = img_bgr.copy()
img_rgb = img_bgr[:, :, -1::-1]

img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
```

```
<matplotlib.image.AxesImage at 0x24f6e834490>
```

![image](https://user-images.githubusercontent.com/84713532/207256409-969a97d7-0b7b-4258-bac4-9137824dddf1.png)


# 동영상 파일 다루기

```
객체 = 비디오 객체 생성

while True:
    배열 = 객체.read() # 배열 한장이 이미지 한장 (shape: w, h, c)
    배열 보여주기 (재생)
    배열 저장하기 (녹화)

    키 기다리다 조건에 맞으면
        break;
창닫기
```

```python
cap = cv2.VideoCapture(device)  # 카메라 디바이스
cap = cv2.VideoCapture(filepath) # 동영상 파일
cap = cv2.VideoCapture(url)     # 스트리밍 주소
```

## 카메라 입력

```python
import sys
```

```python
cap = cv2.VideoCapture(0)   # 0: main camera

if not cap.isOpened():
    print('Camera open failed!')
    sys.exit()

while True:
    ret, frame = cap.read()  # frame은 이미지 한장

    if not ret:
        print('frame read error')
        break

    cv2.imshow('camera', frame)

    key = cv2.waitKey(10)  # ESC Key (27), 10ms 기다리기 - sleep 효과
    if key == 32:
        break;

if cap.isOpened():
    print('cap release!')
    cap.release()

cv2.destroyAllWindows()
```

```
cap release!
```

## 동영상 파일

```python
!dir data
```

```
 C 드라이브의 볼륨에는 이름이 없습니다.
 볼륨 일련 번호: 3A54-31BE

 C:\Users\Playdata\Documents\인공지능 25기\Computer Vision\data 디렉터리

2022-12-12  오전 10:40    <DIR>          .
2022-12-12  오전 10:40    <DIR>          ..
2022-12-12  오전 10:37           720,056 airplane.bmp
2022-12-12  오전 10:37           263,222 alphabet.bmp
2022-12-12  오전 10:37            50,728 box.png
2022-12-12  오전 10:37           122,490 box_in_scene.png
2022-12-12  오전 10:37            79,718 building.jpg
2022-12-12  오전 10:37            44,746 butterfly.jpg
2022-12-12  오전 10:37           538,711 candies.png
2022-12-12  오전 10:37           921,656 card.bmp
2022-12-12  오전 10:37           921,654 cat.bmp
2022-12-12  오전 10:37            28,288 circles.jpg
2022-12-12  오전 10:37         1,440,056 circuit.bmp
2022-12-12  오전 10:37            45,995 coins.png
2022-12-12  오전 10:37           161,078 contours.bmp
2022-12-12  오전 10:37            19,992 crystal.bmp
2022-12-12  오전 10:37           721,129 digits.png
2022-12-12  오전 10:37           196,664 dog.bmp
2022-12-12  오전 10:37           921,656 eastsea.bmp
2022-12-12  오전 10:37           104,464 exit-ramp.jpg
2022-12-12  오전 10:37           108,520 face.jpeg
2022-12-12  오전 10:37            31,321 faceQS.png
2022-12-12  오전 10:37           105,405 faceR.jpeg
2022-12-12  오전 10:37           317,168 faceRI.png
2022-12-12  오전 10:37           396,561 faceRN5.png
2022-12-12  오전 10:37         2,080,094 family.jpg
2022-12-12  오전 10:37           445,919 family2.jpg
2022-12-12  오전 10:37           720,056 field.bmp
2022-12-12  오전 10:37            85,222 flower.jpg
2022-12-12  오전 10:37            82,429 fruits.jpg
2022-12-12  오전 10:37           341,406 haarcascade_eye.xml
2022-12-12  오전 10:37           930,127 haarcascade_frontalface_default.xml
2022-12-12  오전 10:37            40,540 hand.jpg
2022-12-12  오전 10:37           136,678 hawkes.bmp
2022-12-12  오전 10:37            41,003 Heart10.jpg
2022-12-12  오전 10:37         4,039,698 images.zip
2022-12-12  오전 10:37           250,241 img1.jpg
2022-12-12  오전 10:37           253,190 img2.jpg
2022-12-12  오전 10:37           262,328 img3.jpg
2022-12-12  오전 10:37           786,488 keyboard.bmp
2022-12-12  오전 10:37           594,058 kids.png
2022-12-12  오전 10:37           591,978 kids2.png
2022-12-12  오전 10:37            91,814 lena.jpg
2022-12-12  오전 10:37           786,486 lenna.bmp
2022-12-12  오전 10:37            66,614 lenna256.bmp
2022-12-12  오전 10:37           346,678 mask.bmp
2022-12-12  오전 10:37           720,056 mask_plane.bmp
2022-12-12  오전 10:37           263,222 mask_smile.bmp
2022-12-12  오전 10:37           161,078 milkdrop.bmp
2022-12-12  오전 10:37           605,867 monarch.jpg
2022-12-12  오전 10:37            10,946 morphology.jpg
2022-12-12  오전 10:37         1,810,911 multi_faces.jpg
2022-12-12  오전 10:37           422,874 neutrophils.png
2022-12-12  오전 10:37             3,994 opencv_logo.png
2022-12-12  오전 10:37           563,944 oranges.jpg
2022-12-12  오전 10:37           486,190 people.png
2022-12-12  오전 10:37            16,336 people1.png
2022-12-12  오전 10:37            17,266 people2.png
2022-12-12  오전 10:37           786,486 pepper.bmp
2022-12-12  오전 10:37           921,656 polygon.bmp
2022-12-12  오전 10:37           182,704 psj.png
2022-12-12  오전 10:37             2,807 qrcode.png
2022-12-12  오전 10:37           677,043 ref.png
2022-12-12  오전 10:37           460,856 rose.bmp
2022-12-12  오전 10:37             3,238 S.bmp
2022-12-12  오전 10:37            54,820 skewed_chessboard.jpg
2022-12-12  오전 10:37           105,839 skewed_chessboard_org.jpg
2022-12-12  오전 10:37            66,614 square.bmp
2022-12-12  오전 10:37           208,094 srcThreshold.png
2022-12-12  오전 10:37         3,681,298 stopwatch.avi
2022-12-12  오전 10:37            46,768 sudoku.jpg
2022-12-12  오전 10:37         3,243,469 Team.jpeg
2022-12-12  오전 10:37           921,656 tekapo.bmp
2022-12-12  오전 10:37            92,601 test.jpg
2022-12-12  오전 10:37            33,159 thumbs_up_down.jpg
2022-12-12  오전 10:37         8,131,690 vtest.avi
2022-12-12  오전 10:37             8,978 waffle.jpg
              75개 파일          45,946,785 바이트
               2개 디렉터리  175,878,012,928 바이트 남음
```

```python
cap = cv2.VideoCapture('./data/stopwatch.avi')   # 0: main camera

if not cap.isOpened():
    print('Camera open failed!')
    sys.exit()

w = cap.get(cv2.CAP_PROP_FRAME_WIDTH)
h = cap.get(cv2.CAP_PROP_FRAME_HEIGHT)
fps = cap.get(cv2.CAP_PROP_FPS) # frame per second

delay = round(1000 / fps)  # 1000 / 30

while True:
    ret, frame = cap.read()  # frame은 이미지 한장

    if not ret:
        print('frame read error')
        break

    cv2.imshow('camera', frame)

    key = cv2.waitKey(delay)
    if key == 32:
        break;

if cap.isOpened():
    print('cap release!')
    cap.release()

cv2.destroyAllWindows()
```

```
frame read error
cap release!
```

## 동영상 저장

```python
cap = cv2.VideoCapture('./data/stopwatch.avi')   # 0: main camera

if not cap.isOpened():
    print('Camera open failed!')
    sys.exit()

w = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
h = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = cap.get(cv2.CAP_PROP_FPS) # frame per second

delay = round(1000 / fps)  # 1000 / 30

fourcc = cv2.VideoWriter_fourcc('D', 'I', 'V', 'X')  # DivX Mpeg-4 코덱
# fourcc = cv2.VideoWriter_fourcc(*'DIVX')

# 저장을 위한 객체 = cv2.VideoWriter(파일명, 코덱, FPS, 해상도)
outputVideo = cv2.VideoWriter('./out/output.avi', fourcc, fps, (w, h))

while True:
    ret, frame = cap.read()  # frame은 이미지 한장

    if not ret:
        print('frame read error')
        break

    cv2.imshow('camera', frame)   # 재생
    outputVideo.write(frame)     # 녹화

    key = cv2.waitKey(delay)
    if key == 32:
        break;

if cap.isOpened():
    print('cap release!')
    cap.release()

cv2.destroyAllWindows()
```

```
cap release!
```

## 드로이드캠 영상

```python
cap = cv2.VideoCapture('http://192.168.80.235:4747/mjpegfeed')   # 드로이드캠 연결 IP

if not cap.isOpened():
    print('Camera open failed!')
    sys.exit()

w = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
h = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = cap.get(cv2.CAP_PROP_FPS) # frame per second

delay = round(1000 / fps)  # 1000 / 30

fourcc = cv2.VideoWriter_fourcc('D', 'I', 'V', 'X')  # DivX Mpeg-4 코덱
# fourcc = cv2.VideoWriter_fourcc(*'DIVX')

# 저장을 위한 객체 = cv2.VideoWriter(파일명, 코덱, FPS, 해상도)
outputVideo = cv2.VideoWriter('./out/output.avi', fourcc, fps, (w, h))

while True:
    ret, frame = cap.read()  # frame은 이미지 한장

    if not ret:
        print('frame read error')
        break

    cv2.imshow('camera', frame)   # 재생
    outputVideo.write(frame)     # 녹화

    key = cv2.waitKey(delay)
    if key == 32:
        break;

if cap.isOpened():
    print('cap release!')
    cap.release()

cv2.destroyAllWindows()
```

```
cap release!
```

## 유튜브 영상

```python
import pafy
import youtube_dl
```

```python
url = 'https://www.youtube.com/watch?v=9SmQOZWNyWE&list=RD9SmQOZWNyWE&index=3'
video = pafy.new(url)
```

```python
print('title: ', video.title)
```

```
title:  BTS - "Permission to Dance" performed at the United Nations General Assembly | SDGs | Official Video
```

```python
print('rating: ', video.rating)
```

```
rating:  None
```

```python
print('duration: ', video.duration)
```

```
duration:  00:03:43
```

```python
best = video.getbest()
```

```python
print('download url: ', best.url)
```

```
download url:  https://rr2---sn-ab02a0nfpgxapox-bh2sd.googlevideo.com/videoplayback?expire=1670848494&ei=jsuWY6ahMK3L2roPrqa-mAU&ip=112.220.17.226&id=o-AHNAmGzx2KuKYzC7usWOAJmcvEKNOnqGFW9abkCA53NR&itag=18&source=youtube&requiressl=yes&mh=e9&mm=31%2C26&mn=sn-ab02a0nfpgxapox-bh2sd%2Csn-n4v7snl7&ms=au%2Conr&mv=m&mvi=2&pl=24&initcwndbps=760000&vprv=1&mime=video%2Fmp4&ns=LIheIsB9v4kOwszelDzLeD0J&cnr=14&ratebypass=yes&dur=223.445&lmt=1665478137806352&mt=1670826553&fvip=2&fexp=24001373%2C24007246&c=WEB&txp=5538434&n=_1_uNaZuS9TMFOnCc&sparams=expire%2Cei%2Cip%2Cid%2Citag%2Csource%2Crequiressl%2Cvprv%2Cmime%2Cns%2Ccnr%2Cratebypass%2Cdur%2Clmt&sig=AOq0QJ8wRQIgJsaOqxCZQGUgTmrQoC9Du9xRfjpMCeHlww3e2XFLW8sCIQDsCwoCOI6zSAKu561WmZJX-Mx-cTxjNLdlvz6bVs-g6A%3D%3D&lsparams=mh%2Cmm%2Cmn%2Cms%2Cmv%2Cmvi%2Cpl%2Cinitcwndbps&lsig=AG3C_xAwRQIhAMMM8TB5l7MdbPfgIbakyd3SYL_S5WTDINFSDPUl_ZCEAiAygCnv11qIygQyhXM9zJFPgF-ObzavvvM5MDYWGsNIOg%3D%3D
```

```python
print('resolution: ', best.resolution)
```

```
resolution:  640x360
```

```python
cap = cv2.VideoCapture(best.url) #  유튜브 다운로드 URL

if not cap.isOpened():
    print("Camera open failed!")
    sys.exit()

w = cap.get(cv2.CAP_PROP_FRAME_WIDTH)    
h = cap.get(cv2.CAP_PROP_FRAME_HEIGHT)    
fps = cap.get(cv2.CAP_PROP_FPS)   # frame per second
delay = round(1000/fps) # 1000/30 
print(delay)

while True:
    ret, frame = cap.read() # frame은 이미지 한장

    if not ret:
        print("frame read error")
        break

    cv2.imshow('origial', frame)
    cv2.imshow('inverse', 255 - frame)

    edge = cv2.Canny(frame, 100, 200)
    cv2.imshow('edge', edge)


    key = cv2.waitKey(delay) # ESC Key (27), 10ms 기다리기 (sleep 효과)
    if key == 32:
        break;

if cap.isOpened():
    print('cap release!')
    cap.release()

cv2.destroyAllWindows()   
```

```
33
cap release!
```

# 다양한 그리기 함수

```python
import numpy as np
```

```
# numpy ndarray로 색인할 때는 행(수직방향)을 색인 -> 열(수평방향)을 색인
img[100, 50]      
# openCV 함수에서 좌표를 찾아갈 때는 x좌표(수평방향) -> y좌표(수직방향)
pt1 = (50, 100)     # x좌표 50, y좌표 100
```

## 직선 그리기

```python
# np.full(사이즈, 초기값, 데이터타입)
img = np.full((400, 400, 3), 255, np.uint8)

pt1 = (50, 100) # x좌표, y좌표
pt2 = (150, 100) # x좌표, y좌표

cv2.line(img, pt1, pt2, (0, 0, 255), 2)

# 대각선
pt3 = (200, 100)
pt4 = (300, 150)
cv2.line(img, pt3, pt4, (0, 0, 255), 2, cv2.LINE_AA)



cv2.imshow('img', img)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 도형 그리기

```python
cv2.FILLED
```

```
-1
```

```python
img = np.full((400, 400, 3), 255, np.uint8)

# rectangle
# cv2.rectangle(도화지, 시작점, 끝점, 색깔, 굵기)  # 시작점 끝점은 대각방향으로 마주보는 점
cv2.rectangle(img, (50, 50), (150, 100), (0, 0, 255), 3)
cv2.rectangle(img, (50, 150), (150, 300), (0, 0, 255), cv2.FILLED)  # 굵기 자리에 -1을 입력하면 내부가 채워짐

# circle
# cv2.circle(도화지, 중심점, 반지름, 색깔, 굵기...)
cv2.circle(img, (300, 120), 30, (255, 255, 0), 2)
cv2.circle(img, (300, 200), 30, (255, 255, 0), cv2.FILLED)

# elipse
# cv.ellipse(도화지, 중심점, 반지름쌍, 기울기, 시작각도, 끝각도, 색깔, 굵기)
cv2.ellipse(img, (100, 300), (60, 30), 0, 0, 360, (255, 0, 0), 3)

# polylines
# cv2.polylines(도화지, [다각형을 이룰 점들], 다각형을 닫을지 여부, 색깔, 굵기...)
pts = np.array([[250, 250], [300, 250], [300, 300], [350, 300], [350, 350], [250, 350]])
cv2.polylines(img, [pts], True, (255, 0, 255), 2)

cv2.imshow('img', img)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 문자열 출력하기

```python
img = np.full((400, 400, 3), 255, np.uint8)

# text
# cv2.putText(도화지, 텍스트, 텍스트의 좌하단 좌표, 폰트, 스케일, 색깔, 굵기)
cv2.putText(img, 'Hello', (20, 50), cv2.FONT_HERSHEY_SIMPLEX, 2, (255, 0, 255), 2)

cv2.imshow('img', img)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
img1 = np.full((400, 400, 3), 255, np.uint8)

text = 'Hello, OpenCV'

fontFace = cv2.FONT_HERSHEY_SIMPLEX
fontScale = 1
thickness = 1

size_Text, retVal = cv2.getTextSize(text, fontFace, fontScale, thickness)

print(size_Text)
print(img.shape)

org_x = (img.shape[1] - size_Text[0]) // 2
org_y = (img.shape[0] + size_Text[1]) // 2

org_x, org_y

cv2.putText(img1, text, (org_x, org_y), fontFace, fontScale, (255, 0, 0), thickness)
cv2.rectangle(img1, (org_x, org_y), (org_x + size_Text[0], org_y - size_Text[1]), (0, 255, 0), 2)
cv2.circle(img1, (org_x, org_y), 5, (25, 100, 255))

cv2.imshow('imgText', img1)

cv2.destroyAllWindows()
```

```
(219, 22)
(400, 400, 3)
```

## 실습: 카운트 다운 만들기

```python
import time
```

```python
img2 = np.full((400, 400, 3), 255, np.uint8)

circle_size = 200

for i in range(5, 0, -1):
    text = str(i)

    cv2.circle(img2, (200, 200), circle_size, (100, 100, 100), 2)
    cv2.putText(img2, text, (180, 220), cv2.FONT_HERSHEY_SIMPLEX, 2, (200, 200, 200), 2)

    circle_size -= 30

    cv2.imshow('countdown', img2)
    cv2.waitKey(1000)
    img2 = np.full((400, 400, 3), 255, np.uint8)

cv2.destroyAllWindows()
```

```python
import cv2
import numpy as np
import sys
import matplotlib.pyplot as plt
```

## 이벤트 처리

### 키보드 이벤트

```python
img = cv2.imread('./data/lena.jpg')

cv2.imshow('img', img)
while True:
    keycode = cv2.waitKey()
    print(keycode)
    if keycode == ord('i'):
        img = 255 - img
        cv2.imshow('img', img)
    elif keycode == ord('q'):
        break

cv2.destroyAllWindows()
```

```
105
113
```

### 마우스 이벤트

```python
cv2.EVENT_LBUTTONDOWN
```

```
1
```

```python
cv2.EVENT_LBUTTONUP
```

```
4
```

```python
cv2.EVENT_MOUSEMOVE
```

```
0
```

```python
cv2.EVENT_FLAG_SHIFTKEY
```

```
16
```

```python
# 마우스 이벤트를 처리할 루틴
def on_mouse(event, x, y, flags, param):
    global old_x, old_y
    if event == cv2.EVENT_LBUTTONDOWN:
        old_x, old_y = x, y

    elif event == cv2.EVENT_LBUTTONUP:
        pass
    elif event == cv2.EVENT_MOUSEMOVE:
        if flags & cv2.EVENT_FLAG_LBUTTON:
            cv2.line(img, (old_x, old_y), (x, y), (0, 255, 255), 2)
            cv2.imshow('img', img)
            old_x, old_y = x, y


img = cv2.imread('./data/lena.jpg')

cv2.imshow('img', img)

# 마우스 이벤트가 발생했을 때 처리할 루틴(함수) 등록
cv2.setMouseCallback('img', on_mouse)

cv2.waitKey()
cv2.destroyAllWindows()
```

### 트랙바 이벤트

```python
def on_level_change(pos):
    # 이벤트가 발생할 때마다 화면 밝기가 바뀌도록 구현
    img[:] = pos
    cv2.imshow('img', img)

img = np.full((512, 512, 3), 0, np.uint8)

cv2.imshow('img', img)

# 트랙바 이벤트가 발생했을 때 처리할 루틴(함수) 등록
# cv2.createTrackbar(트랙바이름, 윈도우, 트랙바값의 범위, 이벤트발생시 처리할 함수)
cv2.createTrackbar('level', 'img', 0, 255, on_level_change)
cv2.setTrackbarPos('level', 'img', 128)      # 시작점 지정

cv2.waitKey()
cv2.destroyAllWindows()
```

```python
def onChange(x):
    pass

img = np.zeros((1024 , 1024, 3), np.uint8)
cv2.namedWindow('trackBar',cv2.WINDOW_NORMAL)
cv2.createTrackbar('R', 'trackBar',0,255, onChange)
cv2.createTrackbar('G', 'trackBar', 0, 255, onChange)
cv2.createTrackbar('B','trackBar', 0, 255, onChange)

while True:
    cv2.imshow('trackBar', img)
    R = cv2.getTrackbarPos('R', 'trackBar')
    G = cv2.getTrackbarPos('G', 'trackBar')
    B = cv2.getTrackbarPos('B', 'trackBar')

    img[:] = [B,G,R]
    k = cv2.waitKey(1)
    if k == 27:
        break

cv2.destroyAllWindows()
```

```python
def on_level_change(pos):
    R = cv2.getTrackbarPos('R', 'img')
    G = cv2.getTrackbarPos('G', 'img')
    B = cv2.getTrackbarPos('B', 'img')
    img[:] = (B, G, R)
    cv2.imshow('img', img)

img = np.full((512, 512, 3), 0, np.uint8)

cv2.imshow('img', img)

cv2.createTrackbar('R', 'img', 0, 255, on_level_change)
cv2.createTrackbar('G', 'img', 0, 255, on_level_change)
cv2.createTrackbar('B', 'img', 0, 255, on_level_change)
cv2.setTrackbarPos('B', 'img', 255)

cv2.waitKey()
cv2.destroyAllWindows()
```

# 유용한 기능들

## 마스크 연산

```python
lena = cv2.imread('./data/lenna.bmp')
mask = cv2.imread('./data/mask_smile.bmp', cv2.IMREAD_GRAYSCALE)

# mask 이미지에서 흰색 부분(mask > 0)의 위치만 레나영상에서 노랑색으로 바꾸기
lena[mask > 0] = (0, 255, 255) # yellow

cv2.imshow('lena', lena)
cv2.imshow('mask', mask)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
lena[mask > 0] = (0, 255, 255) # yellow

cv2.imshow('lena', lena)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/airplane.bmp', cv2.IMREAD_COLOR)
mask = cv2.imread('./data/mask_plane.bmp', cv2.IMREAD_GRAYSCALE)
dst = cv2.imread('./data/field.bmp', cv2.IMREAD_COLOR)

dst[[mask > 0]] = src[mask > 0]

cv2.imshow("src", src)
cv2.imshow("mask", mask)
cv2.imshow("dst", dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```
C:\Users\Playdata\AppData\Local\Temp\ipykernel_11108\1373217919.py:5: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
  dst[[mask > 0]] = src[mask > 0]
```

# 영상의 밝기 조절

**영상의 밝기**

- 분류기를 만들 때 특징으로 활용이 될 수 있음 $ ~~~ $ 예) 주간/야간 영상
- 어두운 데이터의 밝기값을 조정해서 품질을 높일 때 활용
- 딥러닝의 데이터를 증강(원본 데이터 + 밝기가 조정된 데이터)하는 목적으로 활용

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)
src = np.array(src, dtype=np.int32)  # 음수와 255보다 큰 수까지 표현할 수 있게

dst = src.copy()
dst = src + 50
dst = np.clip(dst, 0, 255)  # dst의 상한선과 하한선을 255, 0으로 지정

# 데이터 타입 복구
src = np.array(src, dtype=np.uint8)
dst = np.array(dst, dtype=np.uint8)


cv2.imshow('src', src)
cv2.imshow('dst', dst)

cv2.waitKey()
cv2.destroyAllWindows()
```

**영상의 밝기를 +100만큼 조절**

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

dst = cv2.add(src, 100)

cv2.imshow('src', src)
cv2.imshow('dst', dst)

cv2.waitKey()
cv2.destroyAllWindows()
```

**TrackBar를 이용해서 레나영상의 밝기를 조절**

```python
def update(pos):
    dst = cv2.add(src, pos)
    cv2.imshow('dst', dst)

src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)
dst = src.copy()
cv2.imshow('dst', dst)

cv2.createTrackbar('brightness', 'dst', 0, 100, update)

cv2.waitKey()
cv2.destroyAllWindows()
```

# 영상의 명암비 조절

```python
from IPython.display import Image
Image('./images/image1.png')
```

![image](https://user-images.githubusercontent.com/84713532/207256704-bf5c3303-5c40-49e1-a479-c01c6c684837.png)


```python
Image('./images/image2.png')
```

![image](https://user-images.githubusercontent.com/84713532/207256732-7af6b970-6cd1-49c1-a338-f7fb40fb3e7c.png)


```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

alpha = 1.0

dst = src + (src - 128.0) * alpha
dst = np.clip(dst, 0, 255)
dst = dst.astype(src.dtype)

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 히스토그램 분석

## cv2.calcHist() 함수

```python
src = np.array([[0, 0, 0, 0],
                [1, 2, 3, 5],
                [6, 1, 2, 3],
                [4, 3, 1, 7]], dtype=np.uint8) # 4*4, 1 channel 영상
```

```python
# cv2.calcHist(images=[이미지], channels=[채널], mask=[마스크], histSize=[구간], ranges=[범위])
hist = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[8], ranges=[0, 8])
hist
```

```
array([[4.],
       [3.],
       [2.],
       [3.],
       [1.],
       [1.],
       [1.],
       [1.]], dtype=float32)
```

```python
hist2 = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[4], ranges=[0, 8])
hist2
```

```
array([[7.],
       [5.],
       [2.],
       [2.]], dtype=float32)
```

```python
hist3 = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[4], ranges=[0, 4])
hist3
```

```
array([[4.],
       [3.],
       [2.],
       [3.]], dtype=float32)
```

## 히스토그램 구하기 (lena)

**그레이 스케일 영상**

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)
hist = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[32], ranges=[0, 255])

plt.plot(hist, color='r')
plt.bar(np.arange(32), hist.flatten(), color='c')
```

```
<BarContainer object of 32 artists>
```

![image](https://user-images.githubusercontent.com/84713532/207256793-a126cc14-69d5-4e1d-8885-fd5c8d9c2240.png)


**컬러 영상(채널별 히스토그램)**

```python
src = cv2.imread('./data/lenna.bmp')
colors = ['b', 'g', 'r']

for i in range(3):
    hist = cv2.calcHist(images=[src], channels=[i], mask=None, histSize=[256], ranges=[0, 255])
    plt.plot(hist, color=colors[i])
```

![image](https://user-images.githubusercontent.com/84713532/207256819-cb0290fb-826f-4dd4-bff9-b8c271be9dd9.png)


```python
cv2.imshow('src', src)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 히스토그램 스트레칭

```python
from IPython.display import Image
Image('./images/image3.png')
```

![image](https://user-images.githubusercontent.com/84713532/207256853-f2ec8c78-4431-4abc-a471-85e77e9b02a9.png)


```python
src = cv2.imread('./data/hawkes.bmp', cv2.IMREAD_GRAYSCALE)

dst = (src - src.min()) / (src.max() - src.min()) * 255
dst = np.array(dst, dtype=np.uint8)

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

**히스토그램으로 src, dst의 명암비 확인**

```python
# 히스토그램 스트레칭 전
src_hist = hist = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[256], ranges=[0, 255])
plt.bar(np.arange(256), src_hist.flatten(), color='c')
plt.show()

# 히스토그램 스트레칭 후
dst_hist = hist = cv2.calcHist(images=[dst], channels=[0], mask=None, histSize=[256], ranges=[0, 255])
plt.bar(np.arange(256), dst_hist.flatten(), color='b')
plt.show()
```
![image](https://user-images.githubusercontent.com/84713532/207256895-7979b3ae-d513-45ac-986b-d6358cb5d5bd.png)


## 히스토그램 평활화 (GrayScale Image)

![image](https://user-images.githubusercontent.com/84713532/207256964-1c1a5549-dfc7-444f-8e51-9430a104b53c.png)


```python
src = cv2.imread('./data/hawkes.bmp', cv2.IMREAD_GRAYSCALE)
dst = cv2.equalizeHist(src)

cv2.imshow("src", src)
cv2.imshow("dst", dst)
cv2.waitKey()
cv2.destroyAllWindows() 
```

**히스토그램으로 src, dst의 명암비 확인**

```python
# 히스토그램 평활화 전
src_hist = hist = cv2.calcHist(images=[src], channels=[0], mask=None, histSize=[256], ranges=[0, 255])
plt.bar(np.arange(256), src_hist.flatten(), color='c')
plt.show()

# 히스토그램 평활화 후
dst_hist = hist = cv2.calcHist(images=[dst], channels=[0], mask=None, histSize=[256], ranges=[0, 255])
plt.bar(np.arange(256), dst_hist.flatten(), color='b')
plt.show()
```

![image](https://user-images.githubusercontent.com/84713532/207257050-e93404c8-2636-48ad-ab1a-8b4a23f7e93e.png)


## 히스토그램 평활화 (Color Image)

**컬러이미지 히스토그램 평활화의 잘못된 예**

- 각 채널별로 평활화를 수행한 후 합치게 되면
- 입력 영상만의 고유한 색상 조합이 깨짐

```python
src = cv2.imread('./data/pepper.bmp')

b = src[:, :, 0]
g = src[:, :, 1]
r = src[:, :, 2]

# b, g, r = cv2.split(src)          # 나누기

dst_b = cv2.equalizeHist(b)
dst_g = cv2.equalizeHist(g)
dst_r = cv2.equalizeHist(r)

dst = src.copy()
dst[:, :, 0] = dst_b
dst[:, :, 1] = dst_g
dst[:, :, 2] = dst_r            
# cv2.merge([dst_b, dst_g, dst_r])  # 합치기

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

**컬러이미지 히스토그램 평활화의 잘된 예**

- 명암비를 조절한다는 것은 '밝기'값만 관계가 있으므로
- 컬러공간(Color Space)을 BGR에서 yCrCb(y: 밝기값, Cr/Cb 색상)로 바꾼 뒤에
- y(밝기) 채널에 대해서만 히스토그램 평활화를 수행
- 합치면 색상 정보는 그대로 유지

```python
src = cv2.imread('./data/pepper.bmp')  # BGR
src_yCrCb = cv2.cvtColor(src, cv2.COLOR_BGR2YCrCb)

y, Cr, Cb = cv2.split(src_yCrCb)
y_equalized = cv2.equalizeHist(y)

dst_yCrCb = cv2.merge([y_equalized, Cr, Cb])
dst = cv2.cvtColor(src_yCrCb, cv2.COLOR_YCrCb2BGR)

cv2.imshow('src', src)
cv2.imshow('dst', dst)  # BGR 채널 순서를 기대
cv2.waitKey()
cv2.destroyAllWindows()
```
```python
import cv2
import numpy as np
```

# 영상의 산술 연산

```python
src1 = cv2.imread('./data/lenna256.bmp', cv2.IMREAD_GRAYSCALE)
src2 = cv2.imread('./data/square.bmp', cv2.IMREAD_GRAYSCALE)

dst1 = cv2.add(src1, src2)
dst2 = cv2.addWeighted(src1, 1, src2, 0.3, 0)
dst3 = cv2.subtract(src1, src2)
dst4 = cv2.absdiff(src1, src2)

cv2.imshow('src1', src1)
cv2.imshow('src2', src2)
# cv2.imshow('dst1', dst1)
# cv2.imshow('dst2', dst2)
# cv2.imshow('dst3', dst3)
cv2.imshow('dst4', dst4)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 영상의 논리 연산

```python
src1 = cv2.imread('./data/lenna256.bmp', cv2.IMREAD_GRAYSCALE)
src2 = cv2.imread('./data/square.bmp', cv2.IMREAD_GRAYSCALE)

dst1 = cv2.bitwise_and(src1, src2)
dst2 = cv2.bitwise_or(src1, src2)
dst3 = cv2.bitwise_xor(src1, src2)
dst4 = cv2.bitwise_not(src1)

cv2.imshow('src1', src1)
cv2.imshow('src2', src2)
cv2.imshow('dst1', dst1)
cv2.imshow('dst2', dst2)
cv2.imshow('dst3', dst3)
cv2.imshow('dst4', dst4)

cv2.waitKey()
cv2.destroyAllWindows()
```

**(참고) 영상의 이진화

```python
def on_thresh(pos):
    # cv2.threshold(이미지, 임계값, 임계값을 넘었을때 적용할 최대값, 임계값연산방법)
    ret, dst = cv2.threshold(src, pos, 255, cv2.THRESH_BINARY)
    cv2.imshow('dst', dst)

src = cv2.imread('./data/neutrophils.png', cv2.IMREAD_GRAYSCALE)
dst = src.copy()

cv2.imshow('src', src)
cv2.imshow('dst', dst)

cv2.createTrackbar('threshold', 'dst', 0, 255, on_thresh)

cv2.waitKey()
cv2.destroyAllWindows()
```

```python
# 빈 들판에 비행기 띄우기
airplane = cv2.imread('./data/airplane.bmp', cv2.IMREAD_COLOR)
field = cv2.imread('./data/field.bmp', cv2.IMREAD_COLOR)

gray = cv2.cvtColor(airplane, cv2.COLOR_BGR2GRAY)
ret, mask = cv2.threshold(gray, 163, 255, cv2.THRESH_BINARY)

mask_inv = cv2.bitwise_not(mask)
field[mask_inv > 0] = airplane[mask_inv > 0]

# cv2.imshow('airplane', airplane)
cv2.imshow('field', field)
# cv2.imshow('gray', gray)
# cv2.imshow('mask', mask)
cv2.imshow('mask_inv', mask_inv)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 영상의 필터링

## 엠보싱 필터

```python
src = cv2.imread('./data/rose.bmp', cv2.IMREAD_GRAYSCALE)

emboss = np.array([[-1, -1, 0],
                   [-1, 0, 1],
                   [0, 1, 1]])

# cv2.filter2D(적용할 이미지, 출력채널수, 필터)
dst = cv2.filter2D(src, -1, emboss, delta = 128)   # -1은 입력 영상과 출력 영상의 채널 깊이 동일
                                                   # 필터링 연산의 결과, 전체 영상의 값이 작아짐
                                                   # delta=128을 통해서 전체 결과에 128을 더해줌
                                                   # 전반적으로 밝게 표시해주는 효과

cv2.imshow('src', src)
cv2.imshow('dst', dst)

cv2.waitKey()
cv2.destroyAllWindows()
```

## 블러링

### 평균값 필터

```python
src = cv2.imread('./data/rose.bmp', cv2.IMREAD_GRAYSCALE)

blur = np.array([[1, 1, 1],
                 [1, 1, 1],
                 [1, 1, 1]], dtype=np.float32) * 1/9

dst = cv2.filter2D(src, -1, blur)

cv2.imshow('src', src)
cv2.imshow('dst', dst)

cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/rose.bmp', cv2.IMREAD_GRAYSCALE)
cv2.imshow('src', src)

for ksize in (3, 5, 7):
    # cv2.blur(입력영상, 필터사이즈)
    dst = cv2.blur(src, (ksize, ksize))
    desc = 'Mean: %d X %d' % (ksize, ksize)
    cv2.putText(dst, desc, (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1.0, 255, 1, cv2.LINE_AA)
    cv2.imshow('dst', dst)
    cv2.waitKey()

cv2.destroyAllWindows()
```

### 가우시안 필터

```python
src = cv2.imread('./data/rose.bmp', cv2.IMREAD_GRAYSCALE)
cv2.imshow('src', src)

for sigma in range(1, 6):
    # cv2.GaussianBlur(입력영상, 커널사이즈, 시그마)
    dst = cv2.GaussianBlur(src, (0, 0), sigma)
    desc = 'Gaussian: sigma %d'% (sigma)
    cv2.putText(dst, desc, (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1.0, 255, 1, cv2.LINE_AA)
    cv2.imshow('dst', dst)
    cv2.waitKey()

cv2.destroyAllWindows()
```

## 샤프닝 (영상 날카롭게 하기)

```python
from IPython.display import Image
Image('./images/image4.png')
```

![image](https://user-images.githubusercontent.com/84713532/207936538-1228121e-a823-45a9-a0cd-04db66dfd2c8.png)


```python
src = cv2.imread('./data/rose.bmp', cv2.IMREAD_GRAYSCALE)
cv2.imshow('src', src)

for sigma in range(1, 6):  # sigma가 증감함에 따라 Blur 강도가 커짐 -> 샤프닝 강도가 커짐
    blurred = cv2.GaussianBlur(src, (0, 0), sigma)
    alpha = 1.0
    dst = cv2.addWeighted(src, (1 + alpha), blurred, -alpha, 0)
    desc = "Guassian: sigma %d"%(sigma)
    cv2.putText(dst, desc, (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1.0, 255, 1, cv2.LINE_AA)
    cv2.imshow('dst', dst)
    cv2.waitKey()

cv2.destroyAllWindows()
```

## 가우시안 잡음 모델

```python
Image('./images/image5.png')
```

![image](https://user-images.githubusercontent.com/84713532/207936573-28ed2213-0e63-4817-9737-3c6f1ac91555.png)


```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)
cv2.imshow('src', src)

for stdev in [10, 20, 30]:
    noise = np.zeros(src.shape, np.int32)
    cv2.randn(noise, 0, stdev)
    dst = cv2.add(src, noise, dtype=cv2.CV_8UC1)  # 8CU1: 8 bit Unsigned 1 Channel
    desc = "stdev: %d"%(stdev)
    cv2.putText(dst, desc, (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1.0, 255, 1, cv2.LINE_AA)

    cv2.imshow('dst', dst)
    cv2.waitKey()
cv2.destroyAllWindows()
```

## 양방향 필터

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

noise = np.zeros(src.shape, np.int32)
cv2.randn(noise, 0, 5)
dst = cv2.add(src, noise, dtype=cv2.CV_8UC1) # np.uint8

# 가우시안
dst_gaussian = cv2.GaussianBlur(dst, (0, 0), 5)
# 양방향필터
dst_bilateral = cv2.bilateralFilter(dst, -1, 10, 5)
# sigmaColor : 밝기값의 차이에 따라 에지를 얼마나 보전할지 여부(이 값이 작을수록 에지가 더 보전)
# sigmaSpace : 거리의 차이(필터 사이즈) 기준으로 얼마나 블러링을 강하게 할지 여부(이 값이 클수록 블러링이 강하게 적용)

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.imshow('dst_gaussian', dst_gaussian)
cv2.imshow('dst_bilateral', dst_bilateral)
cv2.waitKey()    
cv2.destroyAllWindows()
```

## 미디언 필터

```python
import random
```

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

# salt & pepper noise(소금 & 후추)

for i in range(0, int(src.size/10)):
    x = random.randint(0, src.shape[0] - 1)
    y = random.randint(0, src.shape[1] - 1)
    src[x, y] =(i % 2) * 255 # i가 짝수일 때는 0(pepper)값이 들어가고, 홀수일 때는 255(salt)값이 들어감

gaussian_blur = cv2.GaussianBlur(src, (0, 0), 1)
median_blur = cv2.medianBlur(src, 3)



cv2.imshow('src', src)
cv2.imshow('gaussian_blur', gaussian_blur)
cv2.imshow('median_blur', median_blur)

cv2.waitKey()
cv2.destroyAllWindows()
```

# 영상의 기하학적 변환

## 어파인 변환

```python
src = cv2.imread('./data/tekapo.bmp')

src_pts = np.array([[0, 0], [src.shape[1] - 1, 0], [src.shape[1] - 1, src.shape[0] - 1]], dtype=np.float32)
dst_pts = np.array([[50, 50], [500, 100], [600, 400]], dtype=np.float32)

M = cv2.getAffineTransform(src_pts, dst_pts)  # 2 X 3 변환행렬을 반환
dst = cv2.warpAffine(src, M, (0, 0))   # dsize=(0, 0): 원본 영상과 동일한 사이즈


cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 이동 변환

```python
src = cv2.imread('./data/tekapo.bmp')

a = 150  # x축으로 이동할 픽셀 수
b = 100  # y축으로 이동할 픽셀 수

M = np.array([[1, 0, a],
              [0, 1, b]], dtype=np.float32)

dst = cv2.warpAffine(src, M, (0, 0))   # dsize=(0, 0): 원본 영상과 동일한 사이즈


cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```
```python
import cv2
import numpy as np
```

# 영상의 기하학적 변환

## 전단 변환

```python
src = cv2.imread('./data/tekapo.bmp')

height = src.shape[0]
width = src.shape[1]

Mx = 0.3

M = np.array([[1, Mx, 0],
              [0, 1, 0]], dtype=np.float64)

dst = cv2.warpAffine(src, M, (int(width + Mx*height) , height)) # dsize=(0, 0) : 원본영상과 동일한 사이즈

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 크기 변환

```python
src = cv2.imread('./data/tekapo.bmp')

height = src.shape[0]
width = src.shape[1]

Sx = 2
Sy = 2


M = np.array([[Sx, 0, 0],
              [0, Sy, 0]], dtype=np.float64)

dst = cv2.warpAffine(src, M, (int(width * Sx), int(height * Sy))) # dsize=(0, 0): 원본 영상과 동일한 사이즈


cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/tekapo.bmp')

dst = cv2.resize(src, (0, 0), fx=1.2, fy=1.2)

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/tekapo.bmp')

dst = cv2.resize(src, (1920, 1280))

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 회전 변환

```python
src = cv2.imread('./data/tekapo.bmp')

height = src.shape[0]
width = src.shape[1]

center = width / 2, height / 2
angle =20 # 반시계방향 20도
scale = 1

M = cv2.getRotationMatrix2D(center, angle, scale)

dst = cv2.warpAffine(src, M, (0, 0)) # dsize=(0, 0): 원본 영상과 동일한 사이즈


cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
# 90도 단위로 회전할 때 rotate 함수 사용
src = cv2.imread('./data/tekapo.bmp')

dst1 = cv2.rotate(src, cv2.ROTATE_90_CLOCKWISE)
dst2 = cv2.rotate(src, cv2.ROTATE_90_COUNTERCLOCKWISE)

cv2.imshow('src', src)
cv2.imshow('dst1', dst1)
cv2.imshow('dst2', dst2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 대칭 변환

```python
src = cv2.imread('./data/tekapo.bmp')

dst = cv2.flip(src, 1) # 좌우 반전

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/tekapo.bmp')

dst = cv2.flip(src, 0)  # 상하 반전

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/tekapo.bmp')

dst = cv2.flip(src, -1)  # 상하좌우 반전

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 투시변환

```python
src = cv2.imread('./data/tekapo.bmp')

height = src.shape[0]
width = src.shape[1]

src_pts = np.array([[0, 0], [width - 1, 0], [width - 1, height - 1], [0, height - 1]], np.float32)
dst_pts = np.array([[60, 100], [width - 20, 80], [width - 10, height - 10], [5, height - 20]], np.float32)

M = cv2.getPerspectiveTransform(src_pts, dst_pts)
dst = cv2.warpPerspective(src, M, (0, 0))


cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
def on_mouse(event, x, y, flag, param):
    if event == cv2.EVENT_LBUTTONDOWN:
        src_pt_list.append([x, y])
        cv2.circle(src, (x, y), 5, (0, 0, 255), 5)
        cv2.imshow('src', src)
        if len(src_pt_list) == 4 :
            src_pts = np.array(src_pt_list, dtype=np.float32)
            M = cv2.getPerspectiveTransform(src_pts, dst_pts)
            dst = cv2.warpPerspective(src, M, (width, height))
            cv2.imshow('dst', dst)

src_pt_list = []
width, height = 200, 300
dst_pts = np.array([[0, 0], [width-1, 0], [width-1, height-1], [0, height-1]], np.float32) # 마우스로 클릭한 순서대로 결과에도 매칭

src = cv2.imread('./data/card.bmp')

cv2.imshow('src', src)
cv2.setMouseCallback('src', on_mouse)

cv2.waitKey()
cv2.destroyAllWindows()
```

# 에지 검출과 응용

## 마스크 기반 에지 검출 - 소벨 마스크

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

Mx = np.array([[-1, 0, 1],
               [-2, 0, 2],
               [-1, 0, 1]], dtype=np.float32)
My = np.array([[-1, -2, -1],
               [0, 0, 0],
               [1, 2, 1]], dtype=np.float32)


dx = cv2.filter2D(src, -1, Mx)
dy = cv2.filter2D(src, -1, My)

cv2.imshow('src', src)
cv2.imshow('dx', dx)
cv2.imshow('dy', dy)
cv2.waitKey()
cv2.destroyAllWindows()
```

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

# 미분필터(소벨필터)를 따로 준비하지 않고, 원본 이미지와 마스크 연산까지 해주는 함수
dx = cv2.Sobel(src, cv2.CV_32FC1, 1, 0) # x축으로 미분
dy = cv2.Sobel(src, cv2.CV_32FC1, 0, 1) # y축으로 미분
# cv2.Sobel() 함수는 cv2.filter2D()로 마스크 연산까지는 동일한 형변환은 안되어 있는 상태

fmag = cv2.magnitude(dx, dy)  # [x축으로 미분, y축으로의 미분] = 그래디언트, magnitude 함수가 그래디언트의 크기를 구해줌
mag = np.clip(fmag, 0, 255).astype(np.uint8)

T = 150
ret, dst = cv2.threshold(mag, T, 255, cv2.THRESH_BINARY)

cv2.imshow('src', src)
cv2.imshow('mag', mag)
cv2.imshow('dst', dst)

cv2.waitKey()
cv2.destroyAllWindows()
```

## 캐니 에지 검출기

```python
src = cv2.imread('./data/lenna.bmp', cv2.IMREAD_GRAYSCALE)

dst = cv2.Canny(src, 90, 150)   # low: high (1:2 or 1:3 recommended)

cv2.imshow('src', src)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 허프 변환 직선 검출

```python
import math

src = cv2.imread('./data/building.jpg', cv2.IMREAD_GRAYSCALE)

edge = cv2.Canny(src, 100, 200)
rho = 1  # or 2 숫자가 작을수록 정밀하게 검출하지만 연산시간이 더 걸림
theta = math.pi / 180  # radian unit
threshold = 120   # 축적배열의 숫자가 높다는 것은 직선을 이루는 점들이 많다는 뜻
                  # 얼마나 큰 값을 직선으로 판단할지는 threshold에 달려있음
minLineLength = 100  # 검출할 선분의 최소길이
maxLineGap = 10  # 직선으로 간주할 최대 에지 점 간격

lines = cv2.HoughLinesP(edge, rho, theta, threshold, minLineLength = minLineLength,
                       maxLineGap = maxLineGap)

dst = cv2.cvtColor(edge, cv2.COLOR_GRAY2BGR)  # 직선을 그릴 도화지 (3 채널 도화지)

if lines is not None:
    for i in range(len(lines)):
        line = lines[i][0]
        pt1 = line[0], line[1]
        pt2 = line[2], line[3]
        cv2.line(dst, pt1, pt2, (0, 0, 255), 2, cv2.LINE_AA)


cv2.imshow('src', src)
cv2.imshow('edge', edge)
cv2.imshow('dst', dst)
cv2.waitKey()
cv2.destroyAllWindows()
```
