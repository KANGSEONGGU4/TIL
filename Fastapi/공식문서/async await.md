>   ## 기술적 세부사항
>   최신 파이썬 버전은 async 와 await 문법과 함께 "코루틴"이라고 하는 것을 사용하는 "비동기 코드"를 지원합니다.

- 비동기 코드
- async 와 await
- 코루틴

## 비공기 코드

수행 시간의 대부분이 I/O 작업을 기다리는데에 소요되기 때문에, "I/O에 묶인" 작업이라고 불립니다.

이것은 "비동기"라고 불리는데 컴퓨터 / 프로그램이 작업 결과를 가지고 일을 수행할 수 있도록, 느린 작업에 "동기화"되어 아무것도 하지 않으면서 작업이 안료될 정확한 시점만을 기다릴 필요가 없기 때문입니다.

이 대신에, "비동기" 시스템에서는, 작업은 일단 완료되면, 컴퓨터 / 프로그램이 수행하고 있는 일을 완료하고 이후 다시 돌아와서 그것의 결과를 받아 이를 사용해 작업을 지속할 때까지 잠시 대기할 수 있습니다.

"동기"는 컴퓨터 / 프로그램이 상이한 작업들간 전환을 하기 전에 그것이 대기를 동반하게 될지라도 모든 순서를 따르기 때문에 "순차"라는 용어로도 흔히 불립니다.

## async 와 await

최신 파이썬 버전에는 비동기 코드를 정의하는 매우 직관적인 방법이 있습니다. 이는 이것을 평범한 "순차적" 코드로 보이게 하고, 적절한 순간에 당신을 위해 "대기"합니다.

연산이 결과를 전달하기 전에 대기를 해야하고 새로운 파이썬 기능들을 지원한다면, 이렇게 코드를 작성할 수 있습니다.
```
burgers = await get_burgers(2)
```

여기서 핵심은 await입니다. 이것은 파이썬에게 burgers 결과를 저장하기 이전에 get_burgers(2) 의 작업이 완료되기를 기다리라고 말합니다. 이로 인해, 파이썬은 그동안 다른 작업을 수행해도 된다는 것을 알게될 것입니다.

await 가 동작하기 위해, 이것은 비동기를 지원하는 함수 내부에 있어야 합니다. 이를 위해서 함수를 async def를 사용해 정의하기만 하면 됩니다.

```
async def get_burgers(number: int):
    # Do some asynchronous stuff to create the burgers
    return burgers
```

```
# This is not asynchronous
def get_sequential_burgers(number: int):
    # Do some sequential stuff to create the burgers
    return burgers
```

async def를 사용하면, 파이썬은 해당 함수 내에서 await 표현에 주의해야한다는 사실과, 해당 함수의 실행을 "일시정지"하고 다시 돌아오기 전까지 다른 작업을 수행할 수 있다는 것을 알게됩니다.

async def f 함수를 호출하고자 할 때, "대기"해야합니다. 따라서, 아래는 동자갛지 않습니다.
```
# This won't work, because get_burgers was defined with: async def
burgers = get_burgers(2)
```
-------------------------------------
따라서, awiat f를 사용해서 호출할 수 있는 라이브러리를 사용한다면, 다음과 같이 async def를 사용하는 경로 작동 함수를 생성해야 합니다.

```
@app.get('/burgers')
async def read_burgers():
    burgers = await get_burgers(2)
    return burgers
```

### 코루틴

코루틴은 async def 함수가 반환하는 것을 칭하는 매우 고급스러운 용어일 뿐입니다. 파이썬은 그것이 시작되고 어느 시점에서 완료되지만 내부에 await가 있을 때마다 내부적으로 일시정지 될 수도 있는 함수와 유사한것이라는 사실을 알고있습니다.

그러나 async 및 await와 함께 비동기 코드를 사용하는 이 모든 기능들은 "코루틴"으로 간단히 요약됩니다.