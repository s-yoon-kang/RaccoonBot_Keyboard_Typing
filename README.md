# Keyboard Typing

해당 코드는 RaccoonBot이 입력된 문장을 직접 키보드로 반복 타이핑하는 예제입니다.

![라쿤 키보드]()

예제에는 **잘못된 입력 감지**, **대/소문자 감지**, **키 입력 감지/재시도** 기능이 있습니다.
<br>

아래 버튼을 눌러 파이썬 코드를 다운로드 받아 RaccoonBot의 동작을 확인해보세요.

<br><br><br>

#### [Raccoon_keyboard_Typing.py 다운로드]()
#### [시작하기에 앞서]()
#### [초보자를 위한 파이썬 설치 가이드](https://github.com/RobomationLAB/Hamster-S_API_KR/wiki/%EC%B4%88%EB%B3%B4%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%84%A4%EC%B9%98-%EA%B0%80%EC%9D%B4%EB%93%9C)
#### [하드웨어 설명]()



<br>

---

<br><br><br><br>


# 예제 설명
사용자가 코드에 반복 타이핑할 문장을 **영어**로 **["문장"]** 과 같이 입력합니다. 
<br>

<img width="569" height="165" alt="Image" src="https://github.com/user-attachments/assets/78056e0e-83d0-4392-a9c0-40b78b0fce89" />

<br><br>

여러 문장의 경우 다음과 같이 **["문장 1", "문장 2"]** 로 나눠서 작성합니다.
<br>

<img width="715" height="166" alt="Image" src="https://github.com/user-attachments/assets/237277ba-68a3-42e8-8a9b-6d395765a971" />

<br><br>

코드를 실행하면 라쿤이 타이핑 자세로 준비한 후 로그 출력과 함께 타이핑을 시작합니다.
<br>

<img width="534" height="127" alt="Image" src="https://github.com/user-attachments/assets/34250add-1295-4f03-a9b1-9cd1ad9e8a80" />

<br><br>

대/소문자는 **Caps Lock 토글**로 제어하여 입력합니다.
<br>

<img width="602" height="150" alt="Image" src="https://github.com/user-attachments/assets/73b41e4c-7390-4573-9e8a-c1aa441eb596" />

<br><br>

잘못된 키 입력을 실시간으로 감지하며 **오동작 시 해당 단어를 건너뛰고 Enter 후 다음 단어로 진행**합니다.
<br>

<img width="668" height="76" alt="Image" src="https://github.com/user-attachments/assets/589bf472-e314-411e-bfb2-37913c58b777" />

<br><br>

동작에 따른 소리는 다음과 같습니다.
<br>

- 타이핑을 할 준비가 되었다면 **BEEP** 소리
- 잘못된 키 입력시 **ENGINE** 소리
- 타이핑을 완료하면 **GOOD JOB** 소리



<br>

---

<br><br><br><br>


# 준비물 및 방법
### 하드웨어
- RaccoonBot
- 키보드용 말단 장치
- PC (Windows 권장)
- 키보드 (Coms 블루투스 키보드(미니) V3.0 또는 RaccoonBot이 모두 상호작용 가능한 크기)

### 소프트웨어
- Python 3.9+
- 패키지: `roboid`, `threading`, `keyboard`, `ctypes`, `time`

<br><br>
### 세팅
- RaccoonBot과 키보드를 **5cm** 간격을 두고 **마주보게** 배치해주세요.
<img width="500" height="500" alt="Image" src="https://github.com/user-attachments/assets/6e493534-edd2-477e-9397-18614ac4790a" />

<br><br>

- **Joint 4**가 **수직**으로 키보드를 누를 수 있게 위치를 조절하며 **key_mapping** 함수를 수정합니다.
<img width="500" height="400" alt="Image" src="https://github.com/user-attachments/assets/73220c2d-ced2-4b4c-8178-90f19193a4b0" />

<br><br>

