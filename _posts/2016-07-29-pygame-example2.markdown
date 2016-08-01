---
layout: post
title:  "pygame 예제 - Step 2"
date:   2016-02-12 17:50:00
categories: main
---

이제 화면에 표시된 이미지를 움직여 봅시다.
이미지를 변경하는 것은 기본적으로 이미지의 좌표를 시간에 따라 변경해주는 일과 동일합니다.  
예를 들어서 앞의 `player` 위치의 X좌표를 `locationX`라 하고, `while`문을 한 번 돌 때마다 X좌표를 1씩 더해주면, 이미지는 오른쪽으로 움직이는 것처럼 보일 것입니다.

다만 여기서 유의해야 할 점이 하나 있습니다.  
while문은 어느 정도의 빠르기로 돌아가는 것일까요?  
똑같이 X좌표를 1씩 더해주어도, while문이 1초에 60번 도는 것과 1초에 30분 도는 것과는, 눈으로 보기에 두 배의 속도 차이가 있습니다.  
또한 컴퓨터의 성능이 낮다면, 성능이 좋은 컴퓨터에서 돌리는 것과 빠르기가 다를 수 있을 것입니다.  
따라서 게임의 FPS(Frames Per Second)를 조절해주는 것이 필요합니다.  
{% highlight python %}
FPS = 30
clock = pygame.time.Clock()
{% endhighlight %}

다음과 같은 코드를 게임이 실행될 때 단 한 번 실행되도록 적어 줍니다. 그 후, while문 안에는 다음과 같은 소스를 추가합니다.  
{% highlight python %}
clock.tick(FPS)
{% endhighlight %}

위에서 FPS를 30으로 설정했기 때문에, 이제 게임은 1초에 30번 화면을 업데이트하여 보여주게 되었습니다. 보통 사람은 24프레임 부근부터 연속적인 움직임이라고 인식하며, 60프레임 정도면 매우 부드러운 움직임이라고 인식합니다. 다만, 저희가 만들 게임인 테트리스는 연속적인 움직임이 많이 필요하지 않으므로, FPS가 매우 낮아도 상관없습니다.

<br>
이 때, 움직이는 이미지를 하나뿐이 아닌, 여러 개, 혹은 수백 개 만들어 주고 싶다면 어떻게 해야 할까요? 이미지 하나하나의 좌표를 담당하는 변수를 일일이 선언해서 관리해 줄 수도 있겠지만, 이미지가 많으면 많아질수록, 귀찮은 작업이 됩니다. 이럴 때 필요한 것이 바로 객체 지향 프로그래밍(OOP) 입니다.  
아래와 같이 이미지 파일, (x, y)좌표, 속도, 새를 화면에 보여주는 함수, 새를 움직이는 함수를 포함한 Bird class를 만들었습니다.  
{% highlight python %}
class Bird:
    def __init__(self, imageName, location, spd):
        self.imageName = imageName
        self.location = location
        self.spd = spd

        self.image = pygame.image.load(imageName)

    def move(self):
        X, Y = self.location
        X += self.spd
        self.location = (X, Y)

    def show(self):
        screen.blit(self.image, self.location)
        self.move()
{% endhighlight %}

`__init__` 함수는 새로운 Bird class가 선언되면 반드시 처음 실행되는 함수입니다. 이곳에서 class 내부 변수들을 초기화하고, 함수들을 불러올 수도 있습니다.  
`self`는 자기 자신을 의미하며, `self.location = location`은 Bird class 내에 location이라는 변수를 만들고, 그 값에 class가 선언될 때에 인자로 부여받은 `location`값을 대입하겠다는 의미입니다.  
예를 들어, 게임 내부에서 `test_bird = Bird(image, (0, 0), 3)`이라고 새로운 Bird를 생성하였다면, `test_bird`의 `location`은 (0, 0), `spd`는 3이 되겠죠. (self는 인자로 따로 넣어 줄 필요가 없습니다.)

이후 표시할 이미지를 각각 `bird1.png`, `bird2.png`, `bird3.png`로 저장하고, 다음과 같은 코드를 작성해 보았습니다.  
{% highlight python %}
bird1 = Bird('bird1.png', (0, 50), 10)
bird2 = Bird('bird2.png', (100, 150), 25)
bird3 = Bird('bird3.png', (50, 250), 15)

birds = [bird1, bird2, bird3]
{% endhighlight %}

그 후 while문 안에 다음과 같은 코드를 적었습니다.
{% highlight python %}
for bird in birds:
    bird.show()
{% endhighlight %}

이제 게임을 실행하면, Python은 birds 리스트를 순환하면서 내부에 있는 bird의 show함수를 실행시킬 것입니다. 새들이 각기 다른 위치에서 다른 속도로 날아가는 걸 보실 수 있습니다.

<br>
이제 테트리스 개발에 필요한 지식을 거의 다 갖췄습니다. 이제 테트리스를 만들어 볼 시간입니다.
혹시나 더 궁금한 게 있다면,  
[http://www.gimo.co.kr/game_dev/985](http://www.gimo.co.kr/game_dev/985)  
[http://xe.obg.co.kr/index.php?mid=programming&order_type=desc&category=7767&document_srl=7933](http://xe.obg.co.kr/index.php?mid=programming&order_type=desc&category=7767&document_srl=7933)  
[http://www.pygame.org/docs/](http://www.pygame.org/docs/)  
[http://devnauts.tistory.com/61](http://devnauts.tistory.com/61) 등을 참고하시기 바랍니다.
