---
description: TCP 소켓을 만들고 HTTP를 따라 서버와 통신한다.
---

# HTTP Client

## Connect

Socket 객체 생성시 바로 접속되며, 실패시 ConnectException이 발생한다.

IP Address (Network Layer, Layer 3), Port No. (Transfer Layer, Layer 4)

```java
String host = "example.com"; // 실제있는 사이트, 확인해보자. IP, 도메인 다 가능
int port = 80; // HTTP의 기본 Port 번호
Socket clientSocket = new Socket(host, port); // 객체 생성시 바로 접속. ConnectException 발생에 주의
```

## Request

요청 메시지를 만들고 TCP Socket을 통해 전송한다.

### Start Line

**마지막 빈 줄을 잊지말자**

```
GET http://example.com/ HTTP/1.1

```

Or

```
GET / HTTP/1.1
Host: example.com

```

### Java 예시

#### Body 생성

```java
String message = """
    GET / HTTP/1.1
    Host: example.com
    
    """;
```

```java
String message = "" +
    "GET / HTTP/1.1\n" +
    "Host: example.com\n" +
    "\n";
```

#### Data 전송

```java
OutputStream outputStream = socket.getOutputStream();
outputStream.write(message.getBytes());
```

```java
// Writer를 이용
Writer writer = new OutputStreamWriter(socket.getOutputStream());
writer.write(message);
writer.flush(); // 내부에 버퍼가 있다. flush를 잊지 말자
```

## Response

```java
InputStream inputStream = socket.getInputStream();

byte[] bytes = new byte[1_000_000];
int size = inputStream.read(bytes);

byte[] data = Arrays.copyOf(bytes, size);
String text = new String(data);

System.out.println(text);
```

```java
// Reader를 이용
Reader reader = new InputStreamReader(socket.getInputStream());
CharBuffer charBuffer = CharBuffer.allocate(1_000_000);
reader.read(charBuffer);
charBuffer.flip(); // toString()전에 flip()을 반드시 수행
System.out.println(charBuffer.toString());
```

## Close

```java
socket.close();
```

```java
try (Socket socket = new Socket(host, port)) {

}
```