- **key_mapping** 함수와 **RaccoonBot**의 **XYZ 좌표계**는 다음과 같습니다. (단위: cm)
<img width="500" height="500" alt="Image" src="https://github.com/user-attachments/assets/12c8777d-20ad-4e7d-983b-cd4033817549" /> <img width="472" height="219" alt="Image" src="https://github.com/user-attachments/assets/02a18a92-bdf9-423a-80f0-47903d1bed77" />

<br><br>

- **Z축**의 경우 키보드를 완전히 누르는 좌표보다 **0.2cm 더 낮게** 설정합니다.
<img width="764" height="218" alt="Image" src="https://github.com/user-attachments/assets/8f6145cb-52f2-431c-8cac-0dfb8f1fadff" />

<br><br>

- **1 ~ 0** | **a ~ z** | **,** | **.** | **Caps lock** | **Space** | **Enter**의 좌표를 모두 수정하고 문장 입력에 차례대로 입력하며 확인합니다.
<img width="1520" height="438" alt="Image" src="https://github.com/user-attachments/assets/3a01331f-c1b0-402b-b966-d7c0ff4fa67c" />

<br><br>


---

<br><br><br><br>


# 코드 설명
<details>
<summary><b>라이브러리</b></summary>
    
``` python
from roboid import *        # RaccoonBot 제어를 위한 라이브러리
import threading            # 멀티스레딩(동시에 여러 작업 실행) 지원
import keyboard             # 키보드 입력 감지 라이브러리 (Windows 관리자 권한 필요)
import ctypes               # Windows API 호출 (Caps Lock 상태 확인용)
import time                 # 시간 관련 함수 (대기, 경과시간 계산 등)
from threading import Lock  # 스레드 동기화를 위한 Lock 객체
```
</details>

---

<details>
<summary><b>초기 상태 정의</b></summary>
    
``` python
robot = Raccoon()             # 로봇 객체 생성 → RaccoonBot 제어 시작
start_time = time.time()      # 프로그램 시작 시간 기록 (로그 경과시간 표시용)
input_detection_lock = Lock() # 입력 감시 스레드와 메인 루프 동기화용 Lock
```
</details>

---

<details>
<summary><b>로그 출력</b></summary>
    
``` python
def log(msg, level="info"):
    elapsed = time.time() - start_time   # 시작 시각 이후 경과시간
    color_codes = {                      # 로그 색상 정의
        "start": 37, "ready": 92, "warn": 33,
        "error": 31, "key": 32, "default": 37
    }
    color = color_codes.get(level, 37)   # 레벨별 색상 선택
    # [시간] 메시지 (색상) 형태로 출력
    print(f"\033[90m[{elapsed:8.2f}s]\033[0m \033[{color}m{msg}\033[0m")
```
</details>

---

<details>
<summary><b>상태 변수</b></summary>
    
``` python
unexpected_input_detected = False   # 잘못된 키 입력이 감지되었는지 여부
current_expected_key = None         # 현재 입력을 기다리는 키
last_detection_time = 0             # 마지막 잘못된 입력 감지 시간
cooldown_secs = 1.5                 # 잘못된 입력 후 일정 시간 무시(중복 방지)
```
</details>

---

<details>
<summary><b>함수</b></summary>

<br>

<details>
<summary><b>Caps lock 상태 반환</b></summary>
    
``` python
def is_capslock_on():
    # Windows API(User32.dll)에서 Caps Lock 상태(0x14 키 코드) 읽기
    return ctypes.WinDLL("User32.dll").GetKeyState(0x14) & 0x0001 != 0
```
</details>

<br>
    
<details>
<summary><b>잘못된 키 입력 감지</b></summary>
    
