> ### threading
>  - `threading` 은 스레드를 이용하여 한 프로세스에서 **2가지 이상의 일을 동시에 실행**할 수 있게 하는 표준 모듈
>  - 파이썬은 기본적으로 싱글 스레드에서 순차적으로 동작함
>  - 병렬 처리를 위해서는 별도 작업이 필요함
>  - 활용 분야 
>    - 대용량 데이터의 처리시간을 줄이기 위해 **데이터를 분할하여 병렬로 처리**
>    - 애플리케이션에서 **다중 네트워크 통신**을 할 때
>    - 여러 **클라이언트의 요청을 동시에 처리**하는 서버를 개발할 때

~~~
from threading import Thread
import time
~~~

#### threading 을 사용하지 않을 경우

~~~
# 0부터 10,000,000 까지의 합을 구하는 프로그램
def work(id, start, end, result):
    total = 0
    for i in range(start, end):
        total += i
    result.append(total)
    return

if __name__ == "__main__":
    start = time.time()
    
    START, END = 0, 10000000
    result = list()
    th1 = Thread(target=work, args=(1, START, END, result))   # 싱글 스레드
    
    th1.start()
    th1.join()
    
    th1_elapsed = round(time.time() - start, 2)
    print(th1_elapsed, ' 초 경과')
    print(f"합계 결과: {sum(result)}")
~~~
0.46  초 경과   
합계 결과: 49999995000000

~~~
# 0부터 10,000,000 까지의 합을 구하는 프로그램
def work(id, start, end, result):
    total = 0
    for i in range(start, end):
        total += i
    result.append(total)
    return

if __name__ == "__main__":
    start = time.time()
    
    START, END = 0, 10000000
    result = list()
    th2 = Thread(target=work, args=(8, START, END, result))   # 멀티 스레드
    
    th2.start()
    th2.join()
    
    th2_elapsed = round(time.time() - start, 2)
    speed_up = round(th1_elapsed/th2_elapsed, 1)
    print(th2_elapsed, ' 초 경과')
    print(speed_up, ' 배 속도 향상')
    print(f"합계 결과: {sum(result)}")
~~~
0.45  초 경과   
1.0  배 속도 향상   
합계 결과: 49999995000000