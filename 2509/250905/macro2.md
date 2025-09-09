```python
import time
import os
import re
import keyboard
import pyautogui
from PIL import Image
import pytesseract
import cv2
import numpy as np

# ===== 사용자 설정 =====
TESSERACT_PATH = r"C:\Program Files\Tesseract-OCR\tesseract.exe"  # 설치 경로에 맞게 수정
pytesseract.pytesseract.tesseract_cmd = TESSERACT_PATH

coords= [(1081, 790), (1544, 279)]

# while True:
#     time.sleep(0.5)
#     print(pyautogui.position())

COLOR_TOL = 35
MAX_WAIT = 15.0
HOTKEY = "F8"
LIMIT = 35

PLAY_X, PLAY_Y = 1081, 790 #플레이 버튼 위치
MORE_X, MORE_Y = 1544, 279 # ... 버튼 위치
CHANNEL_REGION = (651, 425, 755-651, 447-425) #채널인원 ocr (left , top, width, height)
Login_X, Login_Y = 1208, 768 # 로그인 버튼 위치
Sel_X, Sel_Y = 675, 764 #캐릭터선택 위치

def get_player_count():
    """CHANNEL_REGION에서 숫자 추출"""
    img = pyautogui.screenshot(region=CHANNEL_REGION)
    text = pytesseract.image_to_string(img, lang="kor+eng", config="--psm 7")
    print("OCR 결과:", text.strip())

    # "플레이어(83/100)" → 83 추출
    nums = re.findall(r"\d+", text)
    if len(nums) >= 1:
        return int(nums[0])
    return None

def color_changed(a, b, tol=COLOR_TOL):
    """두 RGB 색의 차이가 tol 이상이면 True"""
    return abs(a[0]-b[0]) + abs(a[1]-b[1]) + abs(a[2]-b[2]) >= tol

def wait_until_more_appears(timeout=MAX_WAIT):
    """
    PLAY 클릭 직후 MORE 좌표의 '기준 색'을 측정하고,
    그 픽셀이 충분히 달라질 때까지 대기.
    """
    try:
        base = pyautogui.pixel(MORE_X, MORE_Y)  # 기준 색상
    except OSError:
        # 좌표가 화면 밖이면 발생. 해상도/배율 확인 필요
        base = None

    start = time.time()
    while time.time() - start <= timeout:
        if keyboard.is_pressed(HOTKEY):
            raise SystemExit
        try:
            cur = pyautogui.pixel(MORE_X, MORE_Y)
        except OSError:
            cur = None

        # 기준색이 없다면 현재 프레임을 기준으로 갱신 후 다음 루프
        if base is None and cur is not None:
            base = cur
        elif base is not None and cur is not None:
            if color_changed(cur, base):
                return True
        time.sleep(0.02)  # CPU 과점유 방지
    return False

def fast_click(x, y):
    """딜레이 최소화 빠른 클릭"""
    pyautogui.mouseDown(x, y)
    pyautogui.mouseUp(x, y)

while True:
    if keyboard.is_pressed(HOTKEY):
        print("종료")
        break

    # 1) 플레이 클릭
    fast_click(PLAY_X, PLAY_Y)

    pyautogui.press("enter")

    # 2) 로딩 → ... 버튼 등장 대기 (픽셀 색 변화 감지)
    appeared = wait_until_more_appears(timeout=MAX_WAIT)
    time.sleep(0.1)

    if keyboard.is_pressed(HOTKEY):
        print("종료")
        break

    if appeared:
        # 3) ... 버튼 클릭
        fast_click(MORE_X, MORE_Y)
        print("... 버튼 클릭 완료")

        time.sleep(0.1)
        count = get_player_count()

        if count is None:
            print("인원 숫자 인식 실패 → 다시 시도")
            fast_click(Login_X, Login_Y)
            time.sleep(0.3)
            pyautogui.press("enter")

            # ✅ 로비에서 '플레이' 버튼이 다시 뜰 때까지 대기
            if wait_until_more_appears(timeout=5):
                print("플레이 버튼 재등장 대기 시간 초과 → 재시도")
                time.sleep(1.5)
            # 다음 루프로 (플레이 클릭) 진행
            continue

        if count > LIMIT:
            print(f"채널 인원 {count}명 → 접속 진행 X")
            # 여기서 Enter 누르거나 접속 버튼 클릭
            fast_click(Login_X,Login_Y)
            time.sleep(0.3)
            pyautogui.press("enter")

            # ✅ 로비에서 '플레이' 버튼이 다시 뜰 때까지 대기
            if wait_until_more_appears(timeout=5):
                print("플레이 버튼 재등장 대기 시간 초과 → 재시도")
                time.sleep(1.5)
            # 다음 루프로 (플레이 클릭) 진행
            continue
        else :
            print(f"채널인원 {count}명")
            time.sleep(0.1)
            pyautogui.press("esc")
            time.sleep(0.1)

            while True:
                if keyboard.is_pressed(HOTKEY):
                    print("종료")
                    break
                fast_click(Login_X, Login_Y)
                if wait_until_more_appears(timeout=30):
                    break
            while True:
                if keyboard.is_pressed(HOTKEY):
                    print("종료")
                    break
                pyautogui.doubleClick(Sel_X, Sel_Y)
            break

# while True:
#     if keyboard.is_pressed("F8"):
#         # print("매크로 종료")
#         exit()
#     for (x, y) in coords:
#         if keyboard.is_pressed("F8"):
#             # print("매크로 종료")
#             exit()
#         # pyautogui.click(x,y)
#         pyautogui.mouseDown(x, y)
#         pyautogui.mouseUp(x, y)
#         # print(f"Clicked at ({x}, {y})")
#         time.sleep(0.0001)

```