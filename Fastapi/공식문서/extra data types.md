## Extra Data Types 
일반적인 데이터타입인 int,float,str,bool과 달리 좀 더 복잡한 데이터를 다루는 챕터이다.

좀 더 복잡한 대신에 다음과 장점들을 갖고 있다.

- 에디터가 지원한다.
- 요청으로 해당 데이터가 들어오면 데이터 변환을 한다.
- 데이터 변환을 통해 응답에 반환할 수 있다.
- 데이터 검증이 가능
- 자동 문법검사와 문서화를 갖고 있다.

## Other data types

다음과 같은 추가 데이터타입들이 있다.

- UUID 
    - "Universally Unique Identifier”라고 하는 것인데, 전세계적으로 고유한 값이다.
    - 요청이나 응답에 대해서 str로 표현이 가능하다.
- datetime.datetime 
    - 날짜, 시간 표준이 ISO 8601 포맷으로 표현이 가능하다. 예를 들어서 - 2008-09-15T15:53:00+0:00처럼 말이다.
- datatime.date 
    - 마찬가지로 ISO 8601표준으로 사용이 가능하다. ex) 2008-09-15
- datatime.time 
    - 마찬가지로 ISO 8601표준으로 사용이 가능하다. ex) 14:23:55.003
- datetime.timedelta 
    - 요청이나 응답을 보낼때에는 float형태의 초로 표현할 수 있다.
- frozenset 
    - 요청이나 응답을 보낼때 set처럼 사용할 수 있다.
    - 요청으로 리스트를 읽는데, 중복된 값을 제거하고 set으로 바꿔버린다.
    - 응답에서는 set이 list로 바뀐다.
    - 스키마를 만들때는 set으로 만들어진다.
- byte 
    - 요청이나 응답에서는 str로 다뤄진다.
    - 문서화될 때에는 binary값으로 포맷된 str이 된다.
- Decimal 
    - 요청이나 응답에서 float로 다뤄진다.

```
from datetime import datetime, time, timedelta
from typing import Annotated
from uuid import UUID

from fastapi import Body, FastAPI

app = FastAPI()


@app.put("/items/{item_id}")
async def read_items(
    item_id: UUID,
    start_datetime: Annotated[datetime | None, Body()] = None,
    end_datetime: Annotated[datetime | None, Body()] = None,
    repeat_at: Annotated[time | None, Body()] = None,
    process_after: Annotated[timedelta | None, Body()] = None,
):
    start_process = start_datetime + process_after
    duration = end_datetime - start_process
    return {
        "item_id": item_id,
        "start_datetime": start_datetime,
        "end_datetime": end_datetime,
        "repeat_at": repeat_at,
        "process_after": process_after,
        "start_process": start_process,
        "duration": duration,
    }
```