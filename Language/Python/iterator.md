> ### **이터레이터 (Iterator)**
> - 집합에서 값을 **차례대로 꺼낼 수 있는 `객체(Object)`** 를 말합니다.
> - for 문을 순회할 수 있는 객체
> - 사용이유 ?
>   - 숫자가 아주 많을 경우 미리 만들어 놓는 것 보다 <br>
그때 그때 필요할 때 값을 뽑아 사용하고 싶을 경우가 대부분의 상황에서 효율적 (메모리 등)
> - **반복 가능 (Iterable) 객체**에만 사용 가능
>   - iter() 로 반복 가능 객체 변환
>   - next() 로 다음값 뽑기
> - 한번 반복하면 다시 사용될 수 없음

<br>

```
a = [1,2,3]
iterator = iter(a)
type(iterator)
```
list_iterator

    next(iterator)
1

    next(iterator)
2

    next(iterator)
3

    next(iterator)
StopIteration: 

    for i in iterator:
        print(i) # 아무것도 나오지 않는다.

