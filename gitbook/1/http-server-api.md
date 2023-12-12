# 고수준 HTTP Server API

## 전체 흐름 예시

```java
InetSocketAddress address = new InetSocketAddress(8080);
int backlog = 0;

HttpServer httpServer = HttpServer.create(address, backlog); // C랑 비슷한 느낌이 든다..

// Handler 지정
httpServer.createContext("/", (exchange) -> {
  ...
});

// Listen
httpServer.start();
```

## Reading Request

### HTTP Method

```java
String method = exchange.getRequestMethod();
System.out.println(method);
```

### Headers

```java
Headers headers = exchange.getRequestHeaders();
for (String key : headers.keySet()) {
    System.out.println(key + ": " + headers.get(key));
}
```

### Body

```java
InputStream inputStream = exchange.getRequestBody();
String body = new String(inputStream.readAllBytes());
System.out.println(body);
```

## Writing Response

```java
String body = "Hello, world!";
byte[] bytes = body.getBytes();

exchange.sendResponseHeaders(200, bytes.length);

OutputStream outputStream = exchange.getResponseBody();
outputStream.write(bytes);
outputStream.flush();
```
