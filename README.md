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
    
# URI
<img src="https://blog.kakaocdn.net/dn/uyjWy/btq3mhTCpOy/dBYTP97rxsBMc8qS5hxqF0/img.png" alt="3 way handshake"></img>
* Uniform Resource Identifier

    1. `Uniform` 리소스 식별하는 통일된 방식
    2. `Resource` 자원, URI로 식별할 수 있는 모든 것
    3. `Identifier` 다른 항목과 구분하는데 필요한 정보

    
* URL
  
    1. `Locator` 리소스가 있는 위치를 지정
    2. 대부분 우리가 웹 브라우저에서 사용하는 방식
    3. ex) http://www.example.com/serch?idx=12&page=1
    4. scheme://[userinfo@]host[:port][/path][?query][#fragment]
        - `scheme`
            1. 주로 프로토콜 사용
            2. 어떤 방식으로 자원에 접근할 것인가 하는 규칙 (http, https, ftp)
            3. http (80), https (443) 포트는 생략 가능
        - `userinfo`
            1. url에 사용자 정보를 포함해서 인증
            2. 거의 사용하지 않음
        - host
            1. 도메인명 또는 IP 주소
        - `port`
            1. 접속 포트
            2. 생략 가능
        - `path`
            1. 리소스 경로
            2. 대부분 계층적 구조를 가짐 ex) /order/item/book
        - `query`
            1. key=value 형태
            2. ?로 시작 &으로 추가
            3. query parameter 혹은 query string으로 불림
        - `fragment`
            1. html 내부 북마크 등에 사용
            2. server와 통신하는 정보는 아니고 html 내부에서 사용
* URN
    
    1. `Name` 리소스에 이름을 부여
    2. ex) book:isbn:72989
    
# 웹 브라우저 요청 흐름

* https://www.google.com:443/search?q=hello&hl=ko 의 요청메세지
    
        GET /search?q=hello&hl=ko
        HOST: www.google.com

* 요청에 대한 응답 메세지
        
        HTTP/1.1 200 OK
        Content-Type: text/html;charset=UTF-8
        Content-Length: 3423

        <html>
            <body> ... </body>
        </html>

# HTTP란

* HyperText Transfer Protocol

    1. 최초에는 HTML과 TEXT를 전송하기 위해 고안됨
    2. 현재는 image, 음성, 영상, 파일, json 등 거의 모든 형태의 데이터를 전송
    
    
* HTTP 역사
    1. HTTP/0.9 1991년 : GET만 지원, HTTP 헤더 지원하지 않음
    2. HTTP/1.0 1996년 : 메서드, 헤더 추가
    3. HTTP/1.1 1997년 : 가장 많이 사용되는 버전
    4. HTTP/2   2015년 : 성능 개선
    5. HTTP/3   진행중  : TCP 대신 UDP 사용 및 성능 개선  
    

# HTTP 특징
* 클라이언트 서버 구조
    1. request response 구조
    2. client와 server를 서로 분리한 `독립적` 구조이며 client는 요청을 보내고 server는 응답을 대기하면서 요청에 대한 결과를 만들어 응답한다.
    

* Stateful, Stateless
    1. Stateful 상태유지 프로토콜
        
        - client의 요청을 server 측면에서 항상 같은 server에서 요청을 받아 응답해야한다.
        - server가 중간에 장애가 나면 client를 다시 처음부터 다른 server에 요청을 해야한다.
       
    2. Stateless 무상태 프로토콜
        
        - client의 요청을 server 측면에서 아무 server나 요청을 받아 응답한다.
        - server가 중간에 장애가 나도 client는 다른 server를 사용하여 요청을 진행할 수 있다.
        - 무상태로 설계하는 측면이 서비스 확장에 유리 
        - 하지만 무상태로만 설계할 수 없는 경우가 존재
            1. 무상태 ex) 로그인이 필요 없는 단순한 서비스 소개 화면
            2. 상태 유지 ex) 로그인
                + 일반적으로 브라우저 쿠키와 서버 세션등을 사용하여 상태를 유지
                + 상태유지는 최소한만으로 사용
        - 필요한 값이 많아질 수록 전송해야하는 데이터도 많아짐
    
* connectionless (비 연결성)

        장점
  
        1. HTTP는 기본이 연결을 유지하지 않는 모델
        2. 1시간 동안 수천명이 서비스를 사용해도 실제 서버로 요청을 보내는 요청은 그 수에 비해 현저히 작다
        3. HTTP에서는 요청이 들어왔을 때 결과 값을 반환하고 연결을 끊는다.
        4. 자원의 소모가 적다.
    

        단점

        1. TCP/IP 연결을 새로 맺어야함 - 3 way handshake를 다시 해야함
        2. HTML 뿐만 아니라 javascirpt, css, image 등 수 많은 자료를 연결될 때마다 다운로드
        3. HTTP 지속 연결 (Persistent Connections)로 문제 해결
        4. HTTP2/HTTP3 에서 개선

