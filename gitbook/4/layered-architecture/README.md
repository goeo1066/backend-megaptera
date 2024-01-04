---
description: 관심사의 분리, 응집도, 결합도, Layered Architecture, UUID
---

# Layered Architecture

### Layered Architecture (Style)

#### Separation of Concerns

* 커다란 프로그램은 유지보수가 어렵다.
  * 10권의 책은 관리하기 쉬움, 1만권의 책은 관리하기 어렵다
  * 인간의 한계 + 공간의 한계
* 폴더나 자바 패키지 등이 관심사를 나눈 예
* 그룹화가 필요
* 특정 관심사에 몰입, 관심사가 아닌 것은 칼같이 나눔
* 큰 규모의 프로젝트 일 수록 구조가 낮은 결합도와 높은 응집도를 가지도록 한다

> 참고: [응집도](https://en.wikipedia.org/wiki/Cohesion\_\(computer\_science\)), [결합도](https://en.wikipedia.org/wiki/Coupling\_\(computer\_programming\))

### Layered Architecture

* 다층구조
* 웹과 기능은 분리 될수 있다.
* 3 Tier Architecture
  * Client Device <--> Application Server <--> Database Server
* 3 Layered Architecture
  * Presentation Layer <--> Domain Layer <--> Data Access Layer

> 참고: [다층 구조](https://ko.wikipedia.org/wiki/%EB%8B%A4%EC%B8%B5\_%EA%B5%AC%EC%A1%B0), [Layered Architecture](https://github.com/ahastudio/til/blob/main/architecture/layered-architecture.md)
>
> Repository <-(Demain Model)-> Service <-(DTO)-> Controller

### UUID

ULID // 시간순 정렬 가능한 ID

TSID // 시간순 정렬 가능한 ID

> 참고: [Identifier](https://github.com/ahastudio/til/tree/main/identifier), [UUID](https://ko.wikipedia.org/wiki/%EB%B2%94%EC%9A%A9\_%EA%B3%A0%EC%9C%A0\_%EC%8B%9D%EB%B3%84%EC%9E%90), [Java UUID](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/UUID.html), [ULID](https://github.com/ulid/spec), [ULID Creator](https://github.com/f4b6a3/ulid-creator), [TSID Creator](https://github.com/f4b6a3/tsid-creator)

### Tiers Vs. Layers

참고: [Should all apps be n-tier?](https://web.archive.org/web/20200802111420/http://www.lhotka.net:80/weblog/ShouldAllAppsBeNtier.aspx)

#### Logical layers&#x20;

Logical layers are merely a way of organizing your code. Typical layers include Presentation, Business and Data – the same as the traditional 3-tier model. But when we’re talking about layers, we’re only talking about logical organization of code. In no way is it implied that these layers might run on different computers or in different processes on a single computer or even in a single process on a single computer. _All_ we are doing is discussing a way of organizing a code into a set of layers defined by specific function.

#### Physical tiers

Physical tiers however, are only about where the code runs. Specifically, tiers are places where layers are deployed and where layers run. In other words, tiers are the physical deployment of layers.

UI Layer

* Application Layer 또는&#x20;
* Interface Layer(Eric Evans)라고도 한다.
