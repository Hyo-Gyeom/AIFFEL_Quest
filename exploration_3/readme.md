# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 신유진


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 코드에 각 주석이 task별로 쪼개져 있어서 잘 이해가 감
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 없는 거 같음
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 넵, 주석이 잘 기록되어 있고, 코드의 전체적인 flow와 노드에서 언급되어있는 최종 보고 부분까지 잘 정리되어있다. 
- [X] 코드가 간결한가요?
  > 함수단위로 있어서 간결

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 다음과 같이 함수 2개가 있고 각 함수의 구동과정에 대해 설명이 되어이있어서 알아보기 쉬웠음.
def cat_sticker(landmark, img):
    """
    입력받은 이미지에 고양이 수염 부착
    :param img: img
    :return: 부착된 이미지 반환
    """
    # 스티커 부착지점 x,y와 넓이 높이w, h
    # 이미지가 깨지지 않게 w와 h를 같게 설정
    # 코볼 중심사이의 4배로 설정
    w = h = (landmark[5][0] - landmark[1][0]) * 4
    x, y = landmark[0][0] - int(w // 2), landmark[0][1] - int(h // 2)
    
    # 랜드마크의 코 밑 부분을 기준으로 각도구하기
    rad = math.atan2(abs(landmark[5][1] - landmark[1][1]), abs(landmark[5][0] - landmark[0][1]))
    angle = 360 - ((rad * 180) / math.pi)
    print(landmark[5][1] - landmark[1][1])
    if landmark[5][1] - landmark[1][1] > 0:
        angle = -angle
    
    print (x, y, w, h)
    
    # 고양이 수염 이미지 준비
    sticker_path = 'cat.png'
    img_sticker = cv2.imread(sticker_path)
    img_sticker = cv2.resize(img_sticker, (w,h))
    
    # 수염 회전시 주변에 생기는 검정 이미지 부분을 반전 시켜 검정 부분을 나미지 배경 부분가 합하고
    # 각도 조절 후 다시 반전하여 주변에 생기는 검은 이미지를 삭제
    img_sticker = np.invert(img_sticker)
    M = cv2.getRotationMatrix2D((w // 2, h // 2), -angle, 1.0)   # rotation 할때 좌표값 조정
    img_sticker = cv2.warpAffine(img_sticker, M, (w, h))
    img_sticker = np.invert(img_sticker)
    
    sticker_area = img[y:y+img_sticker.shape[0], x:x+img_sticker.shape[1]]
    img[y:y +img_sticker.shape[0], x:x+img_sticker.shape[1]] = \
        np.where(img_sticker==255, sticker_area,img_sticker).astype(np.uint8)
    
    return cv2.cvtColor(img, cv2.COLOR_BGR2RGB)



def cat_sticker(landmark, img):
    """
    입력받은 이미지에 고양이 수염 부착
    :param img: img
    :return: 부착된 이미지 반환
    """
    # 스티커 부착지점 x,y와 넓이 높이w, h
    # 이미지가 깨지지 않게 w와 h를 같게 설정
    # 코볼 중심사이의 4배로 설정
    w = h = (landmark[5][0] - landmark[1][0]) * 4   # 4배인 이유는 비율이 잘나옴
    x, y = landmark[0][0] - int(w // 2), landmark[0][1] - int(h // 2)
    
    # 랜드마크의 코 밑 부분을 기준으로 각도구하기
    rad = math.atan2(abs(landmark[5][1] - landmark[1][1]), abs(landmark[5][0] - landmark[0][1]))
    angle = 360 - ((rad * 180) / math.pi)
    print(landmark[5][1] - landmark[1][1])
    if landmark[5][1] - landmark[1][1] > 0:
        angle = -angle
    
    print (x, y, w, h)
    
    # 고양이 수염 이미지 준비
    sticker_path = 'cat.png'
    img_sticker = cv2.imread(sticker_path)
    img_sticker = cv2.resize(img_sticker, (w,h))
    
    # 수염 회전시 주변에 생기는 검정 이미지 부분을 반전 시켜 검정 부분을 나미지 배경 부분가 합하고
    # 각도 조절 후 다시 반전하여 주변에 생기는 검은 이미지를 삭제
    img_sticker = np.invert(img_sticker)
    M = cv2.getRotationMatrix2D((w // 2, h // 2), -angle, 1.0)
    img_sticker = cv2.warpAffine(img_sticker, M, (w, h))
    img_sticker = np.invert(img_sticker)
    
    sticker_area = img[y:y+img_sticker.shape[0], x:x+img_sticker.shape[1]]
    img[y:y +img_sticker.shape[0], x:x+img_sticker.shape[1]] = \
        np.where(img_sticker==255, sticker_area,img_sticker).astype(np.uint8)
    
    return cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

# 참고 링크 및 코드 개선
```python
# https://seongonion.tistory.com/113 (효겸님꼐서 필요하신지 모르겠지만 꽤 괜찮은거 같아요)
# 제가 (감히) 손볼 곳이 없습니다...!
```
