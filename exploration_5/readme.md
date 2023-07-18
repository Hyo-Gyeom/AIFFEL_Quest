# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : [이태훈](https://github.com/git-ThLee)


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네! 이해가 필요한 코드에 주석을 꼼꼼히 작성했습니다!
  ```python
  # 이미지 확인
    if img_check:
        # 255와 0을 적당한 색상으로 바꿔봅니다
        color_mask = cv2.applyColorMap(img_mask, cv2.COLORMAP_JET)
        # 원본 이미지와 마스크를 6:4로 합치기 
        img_show = cv2.addWeighted(img_show, 0.6, color_mask, 0.4, 0.0)
        plt.imshow(cv2.cvtColor(img_show, cv2.COLOR_BGR2RGB))
        plt.show()
  ```
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 네! 코드를 함수로 만들어서 문제가 발생해도 금방 해결이 가능할 것 같습니다.
  ```python
  def person_mode(img_path, img_check=False):
    img = cv2.imread(img_path) 
    img_show = img.copy()
    segvalues, output = model.segmentAsPascalvoc(img_path)
    # ... 이하 생략
  ```
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네! 
  ```python
  # cv2.bitwise_and()을 사용하면 배경만 있는 영상을 얻을 수 있습니다.
    # 0과 어떤 수를 bitwise_and 연산을 해도 0이 되기 때문에 
    # 사람이 0인 경우에는 사람이 있던 모든 픽셀이 0이 됩니다.
    img_bg_blur = cv2.bitwise_and(img_orig_blur, img_bg_mask)
  ```
- [X] 코드가 간결한가요?
  > 네! 함수를 통해 반복되는 코드를 간소화했습니다!
  ```python
  for image_name in image_names:
    # 이미지 경로
    image_path = image_folder_path + '/' + image_name
    person_mode_image = person_mode(image_path)
    plt.imshow(cv2.cvtColor(person_mode_image, cv2.COLOR_BGR2RGB))
    plt.show()
  ```

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