## 소켓(socket) 과 포트(port) 란?

**소켓(socket)** 이란 소켓이란 소프트웨어로 작성된 다른 컴퓨터와 네트워크를 통해 **데이터를 송수신하기 위한 창구** 역할을 하는 통신 접속점입니다. <br>
(ex. 소켓을 구성한다는 것은 이웃과 연락할 수 있는 _**전화기**_ 를 설치하는 것과 비슷한 개념입니다.)

**포트(port)** 란 네트워크 상에서 통신하기 위해서 호스트 내부적으로 프로세스가 할당받아야 하는 고유한 숫자입니다. <br>
하나의 소켓은 여러개의 포트를 할당 받을 수 있습니다. <br>
(ex. 포트는 설치된 전화기로 연락하기 위해 필요한 특정한 _**이웃에게 연결되어 있는 번호**_ 입니다.)  <br>



> ### socket
>  - socket은 파이썬으로 **TCP(Transmission Control Protocol) 서버/클라이언트 프로그램**을 작성할 때 사용하는 표준 라이브러리
>  - socket 의 TCP에 대한 소켓 API 호출 순서와 데이터 플로우

## server
~~~
import socket


# 접속할 서버 주소입니다. 여기에서는 localhost를 사용합니다.
HOST = '127.0.0.1'
# 클라이언트 접속을 대기하는 포트 번호입니다.
PORT = 9999


# 소켓 객체를 생성합니다.
# 주소 체계(address family)로 IPv4, 소켓 타입으로 TCP 사용합니다.
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)


# 포트 사용중이라 연결할 수 없다는
# WinError 10048 에러 해결를 위해 필요합니다.
server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)


# bind 함수는 소켓을 특정 네트워크 인터페이스와 포트 번호에 연결하는데 사용됩니다.
# HOST는 hostname, ip address, 빈 문자열 ""이 될 수 있습니다.
# 빈 문자열이면 모든 네트워크 인터페이스로부터의 접속을 허용합니다.
# PORT는 1-65535 사이의 숫자를 사용할 수 있습니다.
server_socket.bind((HOST, PORT))

# 서버가 클라이언트의 접속을 허용하도록 합니다.
server_socket.listen()
print('서버가 실행되었습니다.')

# accept 함수에서 대기하다가 클라이언트가 접속하면 새로운 소켓을 리턴합니다.
client_socket, addr = server_socket.accept()

# 접속한 클라이언트의 주소입니다.
print('접속한 클라이언트 주소입니다.')
print('Connected by', addr)



# 무한루프
while True:

    # 클라이언트가 보낸 메시지를 수신하기 위해 대기합니다.
    data = client_socket.recv(1024)

    # 빈 문자열을 수신하면 루프를 중지합니다.
    if not data:
        break


    # 수신받은 문자열을 출력합니다.
    print('Received from', addr, data.decode())

    # 받은 문자열을 다시 클라이언트로 전송해줍니다.(에코)
    client_socket.sendall(data)


# 소켓을 닫습니다.
client_socket.close()
server_socket.close()
~~~

## client

~~~
import socket


# 서버의 주소입니다. hostname 또는 ip address를 사용할 수 있습니다.
HOST = '127.0.0.1'
# 서버에서 지정해 놓은 포트 번호입니다. 
PORT = 9999


# 소켓 객체를 생성합니다. 
# 주소 체계(address family)로 IPv4, 소켓 타입으로 TCP 사용합니다.  
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)


# 지정한 HOST와 PORT를 사용하여 서버에 접속합니다. 
client_socket.connect((HOST, PORT))

# 메시지를 전송합니다. 
client_socket.sendall('안녕!'.encode())

# 메시지를 수신합니다. 
data = client_socket.recv(1024)
print('Received', repr(data.decode()))

# 소켓을 닫습니다.
client_socket.close()