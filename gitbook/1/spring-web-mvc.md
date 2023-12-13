# Spring Web MVC

## MVC Architecture Pattern

Model View Controller \[[Link](https://martinfowler.com/eaaCatalog/modelViewController.html)]

GUI Architecture \[[Link](https://martinfowler.com/eaaDev/uiArchs.html)]

### View, Controller, Model

#### 계층구조

\[사용자] - \[View] - \[Controller] - \[Model]

#### Controller(입력)

사용자의 입력을 통해 Model을 조작 ("무엇을" 할지 결정)

#### View(표현)

사용자와 상호작용하는 UI 부분

RESTful API를 구성하는 경우 데이터의 '표현'형식을 의미

#### Model(그외 모든 것)

사실상 도메인 모델

UI와 비즈니스 로직의 분리

Active Record\[[Link](https://martinfowler.com/eaaCatalog/activeRecord.html)]

* Model과 DB를 긴밀하게 연결

Spring Web MVC

* Map과 유사한 Model 인터페이스를 제공\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/ui/package-summary.html)] (템플릿 뷰?)
* 애플리케이션 전체가 아니라 웹과 관련된 부분에서만 MVC 개념을 활용할수 있도록 함
  * 관심사의 분리 심화

Hexagonal Architecture\[[Link](https://en.wikipedia.org/wiki/Hexagonal\_architecture\_\(software\))]\[[Link](https://dzone.com/articles/hexagonal-architecture-what-is-it-and-how-does-it)]

* AKA. Ports and adapters architecture
* Nested Layers ("Hexa" is not the matter)
* Get Your Hands Dirty on Clean Architecture\[[Link](https://github.com/thombergs/buckpal/blob/master/src/main/java/io/reflectoring/buckpal/adapter/in/web/SendMoneyController.java)]
  * Clean Architecture 실습

## Spring&#x20;

### Controller

Annotation이 보이면 전부 들어가서 확인하는 습관을 들이자

* @RestController\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RestController.html)]
  * @Controller\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Controller.html)]
  * @ResponseBody\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/ResponseBody.html)]
* @GetMapping\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/GetMapping.html)]
  * @RequestMapping\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/RequestMapping.html)]

```java
@RestController
public class WelcomeController {
	@GetMapping("/")
	public String home() {
		return "Hello, world!";
	}
}
```