``` python
def monitor_unexpected_keys(expected_key_getter):
    """
    예상한 키가 아닌 다른 키가 눌리면 감지해서
    - 로봇이 경고음을 내고
    - 해당 단어 입력을 중단
    """
    global unexpected_input_detected, last_detection_time
    while True:
        with input_detection_lock:   # 스레드 동기화
            now = time.time()
            expected_key = expected_key_getter()  # 현재 기대 키

            # 입력 감시 중지 조건
            if (expected_key is None or unexpected_input_detected or
                (now - last_detection_time < cooldown_secs)):
                time.sleep(0.1)
                continue

            # 현재 눌린 키 목록
            pressed_keys = keyboard._pressed_events.copy()
            expected_codes = keyboard.key_to_scan_codes(expected_key) if expected_key else []

            # 예상 외 키가 눌렸는지 확인
            for code in pressed_keys:
                if code not in expected_codes:
                    if not keyboard.is_pressed(expected_key):  # 기대 키도 아닌 경우
                        robot.sound("ENGINE")                 # 경고음
                        unexpected_input_detected = True
                        last_detection_time = time.time()
                        keyboard._pressed_events.clear()      # 키 상태 초기화
                        log("Unexpected key detected! Skipping to next word.", "error")
                        break
        time.sleep(0.05)  # CPU 과부하 방지
```
</details>

<br>

<details>
<summary><b>입력 대기 중인 키</b></summary>
    
``` python
def get_expected_key():
    return current_expected_key
```
</details>
    
<br>
    
<details>
<summary><b>타이핑 및 재시도</b></summary>
    
``` python
def try_key_press(move_func, x, y, z, key_name, max_attempts=2, **kwargs):
    """
    로봇이 키를 눌렀다고 판단될 때까지 최대 max_attempts번 재시도
    """
    for attempt in range(max_attempts):
        if unexpected_input_detected:  # 오입력 발생 시 즉시 종료
            log(f"Aborted key press [{key_name}] due to unexpected input", "default")
            return "unexpected"

        result = move_func(x, y, z, key_name, **kwargs)  # 실제 키 누르기 실행
        if result == True:
            return True
        elif result == "unexpected":
            return "unexpected"
        log(f"Retrying [{key_name}] (Attempt {attempt + 2})")
    log(f"Failed to press [{key_name}] after {max_attempts} attempts.", "error")
    return False
```
</details>
    
<br>
    
<details>
<summary><b>실제 키다운 감지</b></summary>
    
``` python
def move_key(x, y, z, key, z_after=10, timeout=3, log_key_name=None):
    """
    로봇이 지정된 좌표(x, y, z)로 이동 → 키 누름 → 입력 감지
    성공 시 True, 실패 시 False, 오입력 발생 시 "unexpected" 반환
    """
    global current_expected_key
    if unexpected_input_detected:
        log(f"Aborting [{log_key_name or key}] before movement due to unexpected input")
        return "unexpected"

    current_expected_key = key
    robot.move_to(x, y, z_after)   # 안전 높이로 이동
    robot.move_to_async(x, y, z)   # 키 누르기 (비동기)

    start_wait = time.time()
    while time.time() - start_wait < timeout:
        if unexpected_input_detected:   # 중간에 오입력 발생 시 중단
            robot.move_to(x, y, z_after)
            current_expected_key = None
            return "unexpected"
        
        if keyboard.is_pressed(key):    # 올바른 키 입력 확인
            log(f"Key press detected: [{key.upper()}]", "key")
            keyboard._pressed_events.clear()  # 입력 상태 초기화
            time.sleep(0.05)
            robot.move_to(x, y, z_after)     # 키에서 손 떼기
            time.sleep(0.01)
            current_expected_key = None
            return True
        time.sleep(0.01)

    # 제한 시간 초과
    log(f"Timeout waiting for key press: [{key}]", "error")
    robot.move_to(x, y, z_after)
    current_expected_key = None
    return False
```
</details>
    
<br>
    
<details>
<summary><b>키 매핑</b></summary>
    
``` python
def key_mapping(letter):
    """
    각 키 문자에 해당하는 (x, y, z) 좌표 반환
    설치된 키보드 위치에 따라 보정 필요
    """
    coords = {
        # 생략
    }
    return coords.get(letter)
```
</details>
    
<br>
    
<details>
<summary><b>Caps lock 토글</b></summary>
    