* HTTP 메세지

<img src="https://blog.kakaocdn.net/dn/tWPRN/btq3ncYz5Cr/cf4pEkDQmybrtKztmWhixK/img.png" alt="3 way handshake"></img>
       
1. 요청 메세지 - 시작라인

    1. start-line = `request-line`
    2. `request-line` 'http method' + '(공백)' + '/' + '요청대상' + '(공백)' + '/' + 'version' 의 구조
            
        - `http method` 
            
            종류 : get, post, put, delete
            
            get - 조회
          
            post - 요청

        - `요청대상`
          
            절대경로(/)?query
        
        - `version`
          
            HTTP의 version
    

2. 응답 메세지 - 시작라인
    
    1. start-line = `status-line`
    2. `status-line` 'version' + '/' + status-code + '/' + 'reason-phrase'
    
        - `version`
          
            HTTP version
            
        - `status-code`
            
            200 : 성공
          
            400 : 클라이언트 요청 오류
          
            500 : 서버 내부 오류
          
        - `reason=phrase`
            
            사람이 이해할 수 있는 짧은 설명


3. HTTP HEADER

    1. header-field - field-name":"`OWS`field-value`OWS`    (OWS:띄어쓰기 허용)
    2. filed-name은 대소문자 구분이 없음
    3. 용도
        - HTTP 전송에 필요한 모든 부가정보
        - 표준 헤더가 존재함
        - 필요시 임의의 헤더 추가 가능
    

4. HTTP 메세지 바디
    
    1. 실제 전송할 데이터
    2. HTML, image, 음성, 파일 등
    

5. HTTP는 매우 단순하며 확장도 가능함


# HTTP 메서드

* HTTP 설계
    1. <span style="color:red">회원</span> 목록 `조회`  
       `get` <span style="color:red">/members</span>
    2. <span style="color:red">회원</span> `조회`  
       `get` <span style="color:red">/members</span>/{id}   
    3. <span style="color:red">회원</span> `등록`  
       `post`  <span style="color:red">/members</span>/{id}   
    4. <span style="color:red">회원</span> `수정`  
       `put` <span style="color:red">/members</span>/{id}
    5. <span style="color:red">회원</span> `삭제`  
       `delete` <span style="color:red">/members</span>/{id}
    

* 요구사항에 따른 URI 설계
    1. API URI는 resource를 먼저 식별하고 resource를 가지고 설계해야함
    2. 요구사항에 따른 resource는 <span style="color:red">회원</span>이 resource가 됨 
    3. resource와 행동을 분리하여 리소스는 URI가 되고 행위(`조회`,`등록`,`수정`,`삭제`)는 메서드가 됨
    

* 메서드의 종류
    
    - 주로 사용되는 메서드

        `GET`   조회
        
        1. 서버에 전달하고 싶은 데이터는 QUERY를 통해 전달
        2. 메세지 바디를 사용하여 데이터를 전달할 수 있지만 권장하지 않음
      
        `POST`  요청, 등록
    
        1. 메세지 바디를 통해 서버로 데이터 전달
        2. 주로 데이터 신규 등록, 프로세스에 사용
        3. 프로세스는 예로 주문에서 결제완료 -> 배달시작 처럼 값변경을 넘어 프로세스의 상태가 변경되는 경우에 사용됨
        
        `PUT`   대체
    
        1. 리소스를 완전히 대체 (기존 리소스의 중복되는 내용일지라도 모든 필드값을 그대로 입력해야함)
        2. 없으면 생성
        3. `POST`와 차이점은 클라이언트가 리소스 위치를 알고 URI 지정하여 사용
    
        `PATCH` 부분 변경
        
        1. 리소스를 부분적으로 변경 (`put`과 다르게 부분적인 필드값만 보내면 해당 필드만 수정됨)
    
        `DELETE`    삭제
        
        1. 리소스 제거

    - 기타 메서드

        `HEAD`  GET과 동일하지만 상태줄과 헤더만 반환
        
        `OPTIONS`   대상 리소스에 통신 가능 옵션을 설명
    
        `CONNECT`   대상 자원으로 식별되는 서버에 대한 터널 설정
        
        `TRACE` 리소스 경로를 따라 메세지 루프백 테스트 수행


