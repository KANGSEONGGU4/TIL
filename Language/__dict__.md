## __dict__ 용도

클래스 객체의 속성 정보를 확인하기 위해 사용

객체가 가진 여러가지 속성들을 딕셔너리 형태로 편하게 확인할 수 있다.

## __dict__ 활용 방법

객체의 변수를 dict형태로 변경할 수 있다

dictionary 형태로 만들어 두면, 편하게 속성 값들을 가져올 수 있다.

```
class Test:
    def __init__(self, name):
        self.name = name
        self.test_dict = {"a":1, "b":2}
        self.test_list = ["1", "2", "3"]

# Test 객체 생성		
test_object = Test("kangseonggu")

# __dict__ 메소드를 이용해보면 type이 dict인 것을 확인 할 수 있다.
print(type(test_object.__dict__)) # <class 'dict'>

# print 해보면, 객체에 선언한 변수들이 key,value로 들어간 것을 확인할 수 있다.
print(test_object.__dict__)  # {'name': 'kangseonggu', 'test_dict': {'a': 1, 'b': 2}, 'test_list': ['1', '2', '3']}

# dict 형태이기 때문에 key 값으로 조회시 바로 value를얻을 수 있다.
print(test_object.__dict__['name']) # kangseonggu

# 번외 : dictionary의 key, value를 얻을 수 있는 items() 로 dict로 재변경
print(test_object.__dict__.items()) # dict_items([('name', 'kangseonggu'), ('test_dict', {'a': 1, 'b': 2}), ('test_list', ['1', '2', '3'])])

print(type(test_object.__dict__.items())) # <class 'dict_items'>

object_dict = dict(x for x in test_object.__dict__.items()) # {'name': 'kangseonggu', 'test_dict': {'a': 1, 'b': 2}, 'test_list': ['1', '2', '3']}

print(type(object_dict)) # <class 'dict'>
```

