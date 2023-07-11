# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 없으나, 코드가 간결해서 주석 없이도 코드 이해에는 문제가 없었습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 모두 다 정상적으로 작동합니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 코드에 대한 충분한 이해를 가지고 작성한 것으로 보입니다.
- [O] 코드가 간결한가요?
  > 간결하고 명료합니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 데이터 가져오기
from sklearn.datasets import load_diabetes
from sklearn.model_selection import train_test_split
import numpy as np

diabetes = load_diabetes()

#모델에 입력할 데이터, 예측할 데이터
df_x = diabetes.data
df_y = diabetes.target

#data 특성의 개수 f
f = len(df_x[1])
    
#train 데이터와 test 데이터 분리
X_train, X_test, y_train, y_test = train_test_split(df_x, df_y, test_size=0.2, random_state=42)

#가중치 W와 b
W = np.random.rand(f)
b = np.random.rand()

#모델 구현
def model(x_data, weight, bias):
    predictions = 0
    for i in range(f):
        predictions += x_data[:, i] * weight[i]
    predictions += bias
    return predictions

#손실함수 정의
def loss(x_data, weight, bias, y_data):
    predictions = model(x_data, weight, bias)
    return ((predictions - y_data) ** 2).mean()

#gradient 함수 구현
def gradient(x_data, weight, bias, y_data):
    y_pred = model(x_data, weight, bias)
    dW = (1 / len(y_data)) * 2 * x_data.T.dot(y_pred - y_data)
    db = 2 * (y_pred - y_data).mean()
    return dW, db

#하이퍼파라미터(learning rate) 설정
LEARNING_RATE = 0.1

losses = []
epoch = 10000
for i in range(1, epoch + 1):
    dW, db = gradient(X_train, W, b, y_train)
    W -= LEARNING_RATE * dW
    b -= LEARNING_RATE * db
    L = loss(X_train, W, b, y_train)
    losses.append(L)
    if i % 1000 == 0:
        print('Iteration %d : Loss %0.4f' % (i, L))

#성능 확인
prediction = model(X_test, W, b)
mse = loss(X_test, W, b, y_test)
mse

#데이터 시각화
import matplotlib.pyplot as plt

plt.scatter(X_test[:, 0], y_test)
plt.scatter(X_test[:, 0], prediction)
plt.show()
```

# 참고 링크 및 코드 개선
```python
# 노드 2-1.(2),(3) : df_X, df_y 값 numpy array로 변환하기
import numpy as np
X = np.array(df_X)
y = np.array(df_y)
