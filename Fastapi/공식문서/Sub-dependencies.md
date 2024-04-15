## Sub-dependencies

### First dependency “dependable”

FastAPI는 종속성을 갖고 종속성함수 즉, 하위 종속성들을 저의하고 이를 처리해주는 것을 도와줍니다.

```
from typing import Annotated, Union

from fastapi import Cookie, Depends, FastAPI

app = FastAPI()


def query_extractor(q: Union[str, None] = None):
    return q


def query_or_cookie_extractor(
    q: Annotated[str, Depends(query_extractor)],
    last_query: Annotated[Union[str, None], Cookie()] = None,
):
    if not q:
        return last_query
    return q


@app.get("/items/")
async def read_query(
    query_or_default: Annotated[str, Depends(query_or_cookie_extractor)],
):
    return {"q_or_cookie": query_or_default}
```

read_query()는 query_or_cookie_extractor()의 의존성을 갖고, query_or_cookie_extractor()는 query_extractor()의 의존성을 갖습니다.


### Second dependency, “dependable” and “dependant”

query_or_cookie_extractor()함수는 read_query이 호출하고 의존성으로 엮어있는데, 이러한 의존성 함수를 dependable라고 합니다. 또한 이 의존성 함수는 다시 의존성 함수 query_extractor를 호출합니다.

### Using the same dependency multiple times

만약 여러 의존성 함수들이 하위 의존성 함수로 같은 함수의 값을 받는다면 FastAPI는 한 번 호출에 한 번 의존성 함수를 들립니다.

이러한 동작방식은 최초 하위 의존성 함수에 들릴 때, cache를 통해 값을 저장하고 리턴합니다. 그리고 모든 상위 의존성 함수에 값을 전달합니다.

만약 dependency를 사용하지 않고 해당 함수를 여러번 호출해야한다면, use_cache=False 구문을 통해 매개변수를 설정해줄 수 있습니다.

```
from typing import Annotated, Union

from fastapi import Cookie, Depends, FastAPI

app = FastAPI()


def query_extractor(q: Union[str, None] = None):
    return q


def query_or_cookie_extractor(
    q: Annotated[str, Depends(query_extractor)],
    last_query: Annotated[Union[str, None], Cookie()] = None,
):
    if not q:
        return last_query
    return q


@app.get("/items/")
async def read_query(
    query_or_default: Annotated[str, Depends(query_or_cookie_extractor)],
):
    return {"q_or_cookie": query_or_default}
```