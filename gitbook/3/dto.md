---
description: Data Transfer Object
---

# DTO

> **Martin Flower의 DTO\[**[**Link**](https://martinfowler.com/eaaCatalog/dataTransferObject.html)**]**
>
> * _An object that carries data between processes in order to reduce the number of method calls._ When you're working with a remote interface, such as Remote Facade (388), each call to it is expensive.

## IPC (Inter-Process Communication)

* 서로 다른 프로세스간 통신
* B/E, F/E Tier가 나누어지면, IPC가 필수
  * 서로 다른 프로세스간의 통신이므로
* File, Socket, RMI(Java) 등 IPC를 위한 다양한 방법이 있다.
  * 파일의 경우 한쪽은 쓰고, 한쪽을 읽기만 하면 통신으로 활용가능

> [**RPC**](https://en.wikipedia.org/wiki/Remote\_procedure\_call) **(Remote Procedure Call)**
>
> * _RPC is a request–response protocol. An RPC is initiated by the client, which sends a request message to a known remote server to execute a specified procedure with supplied parameters._
> * _The remote server sends a response to the client, and the application continues its process._&#x20;
> * _While the server is processing the call, the client is blocked, unless the client sends an asynchronous request to the server, such as an XMLHttpRequest._
> * _There are many variations and subtleties in various implementations, resulting in a variety of different (incompatible) RPC protocols._

> Java [RMI](https://en.wikipedia.org/wiki/Java\_remote\_method\_invocation) (Remote Method Invocation)&#x20;
>
> * _In_ [_computing_](https://en.wikipedia.org/wiki/Computing)_, the Java Remote Method Invocation (Java RMI) is a_ [_Java_](https://en.wikipedia.org/wiki/Java\_\(programming\_language\)) [_API_](https://en.wikipedia.org/wiki/Application\_programming\_interface) _that performs_ [_remote method invocation_](https://en.wikipedia.org/wiki/Remote\_method\_invocation)_, the object-oriented equivalent of_ [_remote procedure calls_](https://en.wikipedia.org/wiki/Remote\_procedure\_call) _(RPC), with support for direct transfer of_ [_serialized_](https://en.wikipedia.org/wiki/Serialization#Java) _Java classes and_ [_distributed garbage-collection_](https://en.wikipedia.org/wiki/Distributed\_Garbage\_Collection)_._

## Anemic Domain Model(무기력한 도메인 모델)

> [관련 링크](https://martinfowler.com/bliki/AnemicDomainModel.html)

데이터만 담으므로 제대로 된 객체라고 보기 힘듬(구조체의 느낌)

## DTO (Data Transfer Object)

* Java Bean이라고 부르는 형태에 가깝다.
* 다음과 같은 규칙이 있다. \[[Link](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94%EB%B9%88%EC%A6%88)]
  * getter, setter로만 이루어짐
  * 직렬화가 되어야함 (java.io.Serializable) (이 부분은 의견이 갈린다)
  * 기본 생성자를 가지고 있어야 한다.
  * 필요한 이벤트 처리 메서드들을 포함하고 있어야 한다.
* 최근의 자바에서는 record를 활용할수 있음

> [Spring Bean](https://docs.spring.io/spring-framework/reference/core/beans/introduction.html)
>
> Spring Framework에 의해 관리되는 객체

> [POJO](https://en.wikipedia.org/wiki/Plain\_old\_Java\_object) (Plain Old Java Object)
>
> 엄격한 제약조건이 없지만, 다음과 같은 규칙이 있다.
>
> 1. 미리 정의된 수퍼 클래스를 갖지 않는다. (No extends)
> 2. 미리 정의된 인터페이스를 구현하지 않는다. (No implements)
> 3. 미리 정의된 애노테이션을 갖지 않는다.

> [VO](https://en.wikipedia.org/wiki/Value\_object) (Value Object)
>
> * 동등성(equals()) 비교시, 내부 값을 비교함.&#x20;
>   * 같은 객체(Object)인지 비교하지 않음.
> * 불변해야한다. (Immutability)
> * 자바의 커스텀 타입은 레퍼런스 타입이고, 커스텀 타입을 전달하면 레퍼런스가 전달되므로 불변인것처럼 에뮬레이팅을 해야한다.&#x20;
>   * _Java programmers therefore emulate value objects by creating immutable objects, because if the state of an object does not change, passing references is semantically equivalent to copying value objects._

Data Transfer(데이터 전송) 측면에 집중하면 원격(Remote)가 아닌 경우에도 DTO를 사용할수 있다.

### DTO vs VO

#### Mutability

* DTO는 mutable/immutable 할 수도 있다. (주로 immutable)
* VO는 immutable

#### Comparison

* DTO는 주소를 비교한다.
* VO는 값을 비교한다. (equals, hashCode를 구현해 동등성 비교)

