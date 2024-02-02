# Spring Data JPA

## Repository

> [Spring Data JPA 문서](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)
>
> [조영호님의 DAO와 Repository의 차이에 대한 설명](http://aeternum.egloos.com/1160846)

### vs DAO

DAO는 Data Access의 관점에 무게

Repository는 객체를 관리하는 Collection에 가까운 관점에서 사용한다.



## Transactional Annotation

> [Layered Architecture](https://wikibook.co.kr/article/layered-architecture/)

Spring AOP를 이용한 @Transactional로 지정

일반적으로 Application Layer가 Transaction 범위가 된다

```java
@Service
@Transactional
public class CreateItemService {
	private PersonRepository personRepository;

	public CreateItemService(PersonRepository personRepository) {
		this.personRepository = personRepository;
	}

	void createItem(String personName, String name, String usage) {
		Person person = personRepository.findByName(personName)
				.orElseThrow(() -> new PersonNotFound(personName));

		person.addItem(name, usage);
	}
}
```

### Transactional 테스트

> [토비님의 @Transactional 테스트의 실용성에 대한 설명](https://www.inflearn.com/questions/792383)
