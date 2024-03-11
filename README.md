# Various_Computer_Visions
My various video recoder using OpenCV

## 1. Camera Video Recorder

import cv2

### 카메라 영상을 받아오기 위한 객체 생성
cap = cv2.VideoCapture(0)  # 내장 카메라를 사용하려면 인자를 0으로 설정

### 동영상 파일을 저장하기 위한 설정
frame_width = int(cap.get(3))
frame_height = int(cap.get(4))
out = cv2.VideoWriter('Recorded.avi', cv2.VideoWriter_fourcc(*'XVID'), 20.0, (frame_width, frame_height))

### 초기 모드 설정
mode = "Preview"
font = cv2.FONT_HERSHEY_SIMPLEX

### 코덱과 FPS 설정
codec = cv2.VideoWriter_fourcc(*'XVID')
fps = 20.0
while True:

### 카메라에서 프레임을 읽어옴
ret, frame = cap.read()

### Record 모드 시 화면에 빨간색 원 표시
if mode == "Record":
cv2.circle(frame, (50, 50), 30, (0, 0, 255), -1)

### 프레임을 출력
if mode == "Preview":
cv2.imshow('Preview', frame)
elif mode == "Record":
cv2.putText(frame, 'Recording...', (10, 50), font, 1, (0, 0, 255), 2, cv2.LINE_AA)
cv2.imshow('Recording', frame)
out.write(frame)

### 키 이벤트 처리
key = cv2.waitKey(1)
if key == 27:  # ESC 키를 누르면 종료
break
elif key == ord(' '):  # 스페이스 키를 누르면 모드 변경
mode = "Record" if mode == "Preview" else "Preview"

### 사용한 자원 해제
cap.release()
out.release()
cv2.destroyAllWindows()

### [Running Screenshot]

![image](https://github.com/kohjun/Various_Computer_Visions/assets/82298792/ea8f6a67-c74b-4782-a9d2-e108b1eb0dff)

*빨간색 원 + Recording을 통해 녹화중임을 표시*
