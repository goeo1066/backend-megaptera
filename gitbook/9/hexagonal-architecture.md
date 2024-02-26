# Hexagonal Architecture

> [Hexagonal Architecture ](https://alistair.cockburn.us/hexagonal-architecture/)(Alistair Cockburn)
>
> [Layered Architecture](https://github.com/ahastudio/til/blob/main/architecture/layered-architecture.md) (Ahastudio)

1. User-side(Presentation)
2. Application(Domain)
3. Database-side(Data) (다른 장치나 소켓 등도 포함; 이름만 데이터베이스)

### UI와 비즈니스 로직 분리

* Layered Architecture
  * User-side - Database-side를 완전히 다른 것으로 취급
* Hexagonal Architecture
  * User-side - Database-side를 Application의 외부로 취급
  *    User-side -> Application: Incoming Port
  * Application -> Database-side: Outgoing Port
  * ISP에 따라 작은 인터페이스들을 만들고, 포트로 사용
  * 다른 외부요소오 분리되어 테스트하기 쉬워진다.

> 참고자료
>
> [조영호님의 “우아한객체지향” 세미나](https://youtu.be/dJ5C4qRqAgA)
>
> [Design Patterns: Elements of Reusable Object-Oriented Software](http://aladin.kr/p/S6Nzq)
