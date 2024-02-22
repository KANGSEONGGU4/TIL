> ### **제네레이터 (Generator)**
> - **이터레이터 (Iterator) 를 생성해주는 함수**
> - 사용이유 ?
>   - 함수가 하나의 고정된 값을 반환하는 것이 아닌 순차적으로 다른 값을 반환하기 원할 때
> - yield() 

```
def generator():
    yield 'a'
    yield 'b'
    yield 'c'

g = generator()
type(g)
```
generator

    next(g)
'a'

    next(g)
'b'

    next(g)
'c'

    next(g)
StopIteration:

## 제네레이터 사용 예시

~~~
def client_count(total_client):
    n = 1
    for num in range(total_client):
        print(f'{n} 번째 고객님 입장하십시오!')
        n += 1
        yield
~~~
~~~
mygen = client_count(3)
~~~
~~~
next(mygen)
~~~
1번째 고객님 입장하십시오!
~~~
next(mygen)
~~~
2번째 고객님 입장하십시오!
~~~
next(mygen)
~~~
3번째 고객님 입장하십시오!
~~~
next(mygen)
~~~
StopIteration
~~~
for i in mygen:
    print(i) # 아무것도 나오지 않는다
~~~
