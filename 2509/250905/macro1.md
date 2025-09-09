```python
# import pyautogui
# import time
# import keyboard
#
# coords= [(1176, 915), (1182, 726), (949, 652), (1086, 687)]
#
# # while True:
# #     time.sleep(0.5)
# #     print(pyautogui.position())
#
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
#         if keyboard.is_pressed("F8"):
#             # print("매크로 종료")
#             exit()
#     if keyboard.is_pressed("F8"):
#         # print("매크로 종료")
#         exit()
#     pyautogui.press("esc")
#     # print("ESC 키 입력 완료")
#     if keyboard.is_pressed("F8"):
#         # print("매크로 종료")
#         exit()


import ctypes
import time
import keyboard
import pyautogui

SendInput = ctypes.windll.user32.SendInput

PUL = ctypes.POINTER(ctypes.c_ulong)

class MOUSEINPUT(ctypes.Structure):
    _fields_ = [("dx", ctypes.c_long),
                ("dy", ctypes.c_long),
                ("mouseData", ctypes.c_ulong),
                ("dwFlags", ctypes.c_ulong),
                ("time", ctypes.c_ulong),
                ("dwExtraInfo", PUL)]

class KEYBDINPUT(ctypes.Structure):
    _fields_ = [("wVk", ctypes.c_ushort),
                ("wScan", ctypes.c_ushort),
                ("dwFlags", ctypes.c_ulong),
                ("time", ctypes.c_ulong),
                ("dwExtraInfo", PUL)]

class HARDWAREINPUT(ctypes.Structure):
    _fields_ = [("uMsg", ctypes.c_ulong),
                ("wParamL", ctypes.c_short),
                ("wParamH", ctypes.c_ushort)]

class _INPUTunion(ctypes.Union):
    _fields_ = [("mi", MOUSEINPUT),
                ("ki", KEYBDINPUT),
                ("hi", HARDWAREINPUT)]

class INPUT(ctypes.Structure):
    _fields_ = [("type", ctypes.c_ulong),
                ("union", _INPUTunion)]

# 마우스 이벤트 플래그
MOUSEEVENTF_LEFTDOWN = 0x0002
MOUSEEVENTF_LEFTUP   = 0x0004

# 키보드 이벤트 플래그
KEYEVENTF_KEYUP = 0x0002
VK_ESC = 0x1B

def click_fast(x, y):
    """해당 좌표에서 빠른 클릭"""
    pyautogui.moveTo(x, y)  # 좌표 이동
    extra = ctypes.c_ulong(0)

    inp = INPUT(type=0, union=_INPUTunion(mi=MOUSEINPUT(0, 0, 0, MOUSEEVENTF_LEFTDOWN, 0, ctypes.pointer(extra))))
    SendInput(1, ctypes.pointer(inp), ctypes.sizeof(inp))

    inp = INPUT(type=0, union=_INPUTunion(mi=MOUSEINPUT(0, 0, 0, MOUSEEVENTF_LEFTUP, 0, ctypes.pointer(extra))))
    SendInput(1, ctypes.pointer(inp), ctypes.sizeof(inp))

def press_esc():
    """ESC 키 입력"""
    extra = ctypes.c_ulong(0)

    # 키 누름
    inp = INPUT(type=1, union=_INPUTunion(ki=KEYBDINPUT(VK_ESC, 0, 0, 0, ctypes.pointer(extra))))
    SendInput(1, ctypes.pointer(inp), ctypes.sizeof(inp))

    # 키 뗌
    inp = INPUT(type=1, union=_INPUTunion(ki=KEYBDINPUT(VK_ESC, 0, KEYEVENTF_KEYUP, 0, ctypes.pointer(extra))))
    SendInput(1, ctypes.pointer(inp), ctypes.sizeof(inp))

# 클릭할 좌표들
coords = [(1176, 915), (1182, 726), (949, 652), (1086, 687)]

# print("시작합니다. (F8 누르면 종료)")
# time.sleep(2)

while True:
    if keyboard.is_pressed("F8"):
        print("종료")
        break

    for (x, y) in coords:
        if keyboard.is_pressed("F8"):
            print("종료")
            exit()
        click_fast(x, y)
        time.sleep(0.0001)  # CPU 부담 줄이려면 살짝 쉼
    # time.sleep(0.0001)
    press_esc()
```