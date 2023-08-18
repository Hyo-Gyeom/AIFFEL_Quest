# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 양주영


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 에러 없이 결과가 잘 도출되었습니다. 
  ![정상 작동](https://github.com/Hyo-Gyeom/AIFFEL_Quest/assets/134067511/31f11542-d9c0-4d19-ad71-efb462f1e0ba)
- [ ] 주석을 보고 작성자의 코드가 이해되었나요?
  >함수를 정의하면서 주석을 달아 이해에 도움되었습니다. 
  ![주석 이해](https://github.com/Hyo-Gyeom/AIFFEL_Quest/assets/134067511/38537378-be92-4043-bd33-ee26eac1888a)
- [ ] 코드가 에러를 유발할 가능성이 없나요?
  >한 번에 묶어 불필요한 반복이 없어 에러를 유발을 방지하였습니다. 
  ![코드 간결](https://github.com/Hyo-Gyeom/AIFFEL_Quest/assets/134067511/c814a893-72ad-485a-850d-7cfda0b6c2a9)
- [ ] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  >코더가 원하는 대로 여러 모델을 묶어서 코드를 작성했습니다. 
  ![코드 이해](https://github.com/Hyo-Gyeom/AIFFEL_Quest/assets/134067511/f77ba076-347f-4589-be06-3b6b36725807)
- [ ] 코드가 간결한가요?
  >불필요한 코드 반복을 없앨 수 있도록 하였습니다. 
  ![코드 간결](https://github.com/Hyo-Gyeom/AIFFEL_Quest/assets/134067511/451f3187-fccf-4fc7-a790-bac3470b7972)

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 사칙 연산 계산기
class calculator:
    # 예) init의 역할과 각 매서드의 의미를 서술
    def __init__(self, first, second):
        self.first = first
        self.second = second
    
    # 예) 덧셈과 연산 작동 방식에 대한 서술
    def add(self):
        result = self.first + self.second
        return result

a = float(input('첫번째 값을 입력하세요.')) 
b = float(input('두번째 값을 입력하세요.')) 
c = calculator(a, b)
print('덧셈', c.add()) 
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
