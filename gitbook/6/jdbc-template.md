# JDBC Template

## Spring JdbcTemplate
> [JdbcTemplate](https://docs.spring.io/spring-framework/docs/6.0.4/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html)
> 
> [Data Access](https://docs.spring.io/spring-framework/docs/6.0.4/reference/html/data-access.html#jdbc-core)
> 
> [Spring Initializr](https://start.spring.io/)
>

### 간단한 사용법
```java
@Component
public class AppRunner implements CommandLineRunner {
	private final JdbcTemplate jdbcTemplate;

	public AppRunner(JdbcTemplate jdbcTemplate) {
		this.jdbcTemplate = jdbcTemplate;
	}

	@Override
	public void run(String... args) throws Exception {
		String sql = "SELECT name FROM people";
		
		jdbcTemplate.query(sql, resultSet -> {
			while (resultSet.next()) {
				String name = resultSet.getString("name");
				System.out.println(name);
			}
		});
	}
}
```

### PreparedStatement​
```java
String sql = "SELECT name FROM people WHERE name LIKE ?";

jdbcTemplate.query(sql, resultSet -> {
	String name = resultSet.getString("name");

	System.out.println(name);
}, "%우");​
```

### Insert, Update, Delete
```java
String sql = """
		INSERT INTO people (name, age, gender) VALUES (?, ?, ?)
		""";
			
jdbcTemplate.update(sql, "홍길동", 15, "남");
```

### Transaction 관리
```java
@Component
public class AppRunner implements CommandLineRunner {
	private JdbcTemplate jdbcTemplate;
	private TransactionTemplate transactionTemplate;
	
	public AppRunner(JdbcTemplate jdbcTemplate,
				TransactionTemplate transactionTemplate) {
		this.jdbcTemplate = jdbcTemplate;
		this.transactionTemplate = transactionTemplate;
	}
	
	@Override
	public void run(String... args) throws Exception {
		transactionTemplate.execute(status -> {
			String sql = """
				INSERT INTO people(name, age, gender) VALUES(?, ?, ?)
				""";
	
			jdbcTemplate.update(sql, "홍길동", 15, "남");
	
			// 이런 식으로 예외를 던지면 전부 없던 일로 만들 수 있다.
			// throw new RuntimeException("FAIL!");
	
			return null;
		});
	}
}
```