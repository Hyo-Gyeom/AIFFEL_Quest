# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 신유진

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 넵
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 넵, 주석정리가 잘 되어 있어 직관적이고 보기 쉽습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 없습니다. 코드 한 블록안에도 주석이 잘 정리되어 있어 코드에 에러는 없어 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 넵, 코드 한 블록안에도 주석이 잘 정리되어 있어 코드를 이해하고 작성하신 걸로 보입니다. 
- [X] 코드가 간결한가요?
  > 넵, 간결하고 직관적입니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 모델을 함수로 작성
def sequential_model(vocab_size, max_len=40):
    model = tf.keras.Sequential()
    # model.add(tf.keras.layers.LSTM(8, input_shape=(max_len, 1), return_sequences=True))
    model.add(tf.keras.layers.Embedding(vocab_size, 1, input_shape=(max_len,)))
    model.add(tf.keras.layers.LSTM(8))
    model.add(tf.keras.layers.Dense(8, activation='relu'))
    model.add(tf.keras.layers.Dense(1, activation='sigmoid'))
    
    model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
    
    return model


모델을 함수로 작성한 이 부분이 자동화가 깔끔이 잘 되어있어서 객체 지향적이었고 사용하기 좋았다.
```

# 참고 링크 및 코드 개선
```python
# 없는 것으로 보입니다. 
```
