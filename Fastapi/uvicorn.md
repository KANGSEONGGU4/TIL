## fastapi

- python web framework
- api를 만들 수 있고, python 3.6버전 이상에서 적용 가능

### 1) 주요한 특징
- 데이터 타입을 엔드포인트로 명시하지 않아도 된다(알아서 알맞게 바꾸어 준다)
- Uvicorn ASGI Server 를 사용한다

## ASGI이란
- Asynchronous Server Gateway Interface의 약자
- 비동기 web server를 의미함
    - async / await 구문을 사용

## 비동기 방식이란
- 비동기 방식은 DB나 API 연동 과정에서 발생하는 대기 시간을 낭비하지 않고, CPU가 다른 작업을 할 수 있도록 하는 방식

### 2) 장점
- 빠르다, 퍼포먼스가 좋다
- 코드가 간단하다
- 버그가 적다

## uvicorn

- lightweight(매우 가벼운) ASGI 서버
- fastapi framework만으로는 웹 개발을 할 수 없고, ASGI와 호환되는 웹 서버가 필요함
- 비동기 방식이 가능한 python web server framework(Fastapi가 대표적)와 - application 간의 표준 interface를 제공함
- 배포에 별도의 준비가 필요 없음


### endpoint란
- 특정 서비스의 client 들이 접근할 수 있는 웹 주소 (URL)을 의미