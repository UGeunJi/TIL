# 신경망

```python
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import Image
```

## 활성화 함수

- 계단함수

```python
def step_function(x):
    return np.array(x > 0, dtype=np.int32)
```

```python
X = np.arange(-5.0, 5.0, 0.1)
Y = step_function(X)

plt.plot(X, Y)
```

```
[<matplotlib.lines.Line2D at 0x1d3790463d0>]
```

![image](https://user-images.githubusercontent.com/84713532/209353021-a2fa6931-8a37-4f57-933f-2c77428e2819.png)


- 시그모이드 함수

```python
def sigmoid(x):
    return 1 / (1 + np.exp(-x))
```

```python
X = np.arange(-5.0, 5.0, 0.1)
Y = sigmoid(X)

plt.plot(X, Y)
```

```
[<matplotlib.lines.Line2D at 0x1d37abe7df0>]
```

![image](https://user-images.githubusercontent.com/84713532/209353052-918e9521-b57e-432a-b959-108e83e32373.png)


- ReLU

```python
def relu(x):
    return np.maximum(0, x)
```

```python
X = np.arange(-5.0, 5.0, 0.1)
Y = relu(X)

plt.plot(X, Y)
```

```
[<matplotlib.lines.Line2D at 0x1d37afa58e0>]
```
![image](https://user-images.githubusercontent.com/84713532/209353076-756cd57a-cced-4908-8cc1-98fb45689de5.png)

# 신경망

```python
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import Image
```

## 다차원 배열 계산

```python
from IPython.display import Image
Image('./deep_learning_images/fig 3-11.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353204-3d350ec3-fd8f-4fe9-9ff7-dd69093d18f6.png)


```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

result = np.dot(A, B)
result
```

```
array([[19, 22],
       [43, 50]])
```

```python
Image('./deep_learning_images/fig 3-12.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353240-0b8b8592-c90d-4f24-8083-eb83dc4cfae3.png)


```python
A = np.array([[3, 2], [2, 1], [3, 3]])
B = np.array([[2, 4, 1, 1], [2, 3, 1, 6]])

C = np.dot(A, B)
C
```

```
array([[10, 18,  5, 15],
       [ 6, 11,  3,  8],
       [12, 21,  6, 21]])
```

```python
Image('./deep_learning_images/fig 3-13.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353265-dfaee462-e319-47c7-872c-140b79b5d243.png)


```python
A = np.array([[2, 4], [1, 2], [3, 3]])
B = np.array([3, 2])

C = np.dot(A, B)
C
```

```
array([14,  7, 15])
```

## 신경망에서의 행렬곱

```python
Image('./deep_learning_images/fig 3-14.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353289-279a652b-26eb-4322-8558-bd71f155dd8e.png)


```python
A = np.array([3, 2])
B = np.array([[2, 4, 2], [1, 2, 3]])

C = np.dot(A, B)
C
```

```
array([ 8, 16, 12])
```

```python
Image('./deep_learning_images/fig 3-17.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353317-0a190add-23d4-4709-ae46-b55623c0f607.png)


```python
Image('./deep_learning_images/e 3.9.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353358-22c9f8e5-092c-42cf-8d00-99ea6c2d2363.png)


```python
X = np.array([[1.0, 0.3]])  # (2, )
W1 = np.array([[0.3, 0.3, 0.2], [0.2, 0.5, 0.3]]) # (2, 3)
B1 = np.array([[0.1, 0.2, 0.3]])  # (3, )

A1 = np.dot(X, W1) + B1

print(X.shape, W1.shape, B1.shape, A1.shape, A1)
```

```
(1, 2) (2, 3) (1, 3) (1, 3) [[0.46 0.65 0.59]]
```

```python
Image('./deep_learning_images/fig 3-18.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353380-4ad19ba9-0b3f-4c34-ba21-6dd2c8563b0b.png)


```python
def sigmoid(x):
    return 1 / (1 + np.exp(-x))
```

```python
Z1 = sigmoid(A1)
Z1
```

```
array([[0.61301418, 0.65701046, 0.64336515]])
```

```python
Z1.shape
```

```
(1, 3)
```

```python
Image('./deep_learning_images/fig 3-19.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353408-ec57138f-40bf-4399-a7ec-3cd7b170f789.png)


```python
W2 = np.array([[0.7, 0.3], [0.1, 0.2], [0.4, 0.2]])
B2 = np.array([0.1, 0.3])


A2 = np.dot(Z1, W2) + B2

Z2 = sigmoid(A2)

print(W2.shape, B2.shape, A2.shape, Z2.shape, Z2)
```

```
(3, 2) (2,) (1, 2) (1, 2) [[0.70101943 0.67786542]]
```

```python
Image('./deep_learning_images/fig 3-20.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353429-ee315a2f-aee5-4322-b312-5caee9626980.png)


```python
def identity_function(x):
    return x
```

```python
W3 = np.array([[0.1, 0.3], [0.2, 0.4]]) # (2, 2)
B3 = np.array([0.1, 0.2])  # (2, )

A3 = np.dot(Z2, W3) + B3

Y = identity_function(A3)

print(W3.shape, B3.shape, A3.shape, Y.shape, Y)
```

```
(2, 2) (2,) (1, 2) (1, 2) [[0.30567503 0.681452  ]]
```

## 출력층(Softmax 함수)

```python
def softmax(a):
    c = np.max(a)
    exp_a = np.exp(a - c)
    sum_exp_a = np.sum(exp_a)
    y = exp_a / sum_exp_a

    return y
```

## 3층 신경망 구현

```python
def init_network():
    network = {}
    network['W1'] = np.array([[0.3, 0.3, 0.2], [0.2, 0.5, 0.3]]) # (2, 3)
    network['B1'] = np.array([[0.1, 0.2, 0.3]])  # (3, )

    network['W2'] = np.array([[0.7, 0.3], [0.1, 0.2], [0.4, 0.2]])
    network['B2'] = np.array([0.1, 0.3])

    network['W3'] = np.array([[0.1, 0.3], [0.2, 0.4]]) # (2, 2)
    network['B3'] = np.array([0.1, 0.2])  # (2, )

    return network

def forward(network, X):
    W1, W2, W3 = network['W1'], network['W2'], network['W3']
    B1, B2, B3 = network['B1'], network['B2'], network['B3']

    A1 = np.dot(X, W1) + B1
    Z1 = sigmoid(A1)
    A2 = np.dot(Z1, W2) + B2
    Z2 = sigmoid(A2)
    A3 = np.dot(Z2, W3) + B3
    Y = identity_function(A3)

    return Y
```

```python
network = init_network()
X = np.array([1.0, 0.5]) # (2, )

Y = forward(network, X)
Y
```

```
array([[0.30640938, 0.68321928]])
```

## 손글씨 숫자(MNIST)

```python
from dataset.mnist import load_mnist

def get_data():
    (X_train, y_train), (X_test, y_test) = load_mnist(normalize=True, flatten=True, one_hot_label=False)
    return X_test, y_test

X_test, y_test = get_data()

print(X_test.shape, y_test.shape)
```

```
(10000, 784) (10000,)
```

```python
plt.imshow(X_test[1000].reshape(28, 28), cmap='binary')
```

```
<matplotlib.image.AxesImage at 0x25a693e5340>
```

![image](https://user-images.githubusercontent.com/84713532/209353456-6be63c0b-9b9b-4669-a55e-dcb43f2eb883.png)


```python
import pickle

def init_network():
    with open('sample_weight.pkl', 'rb') as f:
        network = pickle.load(f)
    return network
```

```python
network = init_network()
print(type(network), network.keys())
```

```
<class 'dict'> dict_keys(['b2', 'W1', 'b1', 'W2', 'W3', 'b3'])
```

```python
network['W1'].shape, network['W2'].shape, network['W3'].shape
```

```
((784, 50), (50, 100), (100, 10))
```

```python
network['b1'].shape, network['b2'].shape, network['b3'].shape
```

```
((50,), (100,), (10,))
```

- 입력 이미지 한장이 신경망을 통과하는 과정(전방향 연산, 예측)

```python
Image('./deep_learning_images/fig 3-26.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353498-bc7e310b-0339-42c7-8ec8-732a11cce24f.png)


```python
def predict(network, X):
    W1, W2, W3 = network['W1'], network['W2'], network['W3']
    B1, B2, B3 = network['b1'], network['b2'], network['b3']

    A1 = np.dot(X, W1) + B1  # (50, )
    Z1 = sigmoid(A1)         # (50, )
    A2 = np.dot(Z1, W2) + B2 # (100, )
    Z2 = sigmoid(A2)         # (100, )
    A3 = np.dot(Z2, W3) + B3 # (10, )
    Y = softmax(A3)          # (10, )

    return Y
```

```python
X_test[1000].shape
```

```
(784,)
```

```python
y = predict(network, X_test[1000])
y
```

```
array([5.0377946e-07, 5.8335485e-04, 1.8732329e-05, 1.6465841e-02,
       4.6309014e-03, 3.3431701e-04, 1.1879358e-06, 7.5529285e-02,
       5.5383303e-04, 9.0188205e-01], dtype=float32)
```

```python
correct_cnt = 0
for i, test_img in enumerate(X_test):  # 10000 iterations
    prob = predict(network, test_img)
    pred = np.argmax(prob)
    if pred == y_test[i]:
        correct_cnt += 1

Accuracy = correct_cnt / len(y_test)        
print('Accuracy:', Accuracy)
```

```
Accuracy: 0.9352
```

- image 배치 입력에 대한 신경망 예측 과정

```python
Image('./deep_learning_images/fig 3-27.png', width=400)
```

![image](https://user-images.githubusercontent.com/84713532/209353526-f3a68416-2aac-4e1e-9793-b6a2f3beeb25.png)


```python
batch_size = 100
correct_cnt = 0

for i in range(0, len(X_test), batch_size):  # 10000 iterations
    test_img_batch = X_test[i:i + batch_size] # 100개씩 슬라이싱 (0 ~ 99, 100 ~ 199, ...)   
    prob_batch = predict(network, test_img_batch)
    pred_batch = np.argmax(prob_batch, axis = 1)
    correct_cnt += np.sum(pred_batch == y_test[i:i + batch_size])

Accuracy = correct_cnt / len(y_test)        
print('Accuracy:', Accuracy)
```

```
Accuracy: 0.9352
```
# 신경망 학습

```python
import numpy as np
import matplotlib.pyplot as plt
```

## 오차제곱합

```python
from IPython.display import Image
Image('./deep_learning_images/e 4.1.png', width=200)
```

![image](https://user-images.githubusercontent.com/84713532/209353783-9b8e9298-7494-4c25-a352-8501824f4c05.png)


## 교차 엔트로피

```python
Image('./deep_learning_images/e 4.2.png', width=200)
```

![image](https://user-images.githubusercontent.com/84713532/209353807-71ff29bd-b591-413b-b3b3-b9b3ecbbb1a1.png)


```python
def cross_entropy_error(y, t):
    delta = 1e-7 # 0.0000001
    return -np.sum(t * np.log(y + delta))
```

```python
t = [0, 0, 1, 0, 0, 0, 0, 0, 0, 0]  # 정답: 2 (one-hot encoding)
y = [0.1, 0.05, 0.6, 0.0, 0.05, 0.1, 0.0, 0.1, 0.0, 0.0]  # 예측: 2에 60%의 확률로 예측
cross_entropy_error(np.array(y), np.array(t))
```

```
0.510825457099338
```

```python
t = [0, 0, 1, 0, 0, 0, 0, 0, 0, 0]  # 정답: 2 (one-hot encoding)
y = [0.1, 0.05, 0.1, 0.0, 0.05, 0.1, 0.0, 0.6, 0.0, 0.0]  # 예측: 2에 60%의 확률로 예측
cross_entropy_error(np.array(y), np.array(t))
```

```
2.302584092994546
```

**예측을 잘못할수록 cross entropy의 값이 커지는 것을 알 수 있다.**

```python
Image('./deep_learning_images/e 4.3.png', width=200)
```

![image](https://user-images.githubusercontent.com/84713532/209353887-5a69fe68-51a8-46de-a0cf-079d7010a709.png)


```python
# 배치용 크로스 엔트로피 함수

def cross_entropy_error(y, t):
    delta = 1e-7 # 0.0000001

    if y.ndim == 1:  # 배치 단위가 아니라 1차원으로 입력되었을 경우
        t = t.reshape(1, t.size)
        y = y.reshape(1, y.size)

    batch_size = y.shape[0]

    return -np.sum(t * np.log(y + delta)) / batch_size
```

```python
cross_entropy_error(np.array(y), np.array(t))
```

```
2.302584092994546
```

## 미분

```python
Image('./deep_learning_images/e 4.5.png', width=200)
```

![image](https://user-images.githubusercontent.com/84713532/209353922-8e9e8877-2cd3-4109-9aa0-464586effb80.png)


```python
def function_1(x):
    return 0.01 * x ** 2 + 0.1 * x
```

```python
x = np.arange(0.0, 20.0, 0.1)
y = function_1(x)

plt.xlabel('x')
plt.ylabel('f(x)')
plt.plot(x, y)
```

```
[<matplotlib.lines.Line2D at 0x21474368fa0>]
```

![image](https://user-images.githubusercontent.com/84713532/209353872-33a09597-36fd-4cd2-b771-f5123e2001ac.png)

```python
# 중앙차분에 의한 수치미분
def numerical_diff(f, x):
    h = 1e-4  # 0.0001
    return (f(x + h) - f(x - h)) / 2 * h
```

```python
numerical_diff(function_1, 5)
```

```
1.9999999999908982e-09
```

## 편미분

```python
Image('./deep_learning_images/e 4.6.png', width=200)
```

![image](https://user-images.githubusercontent.com/84713532/209353982-4d8df376-2f16-4a1e-98b8-b18f2e527f09.png)


```python
def function_2(x):
    return x[0] ** 2 + x[1] ** 2
```

```python
# 그레디언트 (편미분 벡터)
def numerical_gradient(f, x):
    h = 1e-4 # 0.0001
    grads = np.zeros_like(x)

    for idx in range(x.size):   # x[0], x[1], ....
        tmp_val = x[idx]

        x[idx] = tmp_val + h
        fxh1 = f(x)   # f(x+h)
        x[idx] = tmp_val - h
        fxh2 = f(x)   # f(x-h)

        grads[idx] = (fxh1 - fxh2) / (2*h)

        x[idx] = tmp_val

    return grads
```

```python
numerical_gradient(function_2, np.array([3.0, 4.0]))
```

```
array([6., 8.])
```

## 경사하강법

```python
Image('./deep_learning_images/e 4.7.png', width=150)
```

![image](https://user-images.githubusercontent.com/84713532/209354007-93039331-fcfa-4634-b2e6-6bd8d5d26e1f.png)


```python
def gradient_descent(f, init_x, lr=0.01, step_num=100):
    x = init_x
    for i in range(step_num):
        grad = numerical_gradient(f, x)  # gradient
        x = x - (lr * grad)

    return x
```

```python
# init_x: 초기 랜덤한 weight vector (W1, W2, ...)
# function_2: loss function (손실함수)
# gradient_descent: weight의 기울기(미분)를 단서로 loss의 최솟값을 찾아가는 과정 (경사 하강법)
```

```python
init_x = np.array([-1.0, 4.0])  # 랜덤하게 시작
gradient_descent(function_2, init_x, lr=0.1, step_num=100)
```

```
array([-2.03703598e-10,  8.14814391e-10])
```

## 신경망에서의 기울기

- (참고) np.nditer 사용법

```python
import numpy as np
x=np.array([[1,2,3],[4,5,6]])
it=np.nditer(x,flags=['multi_index'],op_flags=['readwrite'])
while not it.finished:
    print(it.multi_index) #(0,0),(0,1),(0,2),(1,0),(1,1),(1,2)
    print(x[it.multi_index]) # 1,2,3,4,5,6
    it.iternext()
```

```
(0, 0)
1
(0, 1)
2
(0, 2)
3
(1, 0)
4
(1, 1)
5
(1, 2)
6
```

```python
# 신경망에서 사용할 W(Matrix 형태)의 편미분 행렬을 구하는 함수
# 그레디언트 (편미분 벡터)

def numerical_gradient(f, x):
    h = 1e-4 # 0.0001
    grads = np.zeros_like(x)

    it = np.nditer(x, flags=["multi_index"], op_flags=["readwrite"])

    while not it.finished:
        idx = it.multi_index
        tmp_val = x[idx]

        x[idx] = tmp_val + h
        fxh1 = f(x) # f(x+h)
        x[idx] = tmp_val - h
        fxh2 = f(x) # f(x-h)

        grads[idx] = (fxh1 - fxh2) / (2*h)
        x[idx] = tmp_val
        it.iternext()

    return grads
```

```python
def softmax(a):
    c = np.max(a)
    exp_a = np.exp(a - c)
    sum_exp_a = np.sum(exp_a)
    y = exp_a / sum_exp_a

    return y
```

```python
class simpleNet:
    def __init__(self):
        self.W = np.random.randn(2, 3)  # 정규분포로 초기화

    def predict(self, x):
        return np.dot(x, self.W)

    def loss(self, x, t):
        z = self.predict(x)
        y = softmax(z)
        loss = cross_entropy_error(y, t)
        return loss
```

```python
x = np.array([0.6, 0.9])  # (2, )
t = np.array([0, 0, 1])  # (3, )

net = simpleNet()
f = lambda w: net.loss(x, t)  # f: Loss function

dW = numerical_gradient(f, net.W)
```

```python
dW # net.W를 미분한 기울기 벡터
```

```
array([[ 0.11412845,  0.15547512, -0.26960357],
       [ 0.17119268,  0.23321268, -0.40440535]])
```
# 신경망 학습

```python
import numpy as np
from dataset.mnist import load_mnist
```

## Helper functions

```python
# 손실함수 (Cross Entropy)
def cross_entropy_error(y, t):
    delta = 1e-7 # 0.0000001

    if y.ndim == 1:
        t = t.reshape(1, t.size) 
        y = y.reshape(1, y.size)

    batch_size = y.shape[0]
    return -np.sum(t*np.log(y+delta))/batch_size
```

```python
# 신경망에서 사용할 W(Matrix 형태)의 편미분 행렬을 구하는 함수
# 신경망의 기울기 : 그레디언트 (편미분 벡터)
def numerical_gradient(f, x): # x의 shape이 (784, 20) => grads 도 (784, 20)
    h = 1e-4 # 0.0001
    grads = np.zeros_like(x)

    it = np.nditer(x, flags=["multi_index"], op_flags=["readwrite"])

    while not it.finished:
        idx = it.multi_index
        tmp_val = x[idx]

        x[idx] = tmp_val + h
        fxh1 = f(x) # f(x+h)
        x[idx] = tmp_val - h
        fxh2 = f(x) # f(x-h)

        grads[idx] = (fxh1 - fxh2) / (2*h)
        x[idx] = tmp_val
        it.iternext()

    return grads
```

```python
# Softmax
def softmax(x):
    if x.ndim == 2:
        x = x.T # 10*100
        x = x - np.max(x, axis=0) # 10*100 - 100 = 10*100
        y = np.exp(x) / np.sum(np.exp(x), axis=0)
        return y.T 

    x = x - np.max(x) # 오버플로 대책
    return np.exp(x) / np.sum(np.exp(x))
```

```python
# Sigmoid
def sigmoid(x):
    return 1/(1+np.exp(-x))
```

## 2층 신경망 구현하기

```python
class TwoLayerNet:
    def __init__(self, input_size, hidden_size, output_size, weight_init_std=0.01):
        # 모델 파라미터 초기화
        self.params = {}
        self.params['W1'] = weight_init_std * np.random.randn(input_size, hidden_size)  # (784, 20)
        self.params['b1'] = np.zeros(hidden_size)       # (20, )
        self.params['W2'] = weight_init_std * np.random.randn(hidden_size, output_size)   # (20, 10)
        self.params['b2'] = np.zeros(output_size)       # (10, )

    def predict(self, x):
        W1, W2 = self.params['W1'], self.params['W2']
        b1, b2 = self.params['b1'], self.params['b2'],

        a1 = np.dot(x, W1) + b1     # (20, )
        z1 = sigmoid(a1)            # (20, )
        a2 = np.dot(z1, W2) + b2    # (10, )
        z2 = softmax(a2)            # (10, )
        return z2

    def loss(self, x, t):
        y = self.predict(x)
        loss = cross_entropy_error(y, t)
        return loss

    def numerical_gradient(self, x, t):
        f = lambda w: self.loss(x, t)

        grads = {}
        grads['W1'] = numerical_gradient(f, self.params['W1'])  # W1 (784, 20) --> dW1 (784, 20)
        grads['b1'] = numerical_gradient(f, self.params['b1'])  # b1 (20, ) --> db1 (20, )
        grads['W2'] = numerical_gradient(f, self.params['W2'])  # W2 (20, 10) --> dW2 (20, 10)
        grads['b2'] = numerical_gradient(f, self.params['b2'])  # b2 (10, ) --> db2 (10, )
        return grads

    def accuracy(self, ):
        pass
```

```python
(X_train, y_train), (X_test, y_test) = load_mnist(normalize=True, flatten=True, one_hot_label=True)
```

```python
network = TwoLayerNet(input_size = 784, hidden_size = 20, output_size = 10)
```

```python
# Hyper Parameter
iters_num = 1000
batch_size = 100 # mini batch size
learning_rate = 0.1

for i in range(iters_num):
    batch_mask = np.random.choice(60000, 100)
    x_batch = X_train[batch_mask]
    t_batch = y_train[batch_mask]

    # 1. Gradient
    grads = network.numerical_gradient(x_batch, t_batch)

    # 2. Gradient Descent (모델 파라미터 업데이트)
    for keys in ('W1', 'W2', 'b1', 'b2'):
        # W(new) <-- W(old) - (lr * Gradient): 경사 하강법
        network.params[keys] = network.params[keys] - (learning_rate * grads[keys])

    loss = network.loss(x_batch, t_batch)
    print(loss)
```

```
2.296413519548535
2.2936651002506836
2.2955634302552044
2.3003798146752774
2.2997176647342554
2.2980852157645786
2.299867600372201
2.298694935196747
2.300851053396086
2.295233290173953
2.293713768597055
2.2939479259830806
2.3006807613831977
2.302486272539229
2.3020922663609493
2.2959038907496665
2.3065646486137372
2.291779590204008
2.289093952268112
2.3021323362250428
2.3010013309517627
2.2984018751230577
2.295466993230261
2.294979989588273
2.300845718496004
2.3039543119730603
2.2974380667915155
2.299113708435143
2.2976091534388443
2.291842072306648
2.302750364124344
2.301833745149696
2.2916067057803318
2.296609789685288
2.3005388500407835
.
.
.
0.619284901240910
```
