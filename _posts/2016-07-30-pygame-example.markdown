---
layout: default
title:  "pygame 예제"
date:   2016-02-12 17:50:00
categories: main
---

Python은 다들 어느 정도 쓸 줄 아시죠? 이제는 pygame의 기본 기능을 학습해 보도록
합시다.

새 python파일을 만들고, 다음과 같이 적습니다.  
```python
import pygame
```

이제 pygame 모듈에 구현된 모든 기능을 바로 이용할 수 있습니다.
다만, 좀 더 편리한 개발을 위해 약간의 준비를 더 해야 합니다.  
```python
import pygame
from pygame.locals import *
```  


from 명령으로 pygame모듈 안에 정의되어 있는 로컬 변수와 상수들을 가져왔습니다. pygame안에는 `QUIT`, `K_UP`, `K_DOWN`등의 여러 상수들이 미리 정의되어 있습니다.
그냥 import만 해도 `pygame.QUIT`, `pygame.K_UP`등으로 사용이 가능하지만, 매번 `pygame.`을 치기 귀찮은 상황이 올 수도 있으니 적어 둡시다.
