# Database

## Database(DB)

> [Database](https://en.wikipedia.org/wiki/Database)
>
> [Database란?](https://www.oracle.com/kr/database/what-is-database/)

구조화된 정보/데이터의 조직화된 모음

## DBMS(Database Management System)

> [데이터베이스 관리 시스템](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4\_%EA%B4%80%EB%A6%AC\_%EC%8B%9C%EC%8A%A4%ED%85%9C)
>
> [데이터베이스 언어](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4\_%EC%96%B8%EC%96%B4)

데이터베이스 관리 시스템

응용프로그램에서 접근

접근 권한, 보안 문제를 다룰수 있어야 한다.



### RDBMS(Relational Database Management System)

가장 인기있는 DBMS

MySQL, MariaDB, PostgreSQL, MS SQL(SQL Server), Oracle

### 데이터베이스 언어

1. DDL: Schema
2. DML: Query & Command
3. DCL: Grant, Revoke, Commit, Rallback

### SQL

모두 SQL로 표현된다.&#x20;

1970년대 만들어진 SEQUEL이 SQL로 바뀜.

## 데이터 모델(Data Model)

> [Data Model](https://en.wikipedia.org/wiki/Data\_model)
>
> [Types of Data Models](https://opentextbc.ca/dbdesign01/chapter/chapter-4-types-of-database-models/)

데이터 모델 유형

1. Conceptual
2. Logical
3. Physical

### 관계형 데이터 모델

> [관계형 모델](https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95\_%EB%AA%A8%EB%8D%B8)
>
> [관계형 데이터베이스](https://ko.wikipedia.org/wiki/%EA%B4%80%EA%B3%84%ED%98%95\_%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4)
>
> [The Relational Data Model](https://opentextbc.ca/dbdesign01/chapter/chapter-7-the-relational-data-model/)

가장 인기있는 데이터 모델

다른 데이터 모델로 Hierarchical, Network, Object-based Model이 있다.

대부분 ERM(Entity-Relationship Model)과 RM(Relational Model)을 구분하지 못한다.&#x20;

Relation은 튜플의 집합(DBMS의 Table): Relation은 이론적인 설명, Table은 DBMS에서 사용하는 개념; 둘이 같지 않다. (일할때는 구분없이 쓴다)

Relationship과 Relation은 서로 아무 상관없는 단어라고 생각하자

> [A Relational Model of Data for Large Shared Data Banks](https://web.archive.org/web/20070612235326/http://www.acm.org/classics/nov95/toc.html)&#x20;
>
> “The term relation is used here in its accepted mathematical sense. Given sets S1, S1, ···, Sn, (not necessarily distinct), R is a relation on these n sets if it is a set of n-tuples each of which has its first element from S1, its second element from S1, and so on.”

### 튜플

