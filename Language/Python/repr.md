> ### **str() 과 repr() 함수**
> - str()과 repr()은 모두 객체를 문자열로 반환하는 함수이다.
> - str() 은 **비공식적**인 문자열을 출력
> - repr() 은 **공식적**인 문자열을 출력 (시스템에서 인식가능)
>
> | 구분        | str()                     | repr()                     |
|-------------|---------------------------|----------------------------|
| 성격        | 비공식적인 문자열을 출력  | 공식적인 문자열을 출력     |
| 사용 목적   | 사용자가 보기 쉽도록      | 문자열로 객체를 다시 생성  |
| 누구를 위해 | 프로그램 사용자(end user) | 프로그램 개발자(developer) |

## 숫자
~~~
a = 123
str(a)
~~~
'123'
~~~
a = 123
repr(a)
~~~
'123'

## 문자열
~~~
a = "Hello World !"
print(str(a))
~~~
'Hello World !'
~~~
a = "Hello World !"
repr(a)
~~~
"'Hello World !'"

## 날짜

~~~
import datetime
~~~
~~~
# str()
a = datetime.datetime(2022, 1, 1)
str(a)
~~~
'2022-01-01 00:00:00'
~~~
# repr()
a = datetime.datetime(2022, 1, 1)
repr(a)
~~~
'datetime.datetime(2022, 1, 1, 0, 0)'

## 문자열을 객체로 변환 - eval()

~~~
a = "Hello World !"
b = str(a)
~~~
~~~
eval(b)
~~~
SyntaxError

~~~
a = "Hello World !"
b = repr(a)
~~~
~~~
eval(b)
~~~
'Hello World !'

~~~
a = datetime.datetime(2022, 1, 1)
b = str(a)
~~~
~~~
eval(b)
~~~
SyntaxError: leading zeros in decimal integer literals are not permitted; use an 0o prefix for octal integers
~~~
a = datetime.datetime(2022, 1, 1)
b = repr(a)
~~~
~~~
eval(b)
~~~
datetime.datetime(2022, 1, 1, 0, 0)

