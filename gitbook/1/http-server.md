---
description: TCP 소켓을 만들고 HTTP를 따라 클라이언트와 통신한다.
---

# HTTP Server

## Listen

클라이언트 접속이 클라이언트와 통신할 수 있는 소켓이 자동 생성된다.

동기식으로 작성시 처리가 완료될때까지 다른 요청을 수신하지 못하게 되므로 비동기, 이벤트 기반으로 처리할 필요가 있다.

```java
int port = 8080;
ServerSocket listener = new ServerSocket(port);

Socket socket = listener.accept(); // Client 접속시 소켓 자동 생성 
```

## Response

서버는 요청을 받고 응답한다.

```java
String message = """
    HTTP/1.1 200 OK
    
    Hello, world!
    """;
```

```java
String message = "" +
    "HTTP/1.1 200 OK\n" +
    "\n" +
    "Hello, world!\n";
```

```java
// Content-Length, Content-Type Header 추가
String body = "Hello, world!";
byte[] bytes = body.getBytes();
String message = "" +
    "HTTP/1.1 200 OK\n" +
    "Content-Type: text/html; charset=UTF-8\n" +
    "Content-Length: " + bytes.length + "\n" +
    "\n" +
    body; // 정확한 크기를 알수있기 때문에 \n을 추가할 필요가 없다.
```

## Close

전송완료 후 Close한다
