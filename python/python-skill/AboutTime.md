안녕하세요. 개발을 하다 보면 시간 관련 함수가 필요할 때가 많은데요. 

저도 개발을 하면서 여러가지 시간 관련 함수를 구현했었습니다. 이번 포스팅에서는 그 동안 제가 파이썬으로 구현했던 시간 관련 함수를 총 정리해볼려 합니다.



먼저 개발을 할 때 사용하는 시간의 단위는 크게 두 가지가 있는데요.

우리가 평상시에 사용하는 2019-01-01 14:40:30 이런 형식의 시간 타입을 이 포스팅에서는 데이트타임(datetime) 이라 명시했습니다.

그리고 유닉스 시간, unix time , epoch time 이라 불리는 시간 타입이 있습니다. 유닉스 시간은 1970년 1월 1일 00:00:00 협정시를 기준으로 경과된 시간을 초로 환산하여 정수로 나타낸 것입니다. 유닉스 시간은 유닉스 계열 운영체제나 여러 다른 운영체제, 그리고 파일 형식들에서 사용이 됩니다. 이 시간을 이 포스팅에서는 유닉스 시간(unix time)이라고 명시했습니다.



먼저 현재 시간을 위 두 가지 타입으로 나타내는 함수를 구현해보겠습니다.



- Get now datetime



""" 데이트타임(datetime) 형식의 현재시간을 불러옴 , 밀리 세컨즈까지 출력됨 """

def get_now():
    import datetime
    now =datetime.datetime.now()
    return now


- Get now unixtime



""" 유닉스 시간(unixtime) 형식의 현재시간을 가져옴, 밀리 세컨즈까지 출력됨 """

def get_now():
    import time
    now = time.time()
    return now


이 두 가지 시간을 서로의 타입으로 바꿔줄 일이 간혹 일어납니다. 즉 datetime을 unixtime으로 변경한다거나 반대로 unixtime을 datetime으로 변경해주는 일 같은 경우죠. 아래 두 함수는 위의 두 일을 수행해줍니다.





- Convert unixtime to datetime



""" 데이터트타임(datetime)을 유닉스 시간(unixtime)으로 변경해주는 함수 """

def convert_datetime(unixtime):
    """Convert unixtime to datetime"""
    import datetime
    date = datetime.datetime.fromtimestamp(unixtime).strftime('%Y-%m-%d %H:%M:%S')
    return date  # format : str

datetime 모듈의 fromtimestamp는 timestamp 즉 unixtime을 받아 strftime 인자로 받는 형식의 데이트타임으로 변경해주는 함수입니다. 



- Convert datetime to unixtime



""" 유닉스 시간을 데이트타임으로 변경해주는 함수 """

def convert_unixtime(date_time):
    """Convert datetime to unixtime"""
    import datetime
    unixtime = datetime.datetime.strptime(date_time,
                               '%Y-%m-%d %H:%M:%S').timestamp()
    return unixtime
strptime 안에 '%Y-%m-%d %H:%M:%S'    이 부분은 이 형식으로 받은 date_time을 의미합니다. 즉 '2019-01-01 15:30:00' 같은 형식의 데이트타임을 받아서 유닉스 시간으로 변경해줍니다.



만약 데이트타임을 밀리 세컨즈까지 포함된 형식으로 받았다면 유닉스 시간 역시 밀리 세컨즈까지 표현할 수 있습니다. 아래 함수와 같이 말이죠.



def convert_unixtime(date_time):
    """Convert datetime to unixtime"""
    import datetime
    unixtime = datetime.datetime.strptime(date_time,
                               '%Y-%m-%d %H:%M:%S,%f').timestamp()
    unixtime_mili = unixtime * 1000
    return unixtime_mili
위 함수에서 date_time 형식은 '2019-02-17 15:30:00,15' 와 같습니다. 형식은 여러분의 데이터의 맞게 바꿔주시면 됩니다.



- Add datetime



이번에는 데이트타임을 받아서 해당 데이트타임의 시간을 늘려주는 함수를 구현해보겠습니다. 아래의 함수는 데이트타임을 1분 증가시키고 반환해주는 함수입니다.



def add_datetime(date_time):
    """
    :return: add 1 minute datetime
    """
    import datetime
    date_time = datetime.datetime.strptime(date_time, "%Y-%m-%d %H:%M:%S")
    date_time += datetime.timedelta(minutes=1)
    return date_time
date_time의 형식은 '2019-01-01 15:30:00' 입니다. datetime의 timedelta를 이용하여 1분을 증가시켜주었습니다. += 연산을 -= 으로 바꿔주시면 1분이 감소된 데이트타임을 반환해줍니다. timedelta의 파라미터로는 minutes, hour, day, week, month 등이 있습니다. 여러분들이 증감해주고 싶은 파라미터로 위 함수를 수정해서 사용하시면 됩니다.



시간관련 함수가 더 생각이 나거나 구현을 하게된다면 이 포스팅에 추가하도록 하겠습니다.

이상으로 포스팅을 마치겠습니다.



레퍼런스

[1] 유닉스 시간 

[2] 파이썬 docs

