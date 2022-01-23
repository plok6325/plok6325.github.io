---
title: 自动驾驶GTA-Part 1 -获取图像

date: 2017-06-11 20:00:00
categories: Deep-learning
--- 


我们要尝试用Deep learning 的方法 驾驶GTA ～ 

![gta1](/images/gta5-1.jpg)
 

第一步当然是要**将图像作为输入**  
1. 使用PIL 里的ImageGrab 抓取获取图像  
2. 引用time 模块 计时 （检测刷新度）
3. 抓取的图像 用CV2 新建窗口监控 （抓取的是BGR，需要换成RGB）
4. 按Q 键终止程序




        import numpy as np
        from PIL import ImageGrab
        import cv2
        import time

        def screen_record(): 
            last_time = time.time()
            while(True):
                # 800x600 windowed mode for GTA 5, at the top left position of your main screen.
                # 40 px accounts for title bar. 
                printscreen =  np.array(ImageGrab.grab(bbox=(0,40,800,640)))
                print('loop took {} seconds'.format(time.time()-last_time))
                last_time = time.time()
                cv2.imshow('window',cv2.cvtColor(printscreen, cv2.COLOR_BGR2RGB))
                if cv2.waitKey(25) & 0xFF == ord('q'):
                    cv2.destroyAllWindows()
                    break

        screen_record()

## 大概10FPS
 