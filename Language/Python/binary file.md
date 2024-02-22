> ### **바이너리 파일 (Binary file)** 
> - 바이너리 파일이란 ‘0’ 과 ‘1’ 을 이용한 **2진수 데이터** 만으로만으로 인코딩된 파일
> - 사람이 직접 읽을 수 없다
> - 데이터를 효율적으로 처리, 저장, 실행 등을 목적으로 만들어진 파일
> - 장점
>    - 데이터를 처리하고 전송하는데 일반적으로 비용이 적게 든다.
>    - 텍스트 파일에 비해서 데이터 처리 속도가 빠르다.
>    - 데이터 저장 공간도 적게 듦
> - 대표적인 확장자 : exe, dll, zip, rar, mp3, mpg, jpg, png 등

<br>

> ### **Base64 인코딩**
> - 다양한 통신채널 (HTML, 이메일 등) 을 통해 **바이너리 데이터**를 **안전하게 전송**할 수 있게 하는 방법
> - ASCII, Unicode 인코딩과 함께 실생활에서도 많이 사용되는 인코딩 방법
> - ASCII (8bit) 인코딩은 프로토콜,시스템마다 다르게 해석되어 데이터가 왜곡될 여지가 있기 때문에 적합하지 않음
> - XML이나 HTTP 프로토콜에서도 특수문자 파싱 문제를 해결할 수 있는 수단
> - 64 진법은 ASCII문자들을 모두 표현할 수 있는 가장 작은 진법
>    - `문자열 입력` -> `ASCII/Binary (8bit)` -> `6bit cut` -> `base64`
~~~
import base64
string = 'Life is too short, We need Python !'
encoded = base64.b64encode(string)
~~~
TypeError: a bytes-like object is required, not 'str'
~~~
# ascii 인코딩
bstring = string.encode('ascii')
print(bstring)
~~~
b'Life is too short, We need Python !'
~~~
# base64 인코딩
encoded = base64.b64encode(bstring)
print(encoded)
~~~
b'TGlmZSBpcyB0b28gc2hvcnQsIFdlIG5lZWQgUHl0aG9uICE='
~~~
# base64 디코딩
decoded = base64.decodebytes(encoded)
print(decoded)
~~~
b'Life is too short, We need Python !'
~~~
# ascii 디코딩
decoded_str = decoded.decode('ascii')
print(decoded_str)
~~~
Life is too short, We need Python !