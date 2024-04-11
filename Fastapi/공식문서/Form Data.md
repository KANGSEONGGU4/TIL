## Form Data

```
from fastapi import FastAPI, Form
from typing_extensions import Annotated

app = FastAPI()


@app.post("/login/")
async def login(username: Annotated[str, Form()], password: Annotated[str, Form()]):
    return {"username": username}
```


HTML forms은 데이터를 조금 특별하게 encoding해서 보낸다. 이는 JSON과 다르다.

fast api는 이를 자동으로 변환해주어 적절하게 변수 매칭을 해준다.

