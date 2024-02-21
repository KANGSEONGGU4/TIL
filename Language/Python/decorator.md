> ## 데코레이터 (Decorator)
> - 'decorate'는 '꾸미다, 장식하다'라는 뜻으로 함수를 꾸며주는 함수.
> - 함수를 인수로 받는 클로저
> - @를 이용한 어노테이션으로 사용
> - 사용되는 곳
>   - 반복되는 작업을 여러 함수에 적용할 경우
>   - 기존 함수를 수정하지 않고 추가 기능을 구현하고 싶을 경우

<br>

    import time

    def func1(a, b):
        start = time.time()
        print("함수가 실행됩니다.")
    
        val = a + b
    
        end = time.time()
        print("함수 수행시간: %f 초" % (end-start))
    
        return val

    if __name__ == "__main__":
        result = func1(1, 2)
        print(result)

함수가 실행됩니다.   
함수 수행시간: 0.000791 초   
3   

    def func2(a, b):
        start = time.time()
        print("함수가 실행됩니다.")
    
        val = a * b
    
        end = time.time()
        print("함수 수행시간: %f 초" % (end-start))
    
        return val

    if __name__ == "__main__":
        result = func2(1, 2)
        print(result)

함수가 실행됩니다.   
함수 수행시간: 0.001003 초   
2   

### 데코레이터 만들기

~~~
def func1(a, b):
    val = a + b   
    return val

def func2(a, b):
    val = a * b   
    return val
~~~
~~~
''' 실행 시간 측정 데코레이터 '''
def elapsed(func):                                     # 함수를 인풋으로 받는다.
    def wrapper(a, b):
        print('함수가 실행됩니다.')
        start = time.time()
        result = func(a, b)                            # 함수 실행
        end = time.time()
        print("함수 수행시간: %f 초" % (end - start))  # 함수 수행시간
        return result                                  # 함수 실행 결과 반환
    return wrapper
~~~
~~~
if __name__ == "__main__":
    deco1 = elapsed(func1)
    result = deco1(1,2)
    print(result)
~~~
함수가 실행됩니다.   
함수 수행시간: 0.000001 초   
3   

~~~
if __name__ == "__main__":
    deco2 = elapsed(func2)
    result = deco2(1,2)
    print(result)
~~~

함수가 실행됩니다.   
함수 수행시간: 0.000001 초   
2   

~~~
@elapsed
def func1(a, b):
    val = a + b   
    return val

@elapsed
def func2(a, b):
    val = a * b   
    return val
~~~
~~~
if __name__ == "__main__":
    result = func1(1,2)
    print(result)
~~~
함수가 실행됩니다.   
함수 수행시간: 0.000001 초   
3   

~~~
if __name__ == "__main__":
    result = func2(1,2)
    print(result)
~~~
함수가 실행됩니다.   
함수 수행시간: 0.000001 초   
2   