# Application & Domain Layer

Application Layer

* 이 계층을 얇게 유지된다. 거의 있는게 없어야 된다.
* 업무 규칙이나 지식이 포함되지 않으며
* 오직 작업을 조정함도메인 객체의 협력자에게 작업을 위임한다.
* Domain Model은 일반적인 객체로, 행위가 중요하다.
  * 유닛 테스트에 적합하다.

행위없이 코딩

```java
Long amount = account.getAmount();
account.setAmount(amount + 10_000);
```

행위가 있는 경우

```java
account.increaseAmount(10_000);
```

### DAO/Repository

| DAO   | Repository |
| ----- | ---------- |
| DB 중심 | 도메인 모델 중심  |

* JPA Entity랑 DDD Entity는 다르다.

> DAO <--> Repository <--> Service <--> Controller <--> UI

* Getter는 절대로 비즈니스 로직을 위해 쓰지 말것
* getAmount -> 뭔가 잘못 되고 있다는 조짐
