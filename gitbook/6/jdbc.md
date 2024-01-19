# JDBC

## Java Database Connectivity
> [JDBC](https://ko.wikipedia.org/wiki/JDBC)
> 
> [JDBC driver](https://en.wikipedia.org/wiki/JDBC_driver)
> 
> [JDBC Basics](https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html)
>

JDBC(Java Database Connectivity)는 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다. 
JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.

각 벤더에서 제공하는 Driver가 있어야 사용할수 있다.

Sun Microsystems에서 1997년 2월 19일 JDK 1.1의 일부로 JDBC를 출시함
> Robust new features including **JDBC**[tm] for database connectivity, RMI for remote object access, and additional Java Security APIs
> [[ref.](https://web.archive.org/web/20080210044125/http://www.sun.com/smi/Press/sunflash/1997-02/sunflash.970219.0001.xml)]
>

### JDBC의 특징
- 프로그램의 데이터는 대부분 메모리에 저장되며, 영속성을 위해 DB에 저장
- JDBC를 통해 데이터의 영속성을 보장해줄수 있다.
- Java의 Persistance Layer

### JDBC 사용방법 및 기능
- 대부분 인터페이스와 명세의 모음
- 인터페이스에 대한 다수의 구현을 가능하게 하고, 런타임에 동일 애플리케이션 내에서 사용가능
- 올바른 자바 패키지들의 동적 로딩을 제공하고, JDBC Driver Manager(DriverManager)에 등록가능
- DriverManager는 Connection의 팩토리로 사용됨
- JDBC 클래스는 java.sql, javax.sql 패키지에 포함되어 있음
  - javax.sql은 JDBC API의 확장([ref.](https://docs.oracle.com/en/java/javase/20/docs/api/java.sql/javax/sql/package-summary.html))

Oracle Datatype과 JDBC의 set 메서드 비교

| Oracle Datatype | setXXX() Methods   |
| ----------------|--------------------|
| CHAR            | - setString()      |
| VARCHAR2        | - setString()      |
| NUMBER          | - setBigDecimal()<br> - setBoolean()<br> - setByte()<br> - setShort()<br> - setInt()<br> - setLong()<br> - setFloat()<br> - setDouble() |
| INTEGER         | - setInt()         |
| FLOAT           | - setDouble()      |
| CLOB            | - setClob()        |
| BLOB            | - setBlob()        |
| RAW             | - setBytes()       |
| LONGRAW         | - setBytes()       |
| DATE            | - setDate()<br> - setTime()<br> - setTimestamp() |



### JDBC와 Java 버전

버전 3.1을 기점으로 [자바 커뮤니티 프로세스](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EC%BB%A4%EB%AE%A4%EB%8B%88%ED%8B%B0_%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4)를 통해 개발되고 있음

| Year |   JDBC Version   | JSR Specification | JDK Implementation | Features |
|------|------------------|-------------------|--------------------|----------|
| 2017 | JDBC 4.3         | JSR 221           | Java SE 9          | - Support sharding<br> - Extra support for the connection builder interface<br> - Interface of sharding key |
| 2014 | JDBC 4.2         | JSR 221           | Java SE 8          | - Ref Cursor Support<br> - Additional javq.sql interfaces<br> - Additional SQL type interfaces<br> - Additional JDBC type enum |
| 2011 | JDBC 4.1         | JSR 221           | Java SE 7          | - Enhanced Date Type value of timestamp<br>- Additional mappings to JDBC types |
| 2006 | JDBC 4.0         | JSR 221           | Java SE 6          | - Auto-load driver of java.sql<br> - Data Type as a row<br> - Conversion of national Character set<br> - Supports XML and SQL/XML |
| 2001 | JDBC 3.0         | JSR 54            | JDK 1.4            | - SQL Driver |
| 1999 | JDBC 2.1         |                   | JDK 1.2            | - Character Set |
| 1997 | JDBC 1.2         |                   | JDK 1.1            | - SQL Query Execution |

### Connection
> [Establishing a Connection](https://docs.oracle.com/javase/tutorial/jdbc/basics/connecting.html)
>
- JDBC Connection
- JDBC connections support creating and executing statements.
- DBC connections support update statements such as SQL's CREATE, INSERT, UPDATE and DELETE
- Stored procedures may be invoked through a JDBC connection.

### [Statement](https://docs.oracle.com/en/java/javase/19/docs/api/java.sql/java/sql/Statement.html)
> [Processing SQL Statements with JDBC](https://docs.oracle.com/javase/tutorial/jdbc/basics/processingsqlstatements.html)
>
- Statement는 요청 즉시 DBMS로 보내어진다.
- 결과는 ResultSet을 통해 얻을 수 있다.


### [PreparedStatement](https://docs.oracle.com/en/java/javase/19/docs/api/java.sql/java/sql/PreparedStatement.html)
> [Using Prepared Statements](https://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html)
> 

- [기본 중 기본인 SQL Injection 공격](https://ko.wikipedia.org/wiki/SQL_삽입)
- [Exploits of a Mom](https://xkcd.com/327/)
- [국내 사례](https://www.google.com/search?q=뽐뿌+SQL+Injection)

- Statement의 하위 interface
- Statement가 캐싱되며 [execution-path](https://en.wikipedia.org/wiki/Query_plan)(Query Plan)가 미리 정해진다.
- Statement의 재사용이 가능하며 파라미터같은 필요한 정보만 전송하므로 효율적으로 실행이 가능(쿼리 파라미터; 동적 쿼리)

### [CallableStatement](https://docs.oracle.com/en/java/javase/19/docs/api/java.sql/java/sql/CallableStatement.html)
- Statement의 하위 interface
- 데이터베이스의 [Stored Procedure](https://en.wikipedia.org/wiki/Stored_procedures)를 실행하는데 사용된다.
- Input, Output 파라미터 모두 데이터베이스의 Stored Procedure로 전달되어야 한다.
- 어떠한 정보도 반환하지 않는다.
