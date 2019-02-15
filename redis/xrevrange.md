## XREVRANGE

xadd 를 하면 main key 아래에 타임스탬프 순으로 값들이 들어가게 된다.    
이때 xrange 를 통해 main key에 값들을 받을 수 있다

~~~
xrange main_key - + 
~~~

나의 고민은 xadd 를 통해 들어간 마지막 값을 어떻게 반환시켜야 하는 것이었다.   
xrange 로 전체 값을 받아 마지막 값을 얻기는 너무 비효율적이란 생각이 들었다.  


그러다가 XREVRANGE를 발견하게 되었다.   
XREVRANGE는 이름에서 알 수 있듯이 xrange 를 역순으로 출력해준다.   
그래서 count 옵션을 추가하면 마지막 값만 반환할 수 있다.

~~~ 
XREVRANGE MAIN_KEY + - count 1 
~~~

xrange 에서는 - + 였다면 xrevrange 는 반대로 + - 이다 .



------
레퍼런스
[1] https://redis.io/commands/xrange   
[2] https://redis.io/topics/streams-intro
