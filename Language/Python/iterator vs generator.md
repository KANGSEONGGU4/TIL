## 이터레이터와 제너레이터

제너레이터는 이터레이터와 서로 상당히 비슷하다는 것을 알 수 있다.   
클래스를 이용하여 이터레이터를 작성하면 좀 더 복잡한 행동을 하게 할 수 있다.   
이와는 달리 제너레이터 표현식 등을 이용하면 간단하게 이터레이터를 만들 수 있다.   
따라서 이터레이터의 성격에 따라 클래스로 만들 것인지 제너레이터로 만들 것인지를 선택해야 한다.   
간단한 경우라면 제너레이터 함수나 제너레이터 표현식을 사용하는 것이 가독성이나 유지보수 측면에서 유리하다.

~~~
import time


def longtime_job():
    print("job start")
    time.sleep(1)
    return "done"


list_job = iter([longtime_job() for i in range(5)])
print(next(list_job))
~~~
job start   
job start   
job start   
job start   
job start   
done
~~~
import time


def longtime_job():
    print("job start")
    time.sleep(1)
    return "done"


list_job = (longtime_job() for i in range(5))
print(next(list_job))
~~~
job start   
done   

>   모든 함수를 한꺼번에 실행하는 것이 아니라 필요할 때만 실행하는 방식으로 바뀌게 된다.   
>   이러한 방식을 '느긋한 계산법(lazy evaluation)'이라 부른다.

