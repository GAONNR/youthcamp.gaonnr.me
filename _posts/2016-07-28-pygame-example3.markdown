---
layout: post
title:  "pygame 예제 - Step 3"
date:   2016-02-12 17:50:00
categories: main
---

계획이 수정되었으므로, 여러분께 뭔가를 만들 때 좀 더 도움이 될 법한 함수를 몇 개 알려드리고자 합니다.
먼저 `Surface.get_rect()` 함수입니다.  
{% highlight python %}
player = pygame.image.load('player_test.png')
playerRect = player.get_rect()
{% endhighlight %}

pygame안에서 이미지는 거기에 외접한 사각형을 기준으로 처리됩니다. 이 사각형을 가져오는 함수입니다.  
{% highlight python %}
playerRect.center = (180, 300)
{% endhighlight %}

이런 식으로 rect의 중심을 바꿀 수도 있으며, 그 후  
{% highlight python %}
screen.blit(player, playerRect)
{% endhighlight %}

와 같은 코드로 원하는 좌표를 이미지의 중심으로 하게 할 수도 있습니다.

`Surface.get_size()` 함수를 이용하면 이미지나 Surface의 크기를 가져올 수도 있습니다.  


{% highlight python %}
x, y =  player.get_size()
{% endhighlight %}

다음은 `pygame.transform.flip()`함수입니다. 사용 예는 다음과 같습니다.  
{% highlight python %}
flipPlayer = pygame.transform.flip(player, True, False)
{% endhighlight %}

`flip` 함수의 첫 번째 인자는 x축을 반전하는 것을 뜻하며, 두 번째 인자는 y축을 반전하는 것을 뜻합니다.

다음은 `pygame.transform.scale()` 함수입니다. 이는 불러온 이미지나 Surface를 원하는 크기로 확대 / 축소합니다.  
{% highlight python %}
scaledPlayer = pygame.transform.scale(player, (newWidth, newHeight))
{% endhighlight %}

마지막으로 `pygame.transform.rotate()`함수입니다. 이미지나 Surface를 회전시켜 줍니다.  
Surface를 회전시키면 rect의 크기가 달라질 수 있으므로, 표시할 좌표를 rect의 center를 변경시켜서 표현하는 것이 좋습니다.  
{% highlight python %}
rotatedPlayer = pygame.transform.rotate(player, int(i * 60.0 / 60.0))
rotatedRect = rotatedPlayer.get_rect()
rotatedRect.center = (180, 300)
{% endhighlight %}
