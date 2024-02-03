# Tactical Design
전술적 설계
DDD Lite, Model Driven Design

## Model Driven Design
- 전략적 설계 보편 언어를 통해 도메인 모델을 발견, 이를 설계와 코드에 반영

### 도메인 모델 패턴
1. Entity
  - 연속성, 식별성데 따라 정의된다. 앨리스는 키가 작아져도 앨리스 (동일성)
    - 반대로 속성이 완전히 같아도 두개로 식별될수 있음
    - ID가 같으면 둘은 같다 

2. Value Object
  - VO
  - 연속성, 식별성이 중요하지 않은 객체, 두 장의 만원은 각각 같다고 볼수 있다. (동등성)
    - 쇼핑몰 도메인에서는 모든 만원은 똑같다
    - 특정 지폐를 추적한다면 모든 만원을 같다고 안 볼수도 있다.
  - 항상 equals를 구현
  - 불변 객체로 만들어야 한다.
  - Hibernate 6.2부터 records 지원
    - Spring Boot 3.0.4 (Hibernate 6.1.7.Final)

3. Aggregate
  - Entity와 VO은 도메인 모델, 도메인 객체가 맞지만, Entity와 Value Object를 바로 사용하지는 않음
    - 타이어와 엔진은 자동차라는 집합체를 통해서 사용
      - 타이어와 엔진을 집적 다루는 것은 비즈니스를 위한것이 아님
      - 자동차 부품을 모두 직접 컨트롤 하는 것과 자동타 단위로 접근하는 것은 차원이 다른 문제
  - 불변식(무결성)과 일관성을 파괴하는 일이 없도록 집합체가 경계를 만들어줌
    - 불변식은 우리가 지켜야할 제약 조건, 규칙이라고 할수 있다.
#### 주문 예제
```text
Order
  - Identifier: order-123
  - List<LineItem>
    - ListItem
      - Identifier: item-123
      - Product: Guitar
      - Quantity: 1
      - Unit Price: 30만원
      - Total Price: 30만원
    - LineItem
      - Identifier: item-345
      - Product: Microphone
      - Quantity: 1
      - Unit Price: 20만원
      - Total Price: 20만원
```
- 100만원을 넘지 않아야 한다는 불변식이 있다고 가정할때
  - LineItem에 직접 접근하는 경우
    - 두개의 요청이 들어왔을때 100만원이 넘어갈수도 있다.
      - 50만원이라는 여유가 있으니 기타를 한대 더 구입한다
      - 50만원이라는 여유가 있으니 마이크를 2개 더 구입한다
      - 결과적으로 120만원이 되어버림 -> 불변식을 지키지 못함
  - Order라는 Entity를 Aggregate Root, Order를 통해 접근
  - ```java
    Order order = orderRepository.findById("order-123").get();
    order.addItem("Guitar", 1);
    ```
    - OOP에서 말하는 협력하는 객체를 더 잘 구성
    - 책임, 위임, 관심사의 분리 등을 고민하고 적용할 수 있다.

Vaughn Vernon이 제안한 4가지 제안 법칙
- 불변식을 통해서 일관성 경계를 찾아서 모델링한다. (여기서는 Order)
  - Aggregate는 트랙잭션적 일관성 경계와 동의어이다. (100만원을 넘으면 안된다)
- 작은 Aggregate를 설계한다.
- ID로 다른 Aggregate를 참조한다.
  - 일관성 경계 밖인 User를 참조하려면 UserID로 참조
- 일관성 경계 밖에서는 결과적 일관성을 사용한다.
  - 도메인 이벤트 등을 활용할수 있다.
    - 수량이 많아져서 주문이 막히거나 한다면 다르게 다루어야 할 수도 있음
    - 단순한 카운팅이면 도메인 이벤트 활용 가능

4. Repository
- Aggregate를 관리하는 Collection처럼 작동
  1. 오직 Aggregate만 Repository를 갖는다
      - Order라는 일관성 경계가 생기면 LineItemRepository는 없음
  2. Repository는 영속화 방법 및 기술을 감춘다
  - Spring Data JPA는 위 둘을 만족시키기 위한 기능이 있음
    - CascaseType.ALL
    - orphanRemoval=true
    - Persistance Context를 통해 Collection처럼 사용하는게 가능하다.
    - Interface만 만들면 나머지는 크게 신경 쓰지 않아도 되는 기능
    - Repository는 전역적으로 접근할 수 있어야 하는데, Spring의 DI를 통해 간단히 접근

## 결론
- 적절한 Aggregate를 발견하고 적절히 책임을 나눌수 있도록 Entity와 Value Object로 구성
  - 이를 위한 Repository를 만들어 여러 기술 문제와 무관한 비즈니스 도메인에 집중할수 있게 된다
  - 비즈니스 도메인에 집중한 코드를 모아둔 곳을 Domain Layer
  - Repository와 Aggregate를 사용하는 코드가 모인 곳을 Application Layer
    - 애플리케이션의 기능, Use Case가 나열되어 있게 됨
  - Web등 구체적인 기술로 사용자와 소통하는 코드가 모인 곳을 UI Layer
  - Layered Architecture와 DDD가 함께 다루어지는 이유임
    - Layered Archtecture의 도움없이 도메인 모델을 Domain Layer에 격리하는게 불가능
    - 다른 레이어도 중요하지만, 도메인 계층을 분리하여 도메인 로직에 집중할수 있게 된다. 
      - Model Driven Design이 가능한 것은 결정적으로 도메인 계층을 분리하는 데 있다.