* HTTP 메서드 속성

    1. Safe Method `안전`
    
        - 호출해도 리소스를 변경하지 않는다.
        - `GET` , `HEAD`
    
    2. Idempotent Method `멱등`
    
        - 한번 호출하든 두번 호출하든 100번 호출하든 결과가 똑같다.
        - `GET` , `PUT` , `DELETE`
        - PUT은 리소스 자체를 완전히 대체하기 때문에 같은 요청을 계속해서 반복하면 같은 리소스가 대체되는 것이기때문에 동일하다.
        - `멱등`이 필요한 이유는 `멱등`한 메서드는 몇번을 호출해도 결과가 동일하고 리소스에 미치는 영향이 동일하기 때문에 서버 내부의 이유로 정상 응답을 못 주었을 때, 클라이언트가 같은 요청을 동일하게 반복해도 되는지에 대한 판단 근거가 될 수 있다.
    
    3. cacheable Method `캐시가능`
    
        - 웹 브라우저에 똑같은 리소스를 또 다운로드 하지 않고 웹 브라우저 자체에 캐시로 저장하여 사용
        - `GET` , `HEAD` , `POST` , `PATCH` 
        - 실제로는 `GET` , `HEAD` 정도만 캐시로 사용
            1. `POST` , `PATCH`  는 본문 내용까지 캐시 키로 고려해야하는데 구현이 쉽지 않다.


# HTTP 메서드 활용

* 클라이언트 -> server 데이터 전송
    1. 데이터 전송 방법
        
            1. 쿼리 파라미터를 통한 데이터 전송
                - GET
                - 정렬 필터(검색어)
            
            2. 메세지 바디를 통한 데이터 전송
                - POST, PUT, PATCH
                - 회원가입, 상품주문, 등록, 변경
    
    2. 데이터 전송 상황
    
            1. 정적 데이터 조회  ex) /static/start.jpg
                - 쿼리 파라미터 없이 리소스 경로로 단순하게 조회
                - GET 사용
       
            2. 동적 데이터 조회  ex) /search?q=hello&hl=ko
                - GET 사용
                - 쿼리 파라미터를 사용해서 데이터 전달
                - 주로 검색, 게시판 필터로 사용
    
            3. HTML Form 데이터 전송
                - GET, POST 전송가능
                - GET = 쿼리 파라미터로 전송됨
                - POST = 메세지 바디로 전송됨
                - multipart/form-data 파일을 전송하기 위한 Content-Type
       
            4. HTTP API 데이터 전송
                - 서버와 서버간의 백엔드 시스템 통신
                - ajax 통신
                - 주로 Content-Type: application/json 을 사용

* HTTP API 설계 예시
    `참고` https://restfulapi.net/resource-naming
    1. `POST` 기반
        
        회원 목록 `GET` /members

        회원 등록 `POST` /members

        회원 조회 `GET` /members/{id}

        회원 수정 `PATCH` `PUT` `POST` /members/{id}

        회원 삭제 `DELETE` /members/{id}

            1. 클라이언트의 요청 POST /members
    
            2. server에서 새로 등록된 리소스에 대한 URI값을 반환해준다. 
                응답 데이터 예시
       
                HTTP/1.1 201 Created
                Content-Type: application/json
                Content_Length: 33
                Location: /members/100
       
                {
                    "username": "choi",
                    "age": 28
                }
    
            3. 이러한 형식을 컬렉션(Collection)이라 부른다.
                서버가 관리하는 리소스 디렉토리
                서버가 리소스 URI를 생성하고 관리

    2. `PUT` 기반 (파일이 존재한다면 지우고 새로 생성하는게 맞기 때문에 파일 예시가 제일 적당)
    
        파일 목록 `GET` /files
    
        파일 조회 `GET` /files/{filename}
    
        파일 등록 `PUT` /files/{filename}
    
        파일 삭제 `DELETE` /files/{filename}
    
        파일 대량 등록 `POST` /files
        
            1. 클라이언트가 리소스 URI를 알고 있어야한다.
                POST와는 다르게 등록시에도 클라이언트에서 리소스의 URI를 직접 지정해서 등록하게된다.
       
            2. 이러한 형식을 스토어(Store)이라 부른다.
                클라이언트가 관리하는 리소스 저장소
                클라이언트가 리소스의 URI를 알고 관리함

    3. HTML Form 기반 (`GET` `POST`만 지원)
    
        회원 목록 `GET` /members
        
        회원 등록 폼 `GET` /members/new
    
        회원 등록 `POST` /members/new

        회원 조회 `GET` /members/{id}
    
        회원 수정 폼 `GET` /members/{id}/edit
       
        회원 수정 `POST` /members/{id}/edit
    
        회원 삭제 `POST` /members/{id}/delete

            1. HTML Form은 GET, POST만 지원
            2. GET, POST만 지원하기 때문에 여러 제약이 있고 이 제약을 해결하기 위해 컨트롤 URI를 사용
                - /new, /edit, /delete가 컨트롤 URI
            3. HTTP 메서드로 해결하기 애매한 경우 컨트롤 URI를 사용

`출처` https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard