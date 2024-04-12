## JSON 호환 가능 인코더
### jsonable_encoder 사용

```
from datetime import datetime
from typing import Union

from fastapi import FastAPI
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel

fake_db = {}


class Item(BaseModel):
    title: str
    timestamp: datetime
    description: Union[str, None] = None


app = FastAPI()


@app.put("/items/{id}")
def update_item(id: str, item: Item):
    json_compatible_item_data = jsonable_encoder(item)
    fake_db[id] = json_compatible_item_data
```

Pydantic 모델을 dict 로, datetime 형식을 str로 변환

이렇게 호출한 결과는 파이썬 표준인 json.dumps()로 인코딩 