## Body - Updates

### Update replacing with PUT
HTTP의 put라는 것을 통하여 객체를 수정할 수 있도록 한다.

```
from typing import Union

from fastapi import FastAPI
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: Union[str, None] = None
    description: Union[str, None] = None
    price: Union[float, None] = None
    tax: float = 10.5
    tags: list[str] = []


items = {
    "foo": {"name": "Foo", "price": 50.2},
    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},
    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []},
}


@app.get("/items/{item_id}", response_model=Item)
async def read_item(item_id: str):
    return items[item_id]


@app.put("/items/{item_id}", response_model=Item)
async def update_item(item_id: str, item: Item):
    update_item_encoded = jsonable_encoder(item)
    items[item_id] = update_item_encoded
    return update_item_encoded
```

@app.put 을 통해 객체에 대한 정보를 바꿔쓸 수 있다.

### Warning about replacing

```
{
    "name": "Barz",
    "price": 3,
    "description": None,
}
```

tax 필드에 대한 값을 지정하지 않아서 default value인 10.5가 들어간다.

### Partial updates with PATCH

HTTP의 PATCH를 사용해서 사용자가 필요한 데이터만 수정하고 나머지는 그대로 유지할 수 있게 한다.

```
PUT에 비해 PATCH는 인지도가 낮다. 흔히 PUT이 많이 사용되며, 부분적 업데이트에서도 사용된다. 사용하는것은 자유지만, FastAPI는 어떠한 제한을 도입하지 않았다고 한다.
```

### Using Pydantic's exclude_unset parameter

부분적 업데이트가 필요하면 Pydantic's model의 dict()에 있는 exclude_unset을 사용한다.

```
from typing import Union

from fastapi import FastAPI
from fastapi.encoders import jsonable_encoder
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: Union[str, None] = None
    description: Union[str, None] = None
    price: Union[float, None] = None
    tax: float = 10.5
    tags: list[str] = []


items = {
    "foo": {"name": "Foo", "price": 50.2},
    "bar": {"name": "Bar", "description": "The bartenders", "price": 62, "tax": 20.2},
    "baz": {"name": "Baz", "description": None, "price": 50.2, "tax": 10.5, "tags": []},
}


@app.get("/items/{item_id}", response_model=Item)
async def read_item(item_id: str):
    return items[item_id]


@app.patch("/items/{item_id}", response_model=Item)
async def update_item(item_id: str, item: Item):
    stored_item_data = items[item_id]
    stored_item_model = Item(**stored_item_data)
    update_data = item.dict(exclude_unset=True)
    updated_item = stored_item_model.copy(update=update_data)
    items[item_id] = jsonable_encoder(updated_item)
    return updated_item
```

### Using Pydantic's update parameter

sotred_item_model.copy(update=update_data) 에서 update는 Pydantic에서 제공한다.

- PATCH를 PUT대신 사용
- 저장된 데이터를 찾음
- Pydantic model에 저장된 데이터를 넣음
- exclude_unset 을 이용하여 dict을 default value를 제외하고 생성
- 위의 Pydantic model의 Copy를 이용하여 속성값들을 부분적 업데이트
- jsonable_encoder를 이용하여 DB에 저장할 수 있는 자료형으로 변경
- DB에 저장
- 수정된 객체를 반환