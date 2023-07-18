# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 박혜원


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [△] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  - 전부다 진행해주신 것으로 알고 있는데, 파일 문제로 뒤에 부분이 날라가서 추상적 요약 모델 학습, 평가, 추출적 요약 모델 학습 및 평가 부분은 확인하기 어려웠습니다. 
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 마크다운으로 각 스텝 및 상세 과정들에 대한 설명을 추가해주셨고, 주석도 잘 작성해주셨습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 작성해주신 부분까지는 에러가 없었습니다.
    중간에 Output 으로 뜬 Attribute Error 는 코드 상의 문제가 아니라 잘못된 실행으로 오류가 난 것으로 확인되었습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네 상세한 주석을 통해 제대로 이해하고 작성하신 부분이 보였습니다. 
- [O] 코드가 간결한가요?
  > 네 함수등을 활용하여 간결한 코드를 작성해주셨습니다. 

# 제안
- 확인되는 코드까지는 저 또한 유사한 형태로 접근하였기때문에 크게 개선하거나 수정하고 싶은 부분은 없었습니다.
- 그래도 굳이 제안하자면 아래 코드 상에서 6회 이하인 단어들을 제외하셨는데,조금 더 값을 크게 잡아도 될 것 같습니다. 
(가령, 등장 빈도가 threshold 값인 7회 이하인 단어들은 단어 집합에서 약 70% 를 차지하고, 실제로 훈련 데이터에서 등장 빈도로 차지하는 비중은 상대적으로 적은 수치인 3.89% 밖에 되지 않습니다.)

```python
threshold = 7 # --> 값을 좀 더 크게 잡아도 좋을 것 같음 
total_cnt = len(src_tokenizer.word_index) # 단어의 수
rare_cnt = 0 # 등장 빈도수가 threshold보다 작은 단어의 개수를 카운트
total_freq = 0 # 훈련 데이터의 전체 단어 빈도수 총 합
rare_freq = 0 # 등장 빈도수가 threshold보다 작은 단어의 등장 빈도수의 총 합

# 단어와 빈도수의 쌍(pair)을 key와 value로 받는다.
for key, value in src_tokenizer.word_counts.items():
    total_freq = total_freq + value

    # 단어의 등장 빈도수가 threshold보다 작으면
    if(value < threshold):
        rare_cnt = rare_cnt + 1
        rare_freq = rare_freq + value

print('단어 집합(vocabulary)의 크기 :', total_cnt)
print('등장 빈도가 %s번 이하인 희귀 단어의 수: %s'%(threshold - 1, rare_cnt))
print('단어 집합에서 희귀 단어를 제외시킬 경우의 단어 집합의 크기 %s'%(total_cnt - rare_cnt))
print("단어 집합에서 희귀 단어의 비율:", (rare_cnt / total_cnt)*100)
print("전체 등장 빈도에서 희귀 단어 등장 빈도 비율:", (rare_freq / total_freq)*100)
```
