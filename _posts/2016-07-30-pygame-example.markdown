---
layout: post
title:  "pygame 예제"
date:   2016-02-12 17:50:00
categories: main
---

Python은 다들 어느 정도 쓸 줄 아시죠? 이제는 pygame의 기본 기능을 학습해 보도록
합시다.

새 python파일을 만들고, 다음과 같이 적습니다.  
{% highlight python %}
import pygame
{% endhighlight %}

이제 pygame 모듈에 구현된 모든 기능을 바로 이용할 수 있습니다.
다만, 좀 더 편리한 개발을 위해 약간의 준비를 더 해야 합니다.  
{% highlight python %}
import pygame
from pygame.locals import *
{% endhighlight %}


from 명령으로 pygame모듈 안에 정의되어 있는 로컬 변수와 상수들을 가져왔습니다. pygame안에는 `QUIT`, `K_UP`, `K_DOWN`등의 여러 상수들이 미리 정의되어 있습니다.
그냥 import만 해도 `pygame.QUIT`, `pygame.K_UP`등으로 사용이 가능하지만, 매번 `pygame.`을 치기 귀찮은 상황이 올 수도 있으니 적어 둡시다.

게임의 기본이 될 화면을 만들어 봅시다.
{% highlight python %}
import pygame
from pygame.locals import *

pygame.init()

width, height = 640, 480
screen = pygame.display.set_mode((width, height))
{% endhighlight %}

pygame.init()은 pygame 모듈을 초기화시킵니다. 간혹 제대로 구현되지 않는 기능이 있을 수 있기에 사용합니다.  
위의 코드를 통해 640 x 480 크기의 창을 만들었습니다. 다른 숫자를 입력한다면 다른 크기의 창을 만들 수 있겠죠?

위의 코드들은 게임이 실행될 때 처음 단 한 번만 실행되는 코드들입니다. 즉, 게임의 기본 설정을 담당하는 부분이라고 할 수 있습니다.  
실제 게임에서는 화면을 끊임없이 표시해 줘야 하므로, 한 번만 실행되는 코드만으로는 만들 수 없습니다.  
따라서 저희는 `while` 문법을 통해 특정 코드들을 게임이 실행되는 동안 끝없이 반복시킬 것입니다.

코드의 맨 아래에 다음과 같은 코드를 다시 써 넣읍시다.  
{% highlight python %}
while True:
    screen.fill(0)
    pygame.display.update()
{% endhighlight %}
