# Hibernate

> [Hibernate ORM Hibernate Core](https://mvnrepository.com/artifact/org.hibernate.orm/hibernate-core/6.1.7.Final)

## Hibernate

### 설정파일

src/main/resources/META-INF/persistence.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.1">
	<persistence-unit name="demo">
		<class>com.example.demo.models.Person</class>
		<properties>
			<property name="jakarta.persistence.jdbc.url"
				value="jdbc:postgresql://localhost:5432/postgres"/>
			<property name="jakarta.persistence.jdbc.user"
				value="postgres"/>
			<property name="jakarta.persistence.jdbc.password"
				value="password"/>
		</properties>
	</persistence-unit>
</persistence>
```

### 매핑 정보 Annotation

```java
@Entity
@Table(name = "people")
public class Person {
	@Id
	@Column(name = "name") // 생략가능
	private String name;
	
	@Column(name = "age")
	private Integer age;
	
	@Column(name = "gender")
	private String gender;
...
```

### Entity를 생성

```java
Person person = new Person("Mr.Big", 35, "남");
entityManager.persist(person);
```

### CRUD

```java
// Entity 생성 및 확인
Person person = new Person("Mr.Big", 35, "남");
entityManager.persist(person);

Person found = entityManager.find(Person.class, "Mr.Big");
assertEquals(person, found);

// 다른 트랜잭션에 가서 또 확인!
Person person = entityManager.find(Person.class, "Mr.Big");
assertEquals("Mr.Big", person.name());

// Entity의 상태를 바꾸면 commit했을 때 자동으로 UPDATE 수행.
Person person = entityManager.find(Person.class, "Mr.Big");
person.changeAge(30);

// 다른 트랜잭션에 가서 또 확인!
Person person = entityManager.find(Person.class, "Mr.Big");
assertEquals(30, person.age());

// Entity 삭제 및 확인
Person person = entityManager.find(Person.class, "Mr.Big");
entityManager.remove(person);

Person found = entityManager.find(Person.class, "Mr.Big");
assertNull(found);

// 다른 트랜잭션에 가서 또 확인!
Person person = entityManager.find(Person.class, "Mr.Big");
assertNull(person);
```

EntityManager엔 여러 Entity를 얻을 수 있는 메서드가 없다. -> JPQL과 createQuery를 사용

JPQL은 SQL과 다르게 관계(테이블)이 아니라 JPA 객체를 대상으로 하는 SQL과 유사한 쿼리(질의) 언어다.

```java
String jpql = "SELECT person FROM Person person";

List<Person> people = entityManager
	.createQuery(jpql, Person.class) // 타입을 지정하지 않으면 Query, 지정하면 TypedQuery.
	.getResultList();

assertEquals(2, people.size());
```

### Test

```java
public class JpaTest {
	private EntityManagerFactory entityManagerFactory;
	
	private EntityManager entityManager;
	
	@BeforeEach
	void setUp() {
		entityManagerFactory = Persistence.createEntityManagerFactory("demo");
		entityManager = entityManagerFactory.createEntityManager();
	}
	
	@AfterEach
	void tearDown() {
		entityManager.close();
		entityManagerFactory.close();
	}
	
	@Test
	void query() {
		Person person = entityManager.find(Person.class, "견우");

		System.out.println("*".repeat(80));
		System.out.println(person);
		System.out.println("*".repeat(80));
	}
}
```

### Hibernate 구조

1차 캐시

* 스레드의 시작부터 종료까지 사용하는 캐시
* 스레드 종료 후 사라진다
* 조회 시 캐시미스나면 DB에서 로드 후 1차 캐시에 저장한다
* 조회 시 캐시히트하면 캐시에서 바로 불러온다

동일성 보장

* 1차 캐시를 사용하기 때문에, 같은 ID의 객체를 두번 조회하면 같은 객체가 조회된다.(a == b: true)

Dirty Checking (변경 감지)

> [https://jojoldu.tistory.com/415](https://jojoldu.tistory.com/415)

주요 메서드

* persist()
  * 엔티티를 1차 캐시에 저장하고, 쓰기 지연 SQL 저장소에 INSERT 쿼리를 생성후 일시저장
  * 이후 commit() 시점에서 일시저장된 쿼리를 보냄 (flush())
    * 전체/하나씩 설정 가능
    * flush() -> commit()

