### pep8 변수명 설정 convention

- Class Names   
" Class names should normally use the CapWords convention. "   

class의 이름은 CapWords convention 을 따른다. 즉 첫 글자는 대문자 이어지는 다음 단어가 있으면 다음 단어의 첫 글자 역시 대문자이다.   
ex ) 
~~~
class CustomLogger:
~~~

- Function and Variable Names   
"Function names should be lowercase, with words separated by underscores as necessary to improve readability."   

함수명과 변수명은 둘 다 소문자로 쓰는것이 원칙이다. 두 단어를 사용하는 경우 '_' 언더바(underscore)를 사용한다.

ex )
~~~
def get_data
my_dict = dict()
~~~

- 예약어와 충돌할 경우    
함수 인자가 예약어와 충돌할 경우 인자뒤에 '_' 언더바(underscore)를 붙인다.   
ex )
~~~
def func1(time_, name_):
~~~


-----
레퍼런스



[1] https://www.python.org/dev/peps/pep-0008/#id46   
[2] https://b.luavis.kr/python/python-convention

