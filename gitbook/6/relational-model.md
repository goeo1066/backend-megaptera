# Relational Model

## Relational Model

> [관계형 모델](https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95\_%EB%AA%A8%EB%8D%B8)
>
> [관계형 데이터베이스](https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95\_%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)
>
> [The Relational Data Model](https://opentextbc.ca/dbdesign01/chapter/chapter-7-the-relational-data-model/)

데이터를 표현하는 개념의 집합

### 속성(Attribute)

속성은 (이름, 타입)으로 구성. 이름은 집합안에서 유일해야한다.
- (동적 타입 언어에서는) 이름만

예시:
- 이름/문자열
- 나이/정수
- 성별/문자(M/F)



### 튜플(Tuple)

(속성, 값)쌍의 집합, 이름은 하나의 집합안에서 유일, 속성의 이름은 겹치지 않는다.

대게는 Row, Record로 구현됨 { (이름/문자열, 견우), (나이/정수, 13), (성별/문자, 남) }

튜플은 집합이기 때문에 중복을 허용하지 않지만, 대부분의 DBMS는 중복을 허용함, Null도 허용



### 관계(Relation)

> [Relational Model](https://en.wikipedia.org/wiki/Relational\_model)
>
> [Relation (Database)](https://en.wikipedia.org/wiki/Relation\_\(database\))

속성의 집합=Header

튜플의 집합=Body

관계는 튜플의 집합이라고 할수 있다.

관계 변수 대게는 테이블로 구현, 속성 집합을 Schema로 표현.