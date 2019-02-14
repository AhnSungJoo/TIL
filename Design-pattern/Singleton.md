## singleton
- 디자인 패턴 중 하나   
- 인스턴스는 한 번만 생성된다.   
- 아래의 코드에서 customlogger 클래스에 metaclass를 설정해줌으로써 인스턴스를 한 번만 생성하게 한다.    
- 인스턴스를 한 번만 생성한다는 것은 처음 인스턴스를 생성할때만 __init__ 을 호출하고 그 이후 인스턴스를 생성해도 __init__을 호출하지 않는다 
- 이래의 코드에서 logger = CustomLogger.__call__()에서 __call__ 을 호출함으로써 __init__도 호출된다. 


아래의 코드는 python에 logger 클래스를 커스텀 한 코드이다. 
~~~
import logging
import os


class SingletonType(type):
    def __call__(cls, *args, **kwargs):
        try:
            return cls.__instance
        except AttributeError:
            cls.__instance = super(SingletonType, cls).__call__(*args, **kwargs)
            return cls.__instance

class CustomLogger(object, metaclass=SingletonType):
    _logger = None

    def __init__(self, level_name, format_msg, dir_name="./logs/", file_name='.log'):
        """
            Singleton class
            Only first time call __init__ method

        """
        print("init")
        self._logger = logging.getLogger()
        self._logger.setLevel(self.set_level(level_name))
        self.formatter = logging.Formatter(format_msg)
        self.dirname = dir_name
        if not os.path.isdir(self.dirname):
            os.mkdir(self.dirname)
        fileHandler = self.set_filehandler(file_name)
        self.add_handler(fileHandler)

    def add_handler(self, handler_name):
        self._logger.addHandler(handler_name)

    def del_handler(self, handler_name):
        self._logger.removeHandler(handler_name)
        
    def print_info(self, msg):
        self._logger.info(msg)

logger = CustomLogger.__call__()
logger.print_info("hi")   


~~~~
-----
레퍼런스    
[1] http://snowdeer.github.io/python/2017/11/18/python-custom-logging-class/   
[2] https://dragon82.tistory.com/48   
[3] https://ourcstory.tistory.com/105
