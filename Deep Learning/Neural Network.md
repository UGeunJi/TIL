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
