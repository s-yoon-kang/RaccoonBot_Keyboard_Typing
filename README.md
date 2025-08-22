# [Keyboard Typing]

**해당 문서는 Raccoon의 테스트 예제 설명 문서입니다.**

***

RaccoonBot이 입력된 문장을 직접 키보드로 반복 타이핑하는 예제입니다.
<br>
예제에는 **잘못된 입력 감지**, **대/소문자 감지**, **키 입력 감지/재시도** 기능이 있습니다.
<br>

[작동영상]

<br><br>

#### [하드웨어 설명](https://github.com/RoboidStudioLAB/Wiki_Image/wiki/%EB%9D%BC%EC%BF%A4-%ED%95%98%EB%93%9C%EC%9B%A8%EC%96%B4-%EC%84%A4%EB%AA%85)
  
#### [로보메이션 깃허브 바로가기](https://github.com/RobomationLAB)

#### [초보자를 위한 파이썬 설치 가이드](https://github.com/RobomationLAB/Hamster-S_API_KR/wiki/%EC%B4%88%EB%B3%B4%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%84%A4%EC%B9%98-%EA%B0%80%EC%9D%B4%EB%93%9C)

<br><br>


---


## 1. 준비물

[*예제 파일 다운로드*](링크)

| 제품명(수량) | 이미지 | 제품명(수량) | 이미지 |
| :---: | :---: | :---: | :---: |
| Raccoon<br> (1개) | <img width="200" alt="Image" src="https://github.com/user-attachments/assets/6aed75da-3092-4295-9ef7-e8956efa5bae" /> | 키보드용 말단 장치<br> (1개) | <img width="50" alt="Image" src="https://github.com/user-attachments/assets/4c2f9d5a-0253-4ff0-b5cf-58f43507cfec" /> |
| 미니 키보드<br> (1개) | <img width="200" alt="Image" src="https://github.com/user-attachments/assets/d03b4532-8ac9-4c96-a1a5-9764d744256b" /> | Python | <img width="200" alt="Image" src="https://github.com/user-attachments/assets/62366b02-9b80-41fc-951b-b54c51f5814b" /> |

<br><br>


---


## 2. 초기 환경 구성
- Raccoon과 키보드를 **5cm** 간격을 두고 중앙을 맞춰 **마주보게** 배치해주세요.

  <img width="500" alt="Image" src="https://github.com/user-attachments/assets/6e493534-edd2-477e-9397-18614ac4790a" />

<br><br>

- **Joint 4**가 **수직**으로 키의 정중앙을 누를 수 있게 위치를 조절하며 **key_mapping** 함수를 수정합니다.

  <img width="500" alt="Image" src="https://github.com/user-attachments/assets/73220c2d-ced2-4b4c-8178-90f19193a4b0" />

<br><br>

- **key_mapping** 함수와 **RaccoonBot**의 **XYZ 좌표계**는 다음과 같습니다. (단위: cm)

  <img width="500" alt="Image" src="https://github.com/user-attachments/assets/12c8777d-20ad-4e7d-983b-cd4033817549" /> <img width="500" alt="Image" src="https://github.com/user-attachments/assets/02a18a92-bdf9-423a-80f0-47903d1bed77" />

<br><br>

- **Z축**의 경우 키보드를 완전히 누르는 좌표보다 **0.2cm 더 낮게** 설정합니다.

  <img width="500" alt="Image" src="https://github.com/user-attachments/assets/8f6145cb-52f2-431c-8cac-0dfb8f1fadff" />

<br><br>

- **1 ~ 0** | **a ~ z** | **,** | **.** | **Caps lock** | **Space** | **Enter**의 좌표를 모두 수정하고 문장 입력에 차례대로 입력하며 확인합니다.

  <img width="1500" alt="Image" src="https://github.com/user-attachments/assets/3a01331f-c1b0-402b-b966-d7c0ff4fa67c" />

<br><br>


---


## 3. 작동하기
- 블록 컴포저나 파이썬을 통해 작동하는 방법을 적는 란입니다.

<br><br>


---


## 4. 오류 발생시 해결 방법
- 발생 가능한 오류에 대해서 적어두는 란 입니다.

<br><br>


---


## 5. 작동 알고리즘
- 작동하는 알고리즘에 대해 소개하는 란 입니다.

<br><br>


---


## 6. 코드 설명
- 코드를 설명해주는 부분 입니다.

<br><br>


---


## 7. 관련 내용
- 내용에 사용된 이론에 대해서 소개하는 란 입니다.  
- 개별 문서로 링크 걸기


<br>

<img width="10000000" alt="Image" src="https://github.com/user-attachments/assets/aa6d40b2-2d90-4a5e-90b4-1e3049b714db" />

<br><br>
