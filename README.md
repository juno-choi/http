# IP

* Internet Protocol (인터넷 프로토콜)

    1. 복잡한 인터넷 망에서 client가 지정한 IP 주소(IP Address)로 데이터를 전달하는 역할

    2. 패킷(Packet)이라는 통신 단위로 데이터 전달

        `packet` [출발지IP][목적지IP][기타][전송데이터] 의 규칙으로 전송


* IP 프로토콜의 한계

    1. `비연결성`

        패킷을 받을 대상이 없거나 받을 수 없는 서비스 불능 상태여도 패킷은 일방적으로 전송돼고 전송한 client는 전송이 성공한 것만 확인할 수 있을 뿐 상대방이 성공적으로 전송한 내용을 받았는지를 확인할 수 없다.

    2. `비신뢰성`

        위 비연결성, 물리적인 이유로 인한 중간의 패킷의 손실 가능성

        패킷의 전송 속도차나 환경차이에 의한 순서의 확실성이 불확실함

    3. `프로그램 구분`

        하나의 IP에서 여러개의 어플리케이션이 동작하고 있을때 client가 원하는 어플리케이션에 데이터를 전송할 수 없음

# 인터넷 프로토콜 스택의 4계층

<img src="https://blog.kakaocdn.net/dn/nOzzX/btq3mdwSmrr/4cIU4VRzFpqLv0LwaKL5m1/img.png" alt="protocol"></img>

`애플리케이션 계층`

1. Application Layer(응용 계층), Presentation Layer(표현 계층), Session Layer(세션 계층)으로 구분할 수도 있다.
2. 해당 계층은 사용자가 실제로 사용하면서 직접 서비스를 경험하거나 os나 protocol이 간접적으로 서비스를 사용하는 계층

`전송 계층`

1. IP의 문제점을 보완하기 위해 전송에 필요한 계층
2. 네트워크 프로토콜 내에서 송신자와 수시잔의 연결하는 통신 서비스를 제공하는 계층

`인터넷 계층`

1. 네트워크 패킷을 IP Address를 통해 지정된 목적지로 전송하기위한 계층

`네트워크 인터페이스 계층`

1. 네트워크의 하드웨어를 제어하는 계층

<img src="https://blog.kakaocdn.net/dn/chAO9U/btq3kkJ0hd2/v1GGDkhScqXCnZXaEkd46K/img.png" alt="protocol"></img>

위 그림으로 다시 설명하자면 Hello, world라는 메세지를 애플리케이션 계층에 해당하는 chrome application에서 socket library를 통하여 OS에 해당하는 전송 계층의 TCP로 전달하여 TCP 정보를 생성하고 다시 인터넷 계층의 IP로 정보가 전달되어 IP 패킷에 정보를 담아 트워크 인터페이스 계층으로 전달되어져 LAN을 통해 데이터가 전송되어진다.


# TCP
<img src="https://blog.kakaocdn.net/dn/xvO9P/btq3mpjxJXn/tLb8gOFeTr3O57ymSK8zc0/img.png" alt="protocol"></img>
* Transmission Control Protocol (전송 제어 프로토콜)

    1. `연결지향`

        3 way handshake를 통해 client와 데이터를 전송 받을 server의 상태를 확인하여 데이터를 전송

        실제로 물리적으로 연결된 상태는 아니며 논리적인 연결 상태

    2. `데이터 전달 보증`

        데이터를 전송했을 때 데이터를 받았다는 server의 응답을 반환받을 수 있다.

    3. `순서 보장`

        데이터의 패킷의 순서가 달라졌을 때 순서가 틀린 부분부터 데이터를 모두 버리고 재전송을 요청


`3 way handshake`

1. client가 데이터를 전송할때 목적지 server가 현재 데이터를 받을 수 있는 상태인지 먼저 확인
2. 목적지 server에서 데이터를 받을 수 있는 상태일 경우 client로 데이터를 전송해도 좋다고 전송, 또한 목적지 server에서도 client로 데이터를 주고 받을 수 있는 상태인지 확인
3. client도 server에 데이터를 주고 받을 수 있는 상태인 것을 확인하여 전송
4. client에서 목적지 server로 데이터를 전송

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqD6vv%2Fbtq3mvYbGWR%2FIJsh9N20Q9p2DTtr0R9tHk%2Fimg.png" alt="3 way handshake"></img>

`SYN` 접속 요청
`ACK` 요청 수락

# UDP

* User Datagram Protocol (사용자 데이터그램 프로토콜)

    1. IP와 거의 같고 PORT와 체크썸만 추가
    2. 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
    3. TCP는 검증하는 프로세스가 많아 UDP가 훨씬 빠름
    4. 기능이 거의 없지만 사용자가 application에서 수정하여 사용할 수 있어 TCP보다 유연하게 사용 가능

# PORT

* 하나의 client가 여러 server와 동시에 통신

    1. IP를 집주소라고 생각한다면 port는 해당 집에서 살고 있는 사람으로 생각하면 좋을거 같다. IP 주소를 통해 집을 찾고 port번호를 통해 해당 사람을 찾아서 데이터를 전송해주는 것
    2. 0 ~ 65535 까지 사용이 가능하지만 0 ~ 1023은 잘 알려진 port로 사용하지 않는 것이 좋다.

# DNS

* Dmain Name System (도메인 네임 시스템)
    1. ip의 단점을 보완
        1. ip는 기억하기 어렵다
        2. ip는 변경될 수 있다.
    2. goole.com -> 192.168.1.2로 DNS server에 등록해놓으면 도메인명으로만 ip 주소로 접근할 수 있다.
    



`출처` https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/lecture/61370?tab=curriculum