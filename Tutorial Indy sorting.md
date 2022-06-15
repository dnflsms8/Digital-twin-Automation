## Main Contents: Pick and Place using QR code

이 프로젝트에서 구성한 우편 분류 공정에 대한 ROS 코드는 아래의 순서에 따라 작동하게 됩니다.

 - Flow Chart 삽입 요망

   <img src="C:\Users\이창현\AppData\Roaming\Typora\typora-user-images\image-20220615112623160.png" alt="image-20220615112623160" style="zoom:67%;" />

### 1. External Envirionment Setting

1. QR 코드 생성
   우편을 분류하기 위해, 먼저 QR 코드를 생성하는 과정이 필요합니다.
   QR 코드 생성에는, Python Module "qrcode" 를 활용했습니다.
   [이미지 첨부]

   <img src="C:\Users\이창현\AppData\Roaming\Typora\typora-user-images\image-20220615101103286.png" alt="image-20220615101103286" style="zoom:67%;" />

위와 같은 방법을 통해 QR코드 이미지를 만들고, 이를 인쇄한 뒤 편지 봉투에 붙였습니다.

2) 좌표 고정
   편지 봉투를 쌓아 둘 곳과, 분류할 곳의 좌표를 설정해야 합니다.
   **INDY-10 전용 태블릿**을 활용, '직접 교시' 모드를 통해 좌표를 취득하였습니다.
   그 과정은 다음과 같습니다
   1) INDY-10 전용 태블릿에서, 초보자 모드에서 직접교시 모드로 바꿔줍니다.

<img src="C:\Users\이창현\AppData\Roaming\Typora\typora-user-images\image-20220615110914164.png" alt="image-20220615110914164" style="zoom: 50%;" />

 	   2.  로봇을 원하는 위치로 움직여 좌표를 땁니다.		

<img src="C:\Users\이창현\AppData\Roaming\Typora\typora-user-images\image-20220615110525451.png" alt="image-20220615110525451" style="zoom:67%;" />




### 2. Internal Environment Setting

1) Install Anaconda

2) Install Python module
   - !apt install libzbar0
   - !pip install pyzbar
   - pip install numpy

### 3. Coding

1. qr_code_reader.py	

```python
###1###
import pyzbar.pyzbar as pyzbar
import cv2

cap = cv2.VideoCapture(0, cv2.CAP_DSHOW)  # Window에서 실행시킬 때
#cap = cv2.VideoCapture(0)                # Linux에서 실행시킬 때

location = str(0)   # location 위치 선언

###2###
while(cap.isOpened()):
  # 카메라로 매 프레임마다 이미지를 읽어드린다.
  ret, img = cap.read() 

  if not ret:
    continue
  
  # 이미지를 Gray scale로 변환시킨다.
  gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
  
  # Gray scale로 변환된 QR 이미지를 해독한다.
  decoded = pyzbar.decode(gray)

  for d in decoded: 
    x, y, w, h = d.rect

    # QR 코드의 타입과 데이터를 읽는다.
    barcode_data = d.data.decode("utf-8")
    barcode_type = d.type
    # QR 코드의 데이터를 location에 저장한다.
    location = barcode_data

    # QR 코드 부분에 사각형을 그린다.
    cv2.rectangle(img, (x, y), (x + w, y + h), (0, 0, 255), 2)

    # QR 코드의 타입과 데이터를 text에 저장한 뒤에 화면에 나타낸다.
    text = '%s (%s)' % (barcode_data, barcode_type)
    cv2.putText(img, text, (x, y), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 255), 2, cv2.LINE_AA)

  # 카메라로 매 프레임마다 읽고 있는 이미지를 'img' 윈도우로 보여준다.
  cv2.imshow('img', img)

  # location에 QR 코드 데이터가 저장되면 반복문에서 나간다.
  if location != str(0):
      break
  
  # 'q'를 누르게 되면 location에 종료 구문이 저장된 채로 반복문에서 나간다.
  key = cv2.waitKey(1)
  if key == ord('q'):
    location = 'quit'
    break

###3###
# 저장된 location을 print하여 qr_classify_robot.py에서 location을 읽을 수 있도록 한다.
print(location)

# 설정해놓은 카메라와 윈도우를 해제한다.
cap.release()
cv2.destroyAllWindows()
```

1. 필요한 모듈을 불러오고, 객체를 선언
2. 카메라 구동시, QR 값을 해독하고 location 변수에 필요한 값을 넣어준다
3. qr.classify_robot.py에서 location 변수를 사용할 수 있게끔 print해주고 설정을 해제한다
