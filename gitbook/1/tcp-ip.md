# TCP/IP

OSI Layers: Transfer Layer (Layer 4)

Internet Protocol Suite \[[참조](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7\_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C\_%EC%8A%A4%EC%9C%84%ED%8A%B8)]

## TCP/UDP

전송 계층의 대표적인 프로토콜

### TCP

연결이 필요하고, 전달 및 순서를 보장함

### UDP

연결하지 않고 데이터를 보냄

전달 및 순서를 보장하지 않음

## Socket

Socket과 Socket API를 구분하자

유닉스에서 Socket은 일반 File처럼 FD로 읽고 쓰기 가능

Java에서도 File의 IO Stream처럼 IO Stream으로 다룰 수 있다.

## TCP 통신 순서

1. 서버에서 소켓을 열고 클라이언트의 접속요청을 받기 위해 대기 (Listen)
2. 클라이언트에서 소켓을 만들고, 서버에 접속을 요청 (Connect)
3. 서버는 접속 요청을 받고 클라이언트와 통신할 소켓을 생성 (Accept)
4. 소켓을 통해 데이터를 송수신 (Send/Receive)
5. 통신을 마치고 소켓을 닫음 (Close)

