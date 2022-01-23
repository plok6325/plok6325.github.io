---
title: 自动驾驶GTA-Part 2 & Part 3 - 操纵 

date: 2017-06-11 21:00:00
categories: Deep-learning
--- 




我们要尝试用Deep learning 的方法 驾驶GTA ～ 

![gta1](/images/gta5-1.jpg)

这章讲如何预处理数据 和操纵GTA

1. ctypes  - 用它操纵GTA（模拟键入WASD ） 
2. RGB 图像 to  灰度


        import numpy as np
        from PIL import ImageGrab
        import cv2
        import time
        import pyautogui
        from directkeys import PressKey, W, A, S, D

        def process_img(image):
            original_image = image
            # convert to gray
            processed_img = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
            # edge detection
            processed_img =  cv2.Canny(processed_img, threshold1 = 200, threshold2=300)
            return processed_img

        def main():
            
            for i in list(range(4))[::-1]:
                print(i+1)
                time.sleep(1)

            last_time = time.time()
            while True:
                PressKey(W)
                screen =  np.array(ImageGrab.grab(bbox=(0,40,800,640)))
                #print('Frame took {} seconds'.format(time.time()-last_time))
                last_time = time.time()
                new_screen = process_img(screen)
                cv2.imshow('window', new_screen)
                #cv2.imshow('window',cv2.cvtColor(screen, cv2.COLOR_BGR2RGB))
                if cv2.waitKey(25) & 0xFF == ord('q'):
                    cv2.destroyAllWindows()
                    break


**操纵部分** 
1. 按下W - 过一秒 - 释放W 


        ### directkeys.py
        --- 
        import ctypes
        import time

        SendInput = ctypes.windll.user32.SendInput

        W = 0x11
        A = 0x1E
        S = 0x1F
        D = 0x20


        # C struct redefinitions 
        PUL = ctypes.POINTER(ctypes.c_ulong)
        class KeyBdInput(ctypes.Structure):
            _fields_ = [("wVk", ctypes.c_ushort),
                        ("wScan", ctypes.c_ushort),
                        ("dwFlags", ctypes.c_ulong),
                        ("time", ctypes.c_ulong),
                        ("dwExtraInfo", PUL)]

        class HardwareInput(ctypes.Structure):
            _fields_ = [("uMsg", ctypes.c_ulong),
                        ("wParamL", ctypes.c_short),
                        ("wParamH", ctypes.c_ushort)]

        class MouseInput(ctypes.Structure):
            _fields_ = [("dx", ctypes.c_long),
                        ("dy", ctypes.c_long),
                        ("mouseData", ctypes.c_ulong),
                        ("dwFlags", ctypes.c_ulong),
                        ("time",ctypes.c_ulong),
                        ("dwExtraInfo", PUL)]

        class Input_I(ctypes.Union):
            _fields_ = [("ki", KeyBdInput),
                        ("mi", MouseInput),
                        ("hi", HardwareInput)]

        class Input(ctypes.Structure):
            _fields_ = [("type", ctypes.c_ulong),
                        ("ii", Input_I)]

        # Actuals Functions

        def PressKey(hexKeyCode):
            extra = ctypes.c_ulong(0)
            ii_ = Input_I()
            ii_.ki = KeyBdInput( 0, hexKeyCode, 0x0008, 0, ctypes.pointer(extra) )
            x = Input( ctypes.c_ulong(1), ii_ )
            ctypes.windll.user32.SendInput(1, ctypes.pointer(x), ctypes.sizeof(x))

        def ReleaseKey(hexKeyCode):
            extra = ctypes.c_ulong(0)
            ii_ = Input_I()
            ii_.ki = KeyBdInput( 0, hexKeyCode, 0x0008 | 0x0002, 0, ctypes.pointer(extra) )
            x = Input( ctypes.c_ulong(1), ii_ )
            ctypes.windll.user32.SendInput(1, ctypes.pointer(x), ctypes.sizeof(x))

        # directx scan codes http://www.gamespp.com/directx/directInputKeyboardScanCodes.html

        if __name__ == '__main__':
            while (True):
                PressKey(0x11)
                time.sleep(1)
                ReleaseKey(0x11)
                time.sleep(1)