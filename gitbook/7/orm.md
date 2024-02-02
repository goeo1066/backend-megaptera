# ORM

## ORM (Object-Relational Mapping)

> [Object–relational mapping](https://en.wikipedia.org/wiki/Object%E2%80%93relational\_mapping)
>
> [Object–relational impedance mismatch](https://en.wikipedia.org/wiki/Object%E2%80%93relational\_impedance\_mismatch)
>
> [Java Persistence/Mapping](https://en.wikibooks.org/wiki/Java\_Persistence/Mapping)

객체와 관계형 데이터를 매핑하는 작업 또는 기술, 도구

SELECT 후 객체 생성, 객체의 상태를 활용해 UPDATE, 객체의 생명주기 관리, 변화 감지 기능을 추가 할 수 있음

일반적인 ORM 도구들은 SQL문을 자동으로 생성 -> 다양한 DBMS에 대응하기 좋음

## JPA (Jakarta Persistence API)

> [Jakarta Persistence](https://jakarta.ee/specifications/persistence/) (Eclipse)
>
> [Jakarta Persistence](https://en.wikipedia.org/wiki/Jakarta\_Persistence) (Wikipedia)
>
> [Hibernate (framework)](https://en.wikipedia.org/wiki/Hibernate\_\(framework\))
>
> [EclipseLink](https://en.wikipedia.org/wiki/EclipseLink)

관계형 데이터 관리 API

JPA는 인터페이스(스펙)만 다루며 구현체인 Hibernate, EclipseLink를 사용하게 된다.

## JPA Entity

> [What is a JPA Entity?](https://docs.oracle.com/cd/E16439\_01/doc.1013/e13981/undejbs003.htm)
>
> [Entities](https://docs.oracle.com/javaee/6/tutorial/doc/bnbqa.html)

Java Object를 RDBMS의 Table에 맵핑시키는 방법에 관한 표준을 정의

데이터 영속화의 관점(DB세계)과 Business 절차를 다루는 관점(OOP세계)를 적절히 조화시켜 사용

## CMP (Container-managed persistence)

> [CMP](https://docs.oracle.com/cd/E19655-01/819-1644/decmp.html)
>
> [CMP Entity Beans](https://www.oreilly.com/library/view/websphere-v35-handbook/0130416568/0130416568\_ch11lev1sec5.html)

