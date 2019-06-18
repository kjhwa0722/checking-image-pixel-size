# checking-image-pixel-size
이미지 픽셀 확인.py

import cv2
import numpy as np

def Pixel():
    imgFile = "image/coffee.jpg"
    img = cv2.imread(imgFile)

    px = img[100,200]
    print(px)
Pixel()

"""img[x,y] 라는 것은 해당 이미지 파일의 좌표값의 BGR 값을 나타냅니다.
따라서 해당 코드의 출력결과인 [198  202 207] 은 이미지의 [100,200] 좌표의 픽셀값이
BLUE 198
GREEN 202
RED 207
값이라는 의미이다.
일반적으로 이미지를 로드하게되면 3차원 행렬형태로 생성이 되며, [x축좌표,y축좌표,색상정보] 로 나타냅니다.
여기서 좌표는 해당 픽셀이 위치하고 있는 좌표이고, 
색상정보는 0은 Blue
1은 Green
2는 Red 를 의미합니다.
그렇다면 위의 코드는 BGR 세가지 색상을 나타내는 것이고, 3차원행렬 형태로 BGR중 한가지 요소만 변경 또는 읽을 수도 있다는 거겠죠?"""

px = img[100,200,0]  - 100,200  # 좌표 픽셀의 Blue 값
px = img[100,200,1]  - 100,200  # 좌표 픽셀의 Green 값
px = img[100,200,2]  - 100,200  # 좌표 픽셀의 Red 값으로 읽을 수 있습니다.

#그렇다면 해당 픽셀의 BGR 값을 변경하는 작업도 해보아야겠죠??


import cv2
import numpy as np
def Pixel():
    imgFile = "image/coffee.jpg"
    img = cv2.imread(imgFile)
    img[100,200,2] = 100
    px = img[100,200,2]
    print(px)
Pixel()
img[100,200,2] = 100

"""위와 같은 방법으로 BGR 색을 한번에 변경할 수도 있습니다.
일반적으로 특정 Pixel 값을 변경하기 위해서는 Numpy 를 사용한다고 합니다.
사용방법은 아래와 같습니다.
Numpy array의 item() 함수를 사용하여 픽셀의 BGR 하나의 값으로 접근 가능합니다.
해당 위치픽셀의 값을 BGR을 각각 변경하기 위해서는 itemset() 함수를 사용합니다"""

import cv2
import numpy as np

def Pixel():
    imgFile = "image/coffee.jpg"
    img = cv2.imread(imgFile)

    B = img.item(100,200,0)
    G = img.item(100,200,1)
    R = img.item(100,200,2)
    print(B)
    print(G)
    print(R)

Pixel()

# 이렇게 img.item(x좌표,y좌표,색정보) 를 이용하여 픽셀의 BGR 정보를 가져올 수 있습니다.


import cv2
import numpy as np

def Pixel():
    imgFile = "image/coffee.jpg"
    img = cv2.imread(imgFile)

    img.itemset((100,200,0),0)
    B = img.item(100,200,0)
    G = img.item(100,200,1)
    R = img.item(100,200,2)
    print(B)
    print(G)
    print(R)

"""img.itemset((x좌표,y좌표,색정보),변경할값) 을 이용하여 해당 픽셀의 BGR값을 변경할 수도있습니다.
이렇게 픽셀에 대한 조작을 알아보았습니다.
위의 글은 픽셀의 값들을 조정하는 작업이였다면, 지금 할 내용은 그 이전단계에서 행해야할 내용입니다.
바로 이미지의 기본속성에 대한 내용을 알아내는것입니다.
방금은 (100,200) 좌표의 픽셀이 존재하여 가능하였지만, 해당 이미지에 대한 정보가 없으면 정확하게 조작하기가 힘듭니다.
그래서 우선적으로 이미지를 로드하고 행과열 그리고 몇개의 채널로 구성되어있는지 확인해야합니다.
배울 내용은3가지입니다."""

img.shape 
img.size
img.dtype

"""하나씩 살펴봅시다.
직접 코드를 실행해보고 나오는 결과값을 통해 알아보겠습니다"""

import cv2
import numpy as np

def imgValue():
    imgFile = "image/coffee.jpg"
    img = cv2.imread(imgFile)

    print(img.shape)
    print(img.size)
    print(img.dtype)

imgValue()

# 결과값을 보고 각각의 명령어가 어떤 역할을 하며 어떠한 속성을 보여주는지 알아보겠습니다

img.shape
"""결과값 (2656,1494,3)
(height 크기, width 크기, 컬러채널수) 로서 (1494,2656) 의 크기를 가지고 있는 이미지며 ,
컬러채널수가 3인것을 보아 3가지 색상의 BGR로 구성되어있습니다.
(여기서 GRAYSCALE 의 이미지일 경우 행과 열만 출력됩니다.)"""


img.size
"""결과값 11904192
해당 이미지 파일의 사이즈입니다 ( byte )"""


img.dtype
"""결과값 uint8
이미지의 데이터 타입입니다."""

Pixel()
[출처] Python OpenCV 시작 (7) - 이미지 픽셀 조작과 속성확인|작성자 박원영
https://blog.naver.com/pk3152/221442310992
