# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 손정민


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 3가지 모델을 사용하였고 성공적으로 훈련시켰다. Loss에 대한 시각화가 잘 이루어졌고 word2vec 임베딩을 활용하여 기존 모델의 성능을 개선시켰다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 과정이 어떤 역할을 수행했는지 주석으로 설명이 되어 있었고 마크다운으로 프로젝트 목표와 설계 과정을 정리, 기록하여 이해하기 쉬웠다.
  ```python
  # word2ver를 이용하여 학습
  from gensim.models import Word2Vec
  from tensorflow.keras.initializers import Constant

  # sg = 0은 CBOW, 1은 Skip-gram.
  word2vec = Word2Vec(token_word_list, vector_size=100, window=2, min_count=5, workers=4, sg=1)
  word2vec.wv.vectors.shape
  ```
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 실행되었다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 세 개의 모델을 잘 사용하였고, 학습 과정에서 epochs를 수정하는 등의 시도를 한 것, 주석의 내용으로 보아 모델링을 이해하고 프로젝트를 수행한 것으로 보인다.
- [X] 코드가 간결한가요?
  > 코드 사이에 공백이 적절하게 들어가 있었고 변수명 또한 직관적으로 알아볼 수 있게 작성했다. 많은 argument가 있는 fit()같은 경우 괄호 내부 인자 간 개행이 되어있어 가독성이 좋았다.
  ```python
  history = model.fit(X_train,
                    y_train,
                    epochs=epochs,
                    batch_size=256,
                    validation_data=(X_val, y_val),
                    verbose=1)
  ```

# 참고 링크 및 코드 개선
```python
num_tokens = [len(tokens) for tokens in X]
num_tokens = np.array(num_tokens)
# 문장길이의 평균값, 최대값, 표준편차를 계산해 본다. 
print('문장길이 평균 : ', np.mean(num_tokens))
print('문장길이 최대 : ', np.max(num_tokens))
print('문장길이 표준편차 : ', np.std(num_tokens))

# 예를들어, 최대 길이를 (평균 + 2*표준편차)로 한다면,  
max_tokens = int(np.mean(num_tokens) + 2 * np.std(num_tokens))
max_len = int(max_tokens)
print(f'전체 문장의 {np.sum(num_tokens < max_tokens) / len(num_tokens)}%')
```
  데이터 가공 단계에서 평균, 최대, 표준편차를 파악할 때 단순히 계산 결과를 숫자로 확인해 데이터의 분포를 파악하는 것도 충분하지만, 시각화가 추가되면 데이터 분포를 더 쉽게 이해하는 것에 도움이 될 것 같습니다.

```python
plt.hist([len(token) for token in X], bins=50)
plt.show()
```