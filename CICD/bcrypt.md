## bcrpt

단방향 암호화를 위해 만들어진 해시 함수이다.

즉, 복호화는 불가능

그렇다면 복호화가 불가능한데, 어떻게 기존의 비밀번호와 비교하여 옳은 지 판단할 수 있을까? 비밀번호 자체를 검증할 때는 입력받은 값을 암호화해서 저장된 암호화된 값과 비교해서 검증 할 수 있다.

## hash

임의의 길이를 갖는 임의의 데이터에 대해 고정된 길이의 데이터로 매핑하는 함수를 Hash 함수라고 하고, 이 함수의 결과물이 Hash 값이다.

기존에 이미 sha256과 같은 해시 함수들이 사용되고 있었으나, sha256과 같은 경우 암호화를 위해 설계된 것이 아니라 짧은 시간 내에 데이터를 빠르게 검색하기 위한 구조로 설계 되어있다.

따라서 빠른 속도가 장점이지만, 보안에는 취약하다. 또한 미리 해시 값들을 계산해놓은 테이블인 Rainbow table, 즉 Rainbow table attack이라는 해시 함수 반환 값을 역추적하는 해킹 방법으로 인한 보안의 취약점들이 존재한다.

bcrypt는 기존의 단방향 해시 함수들이 가지고 있는 취약점들을 보완하여 탄생했다.
단방향 해쉬 함수의 취약점들을 보안하기 위해 일반적으로 2가지 보완점들이 사용된다.

- salting
    - 실제 비밀번호 이외에 추가적으로 랜덤한 데이터 값을 더해 해시 값을 계산하는 방법을 말한다. 음식에 간을 치듯이, 유저가 어떤 비밀번호를 설정했든지 상관없이 거기에 난수까지 추가하여 해시함수에 집어넣는 것이다.

    - 즉 비밀번호의 복잡도를 키워 보안을 높이는 것이다. 이렇게 되면 비밀번호의 길이가 매우 길어지고, 비밀번호가 길수록 크래킹하는 데 필요한 연산시간이 늘어나게 되므로 해킹이 더욱 어려워지는 것이다.

- Key Stretching
    - 단방향 해시 값을 계산한 뒤, 그 해시 값을 해시하고, 또 해시하는 반복 과정을 말한다. 키 스트레칭을 적용하여 동일 장비에서 1초에 5번 정도만 비교할 수 있도록 한다. 즉, 기존 단방향 해시 알고리즘의 빠른 실행속도가 취약점이 됐던 것을 보안하기 위한 방법이다.