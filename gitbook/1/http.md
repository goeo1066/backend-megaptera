# HTTP

## OSI 7 Layers 간단 설명 (2, 3, 5, 7만 보자)

### Layer 2: 데이터 링크(Data Link) 계층&#x20;

* MAC Address&#x20;
* Network Bridge, Switch
* Network Interface 간의 데이터 전송 담당

### Layer 3: 네트워크(Network) 계층

* IP Address&#x20;
* Router, L3-Switch
* 서로 다른 네트워크 간의 데이터 전송

### Layer 4: 전송(Transport) 계층

* Port Number
* TCP, UDP
* 프로세스 간 데이터 전송

### Layer 7: 응용(Application) 계층

* Protocols, Applications
* HTTP
* 응용 프로세스와 직접 응용 서비스를 수행
* TLS같은 보안 계층이 먼저 들어갈 수 있음

## Client-Server 모델/메시지 교환

### 서비스/리소스

* URL(정확히는 URI)
* scheme://host:port/path?query#fragment

### 클라이언트는 요청한다

* 요청을 쓰고 응답을 읽는다. (당연한 것 같지만 그래도 Remind)

### 서버는 처리하고 응답한다.

* 요청을 읽고 응답을 쓴다.

## Stateless(무상태)

* HTTP는 각 요청에 대한 연결을 유지하지 않음
* 클라이언트를 식별할 수 있는 '키'가 요청마다 있어야한다.
* 세션을 이용
  * Secure, HttpOnly 쿠키를 이용하는 게 보안상 좋다.
  * ~~...브라우저 자체가 취약하면 소용없긴 한것 같다...~~

## HTTP 메시지

사람이 읽을 수 있는 형태를 지향, 요청과 응답의 구조가 같다.

### Start Line

* 간단한 메시지가 한 줄로 구성
* 요청/응답의 Start Line이 다르다.

### Headers

* 각종 헤더들이 여기 들어간다.

### 빈 줄(\n)

* 헤더는 여기까지다

### Body

* 크기를 알기 어렵다. 헤더 내 Content-Length 항목을 활용한다.
* Transfer-Encoding 헤더가 없는 경우 Content-Length를 필수로 지정
  * A user agent SHOULD send Content-Length in a request when the method defines a meaning for enclosed content and it is not sending Transfer-Encoding. \[[Link](https://www.rfc-editor.org/rfc/rfc9110.html#name-content-length)]
* 바이너리 등 가능(Human-readable일 필요는 없다)
* multipart/form-data 등 여러 내용을 포함 할 수 있다.

## HTTP Methods

### GET/HEAD

* CRUD의 Read
* HEAD는 Get인데 Boby가 없는 형태

### POST

* 멱등성이 없다. (같은 URI로 다시 요청해도 다른 응답이 올 수 있다)
* CRUD의 Create, Collection Pattern에서 Create로 사용

### PUT/PATCH

* CRUD의 Update
* PUT -> Overwrite
* PATCH -> 부분 업데이트&#x20;
* 하지만 보통 구분하지 않고 쓴다.

### DELETE

* CRUD의 Delete

### OPTION

* Method 지원 확인 \[[참조](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)]
