---
layout: post
title:  "pygame 예제 - Step 1"
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

<br>
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

<br>
코드의 맨 아래에 다음과 같은 코드를 다시 써 넣읍시다.  
{% highlight python %}
while True:
    screen.fill(0)
    pygame.display.update()
{% endhighlight %}

말 그대로, screen을 컬러코드 값 0, 즉 검정색으로 칠하고 display를 업데이트하는 코드입니다. 코드를 짤 때 `display.update()`를 잊지 않도록 하세요. 애써 짜놓은 결과물이 업데이트가 되지 않아 보이지 않을지도 모릅니다.


<br>
혹시 위의 코드를 짜서 이미 실행해 보았나요? 그렇다면, 종료 버튼을 눌러도 프로그램이 정상적으로 종료되지 않음을 볼 수 있었을 겁니다. 이는 프로그램 내부에서 종료 이벤트를 처리하지 않았기 때문에 발생하는 문제입니다.

종료 이벤트를 핸들링해주기 위해, 다음과 같은 코드를 while문 안에 추가합니다.  
{% highlight python %}
for event in pygame.event.get():
    if event.type == QUIT:  ## also pygame.QUIT
        pygame.quit()
        exit(0)
{% endhighlight %}

pygame은 게임이 실행 중 발생한 이벤트들을 담아 놓고, 이를 pygame.event.get() 함수를 통해 접근할 수 있습니다.
위 코드는 pygame에서 발생한 이벤트 중, event의 type이 `QUIT`, 즉 종료인 이벤트가 있을 경우 게임을 종료해 주는 역할을 합니다. 이제 종료 버튼이 제대로 동작하는 걸 볼 수 있을 것입니다. 비슷한 원리로, 방향키가 눌렸을 때의 처리도 가능합니다:  
{% highlight python %}
if event.type == KEYDOWN:
    if event.key == K_RIGHT:
        # source #
    elif event.key == K_LEFT
        # source #
    elif event.key == K_DOWN:
        # source #
    elif event.key == K_UP:
        # source #
    else:
        continue
{% endhighlight %}

위와 같은 코드로, 각각 오른쪽/왼쪽/아래/위쪽 키를 눌렀을 때의 동작을 설정할 수 있습니다. 이 밖에도 pygame은 많은 입력을 지원하며, 따라서 다른 키를 다른 동작에 배치할 수도 있습니다.

<br>
이제 우리가 원하는 이미지를 불러와 봅시다. 원하는 이미지를 소스 파일이 위치한 폴더에 다운받습니다. 저는 임의로 이미지 파일의 이름을 `player_test.png`라고 하겠습니다.
이제 이미지를 pygame 내부에서 불러올 수 있습니다.  
{% highlight python %}
player = pygame.image.load('player_test.png')
{% endhighlight %}

위 코드는 player_test.png라는 이미지를 불러와 앞으로 player라고 부르게 해 주는 코드입니다. 이제 player를 화면의 어디에 배치할지 마음대로 정할 수 있습니다.  
{% highlight python %}
screen.blit(player, (0, 0))
{% endhighlight %}

위 코드를 통해 player를 screen의 (0, 0) 좌표에 표시하였습니다. 실행을 시켜 보면, 검은 화면의 왼쪽 위 구석에 불러온 이미지가 떠 있을 것입니다.

<br>
혹시 포토샵 등의 이미지 편집 툴을 사용해 본 적이 있나요? 그렇다면 Layer라는 개념에 대해 들어본 적이 있을 것입니다. pygame에서도 Layer와 비슷한 개념을 사용할 수 있습니다.  
pygame에서는 이를 Surface라고 합니다. 다음의 코드를 봅시다.  
{% highlight python %}
screen = pygame.display.set_mode((360, 680))
gameWindow = pygame.Surface((360, 600))

screen.fill((100, 100, 100))
gameWindow.fill(0)

gameWindow.blit(player, (0, 0))
screen.blit(gameWindow, (0, 80))
{% endhighlight %}

위 코드에서는 먼저 360 x 680 크기의 창을 먼저 만들었습니다. 그 후 360 x 600짜리 Surface를 하나 만들어 `gameWindow`라고 명명했죠.  
이제 `screen`을 `(R, G, B) = (100, 100, 100)`의 컬러, 즉 어두운 회색으로 채우고 `gameWindow`를 검정색으로 채웠습니다.  
그 후, `blit`함수를 통해 `player`를 `gameWindow`의 (0, 0)위치에다가 표시하도록 하고, 다시 그 gameWindow를 screen의 (0, 80) 좌표에 표시하였습니다.  
그렇다면 `screen` 기준으로, `player`는 (0, 80)의 좌표에 위치하게 됩니다. 만약 `player`가 gameWindow의 (20, 30) 좌표에 위치했다면, `screen` 기준으로는 (20, 110) 좌표에 위치하게 되겠죠. 다음처럼 말입니다.

<p align = "CENTER">
  <img src="{{ site.baseurl }}/images/image1.png" style="height: 540px;">
</p>
