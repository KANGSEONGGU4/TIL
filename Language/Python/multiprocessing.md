> ### multiprocessing
>  - `multiprocessing` 멀티 프로세스를 활용하여 2가지 또는 그 이상의 일을 동시에 실행할 수 있게 하는 표준 모듈
>  - multiprocessing 모듈은 쓰레드 대신 **다중 프로세스를 만들어** 병렬로 동작

#### 스레드(thread) vs. 멀티프로세싱(multiprocessing)
파이썬에서 병렬처리를 구현하는 방식은 멀티 쓰레드를 사용하거나 멀티 프로세스를 사용하는 두가지 방법이 있습니다.

**_스레드(thread) 특징_**
- 스레드는 가볍지만 cpu 계산 처리를 하는 작업에는 한번에 하나의 쓰레드에서만 작동함
- cpu 작업이 적고 **네트워크 통신** 또는 **파일 읽고 쓰기와 같은 작업 (I/O)** 이 많은 병렬 처리 프로그램에서 효과적

**_멀티프로세싱(multiprocedssing) 특징_**
- 멀티 프로세서와 별개의 메모리를 사용하여 완전히 독립하여 병렬 프로그래밍이 가능
- 여러 개의 CPU가 있는 **멀티코어 환경**에서 **CPU 수 만큼 작업을 나누어 실행** 가능
- 프로세스는 각자가 고유한 메모리 영역을 가지기 때문에 **더 많은 메모리를 필요**로 하지만,
- 각각 프로세스에서 병렬로 cpu 작업을 할 수 있고 이를 이용해 **여러 장비에서 동작**하는 분산 처리 프로그래밍도 구현이 가능

~~~
import multiprocessing
import time
~~~
#### multiprocessing 을 사용하지 않을 경우
~~~
# 0부터 50,000,000 까지의 합을 구하는 프로그램
def work(id, start, end, result):
    total = 0
    for i in range(start, end):
        total += i
    result.append(total)
    return
~~~
~~~
if __name__ == "__main__":
    start = time.time()
    
    START, END = 0, 50000000
    result = list()
    
    # 싱글 프로세스 2번 실행
    for i in range(2):
        work(1, START, END, result)
        print(f'{i+1} 번째 실행')
        
    
    time_elapsed1 = round(time.time() - start, 2)
    print(time_elapsed1, ' 초 경과')
    print(f"합계 결과: {sum(result)}")
~~~
1 번째 실행   
2 번째 실행   
4.6  초 경과   
합계 결과: 2499999950000000   

#### multiprocessing 을 사용할 경우
~~~
if __name__ == "__main__":
    start = time.time()
    
    START, END = 0, 50000000
    result = list()
    
    procs = []
    for i in range(2):
        # 프로세스 수만큼 코어 할당
        p = multiprocessing.Process(target=work, args=(i, START, END, result))
        p.start()
        procs.append(p)
        print(f'{i+1} 번째 실행')

    for p in procs:
        p.join()  # 프로세스가 모두 종료될 때까지 대기
        
        
    time_elapsed2 = round(time.time() - start, 2)
    speed_up = round(time_elapsed1/time_elapsed2, 1)
    print(time_elapsed2, ' 초 경과')
    print(speed_up, ' 배 속도 향상')
    print(f"합계 결과: {sum(result)}")
~~~
1 번째 실행   
2 번째 실행   
0.1  초 경과   
44.2  배 속도 향상   
합계 결과: 0