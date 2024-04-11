## Extra Models

- input model 은 password를 포함
- output model 은 password를 포함하면 안된다.
- database model 은 hashed password를 포함

## Multiple models

```
from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: str | None = None


class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: str | None = None


class UserInDB(BaseModel):
    username: str
    hashed_password: str
    email: EmailStr
    full_name: str | None = None


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```

password를 일반적으로 다루기 위한 예시

## About **user_in.dict()

```
user_in = UserIn(username="kangseonggu", password="secret", email="kangseonggu@example.com")
```
- Pydantic model들은 dict() method가 있다.
    - return dict with the model's data

```
user_dict = user_in.dict()
```

### Unwrapping a dict

- ** 연산이 붙으면, python은 dictionary로 unwrap한다.

```
UserInDB(**user_dict)
```
```
UserInDB(
    username = "kangseonggu",
    password = "secret",
    email = "kangseonggu@example.com",
    full_name = None,
)
```
동일한 코드

## reduce duplication

```
from typing import Union

from fastapi import FastAPI
from pydantic import BaseModel, EmailStr

app = FastAPI()


class UserBase(BaseModel):
    username: str
    email: EmailStr
    full_name: Union[str, None] = None


class UserIn(UserBase):
    password: str


class UserOut(UserBase):
    pass


class UserInDB(UserBase):
    hashed_password: str


def fake_password_hasher(raw_password: str):
    return "supersecret" + raw_password


def fake_save_user(user_in: UserIn):
    hashed_password = fake_password_hasher(user_in.password)
    user_in_db = UserInDB(**user_in.dict(), hashed_password=hashed_password)
    print("User saved! ..not really")
    return user_in_db


@app.post("/user/", response_model=UserOut)
async def create_user(user_in: UserIn):
    user_saved = fake_save_user(user_in)
    return user_saved
```

- 이전에  선언한 코드에서 모델들은 너무 많은 데이터와 속성들을 중복으로 갖고 공유하고 있다. 이를 개선한 코드 예시다.
- base로 userbase를 갖은 채로 이를 상속받은 것이다.

## union or anyof

- 두개 이상의 type에 대해서는 union response 선언
    - response는 2개 이상

## list of models

```
from typing import List

from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()


class Item(BaseModel):
    name: str
    description: str


items = [
    {"name": "Foo", "description": "There comes my hero"},
    {"name": "Red", "description": "It's my aeroplane"},
]


@app.get("/items/", response_model=List[Item])
async def read_items():
    return items
```

## response with arbitrary dict

```
from typing import Dict

from fastapi import FastAPI

app = FastAPI()


@app.get("/keyword-weights/", response_model=Dict[str, float])
async def read_keyword_weights():
    return {"foo": 2.3, "bar": 3.4}
```