``` python
def toggle_capslock(should_be_on):
    # 현재 Caps Lock 상태와 원하는 상태가 다를 때만 동작
    if is_capslock_on() != should_be_on:
        # 'caps lock' 키에 해당하는 로봇 좌표 가져오기
        x, y, z = key_mapping('caps lock')

        # 로그 출력: CAPS ON 또는 CAPS OFF
        log(f"{'CAPS ON' if should_be_on else 'CAPS OFF'}", "warn")

        # 로봇팔을 해당 좌표로 이동시켜 Caps Lock 키를 눌러 상태 변경
        return try_key_press(move_key, x, y, z, 'caps lock',
                             z_after=10, log_key_name='Caps lock')
    # 이미 원하는 상태라면 아무 동작 없이 True 반환
    return True

```
</details>
</details>

---

<details>
<summary><b>초기 설정</b></summary>
    
``` python
words = ["Hello World"]  # 여러 문장은 ["문장1", "문장2"] 형태로 작성
word_idx = 0             # 현재 문장 인덱스
i = 0                    # 현재 글자 인덱스

robot.lock_vert()                       # 수직축 고정
robot.move_to(0, 15, 15)                # 초기 위치로 이동
log("System starting...", "start")
log("Loading key mappings...", "start")
log(f"Initial Caps Lock state: {'ON' if is_capslock_on() else 'OFF'}", "start")
log(f"Sentence settings: \"{words[0]}\"", "start")
log("System ready", "ready")
robot.sound("BEEP")                     # 준비 완료 신호음
```
</details>

---

<details>
<summary><b>잘못된 입력 감지 시작</b></summary>
    
``` python
threading.Thread(target=monitor_unexpected_keys, args=(get_expected_key,), daemon=True).start()
```
</details>

---

<details>
<summary><b>메인 루프</b></summary>
    
``` python
while True:
    # 1) 오입력 발생 시 처리
    if unexpected_input_detected:
        with input_detection_lock:
            x, y, z = key_mapping('enter')
            unexpected_input_detected = False
            try_key_press(move_key, x, y, z, 'enter', z_after=10, log_key_name='Enter')
            i = 0
            word_idx = (word_idx + 1) % len(words)  # 다음 문장으로 전환
            robot.move_to(0, 15, 15)
            log(f'Ready to typing: "{words[word_idx]}"', "ready")
            wait(500)
            robot.sound("BEEP")
        continue

    cur_word = words[word_idx]

    # 2) 문장 끝나면 엔터 + 다음 문장
    if i >= len(cur_word):
        log(f"Finished typing: \"{cur_word}\"", "ready")
        x, y, z = key_mapping('enter')
        try_key_press(move_key, x, y, z, 'enter', z_after=10, log_key_name='Enter')
        i = 0
        word_idx = (word_idx + 1) % len(words)
        robot.move_to(0, 15, 15)
        robot.sound_until_done("GOOD JOB", 1)
        wait(100)
        log(f'Ready to typing: "{words[word_idx]}"', "ready")
        wait(500)
        robot.sound("BEEP")
        continue

    letter = cur_word[i]

    # 3) 공백 입력 처리
    if letter == ' ':
        x, y, z = key_mapping('space')
        log(f"Move to [Space] at {(x, y, z)}")
        try_key_press(move_key, x, y, z, 'space', z_after=10, log_key_name='Space')
        i += 1
        continue

    # 4) 알파벳 처리 (대소문자 구분)
    elif letter.isalpha():
        lower_letter = letter.lower()
        if letter.isupper():
            if toggle_capslock(True) == "unexpected":
                continue
        x, y, z = key_mapping(lower_letter)
        log(f"Move to type [{letter}] at {(x, y, z)}")
        if try_key_press(move_key, x, y, z, lower_letter, z_after=10) == "unexpected":
            continue
        if letter.isupper():
            if toggle_capslock(False) == "unexpected":
                continue

    # 5) 특수문자 처리
    else:
        coords = key_mapping(letter)
        if coords:
            x, y, z = coords
            log(f"Move to type [{letter}] at {coords}")
            try_key_press(move_key, x, y, z, letter, z_after=10)

    i += 1
```
</details>

<br>
