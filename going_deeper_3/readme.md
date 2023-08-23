# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  네, 정상적으로 동작하여 문제를 해결한 것으로 보입니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 전체적인 코드를 이해하는 데에 도움이 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러없이 동작하는 것으로 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 작성된 코드와 결과를 보니, 전반적인 이해를 바탕으로 코드를 작성하신 것 같습니다.
- [X] 코드가 간결한가요?
  > 네, 간결합니다.

# 예시
- 주석이 적혀있어 코드 이해에 도움이 되었습니다.
```python
X = np.array([model.wv[word] for word in attributes[0]])
Y = np.array([model.wv[word] for word in attributes[1]])

for i in range(len(genre_name)-1):
    # i + 1로 이미 계산된 값은 하지 않음 - 좌하단이 0
    for j in range(i + 1, len(genre_name)):
        A = np.array([model.wv[word] for word in attributes[i]])
        B = np.array([model.wv[word] for word in attributes[j]])
        matrix[i][j] = weat_score(X, Y, A, B)
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
