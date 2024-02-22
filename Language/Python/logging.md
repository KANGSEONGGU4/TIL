> ### logging
>  - 프로그램이 실행되는 동안 **일어나는 정보를 기록**하고 관리하는 로깅 모듈
>  - 로그는 파일뿐만 아니라 소켓, 이메일, 콘솔 등 다양한 방법으로 출력이 가능
>  - `print()` 와 차이점?
>    - 콘솔창에 문자열을 출력하는 print 문을 사용해서 기록을 남기는 방법도 있지만, 실행 기록을 관리하거나 분석 시에는 활용이 어려움
>    - `logging` 은 프로그램 진행 상황에 따라 로그를 레벨 별로 관리하거나 모듈 별 별도의 기록을 남기는 등의 작업이 가능 

~~~
def myfunc():
    print("함수가 시작되었습니다.")

myfunc()
~~~
함수가 시작되었습니다.
~~~
import logging

# 로그 생성
logger = logging.getLogger()

# 로그의 출력 기준 설정
logger.setLevel(logging.INFO)

# log 형식 지정
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# log 출력
stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)
logger.addHandler(stream_handler)

# log 파일 생성
file_handler = logging.FileHandler('sample1.log')
file_handler.setFormatter(formatter)
logger.addHandler(file_handler)

def myfunc():
    logger.info("함수가 시작되었습니다.")

myfunc()
~~~
2024-02-22 16:35:47,028 - root - INFO - 함수가 시작되었습니다.   

#### 로그 레벨 5단계
로그는 설정한 레벨 이상만 출력됩니다. <br>
예를 들어 핸들러나 로거의 로그 레벨을 'INFO'로 설정하면 DEBUG 로그는 출력되지 않고 INFO 이상의 로그만 출력합니다.

`DEBUG < INFO < WARNING < ERROR < CRITICAL`
- 1단계 DEBUG: 디버깅 목적으로 사용
- 2단계 INFO: 일반 정보를 출력할 목적으로 사용
- 3단계 WARNING: 경고 정보를 출력할 목적으로(작은 문제) 사용
- 4단계 ERROR: 오류 정보를 출력할 목적으로(큰 문제) 사용
- 5단계 CRITICAL: 아주 심각한 문제를 출력할 목적으로 사용

~~~
import logging

# 로그 생성
logger = logging.getLogger()

# 로그의 출력 기준 설정
logger.setLevel(logging.WARNING)

# log 형식 지정
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# log 출력
stream_handler = logging.StreamHandler()
stream_handler.setFormatter(formatter)
logger.addHandler(stream_handler)

# log 파일 생성
file_handler = logging.FileHandler('sample2.log')
file_handler.setFormatter(formatter)
logger.addHandler(file_handler)

def myfunc():
    logger.debug("DEBUG 로그입니다.")
    logger.info("INFO 로그입니다.")
    logger.warning("WARNING 로그입니다.")
    logger.error("ERROR 로그입니다.")
    logger.critical("CRITICAL 로그입니다.")

myfunc()
~~~
2024-02-22 16:36:09,736 - root - WARNING - WARNING 로그입니다.   
2024-02-22 16:36:09,736 - root - WARNING - WARNING 로그입니다.   
2024-02-22 16:36:09,740 - root - ERROR - ERROR 로그입니다.   
2024-02-22 16:36:09,740 - root - ERROR - ERROR 로그입니다.   
2024-02-22 16:36:09,742 - root - CRITICAL - CRITICAL 로그입니다.   
2024-02-22 16:36:09,742 - root - CRITICAL - CRITICAL 로그입니다.