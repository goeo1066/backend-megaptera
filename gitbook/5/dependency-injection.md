# Dependency Injection

## Spring AOP(Aspect Oriented Programming)

핵심관심사, 횡단관심사를 분리하여 프로그램을 작성하는 패러다임

### 핵심관심사(Core concerns)

비즈니스 로직, 프로그램 흐름을 따라 갖게 되는 관심사

### 횡단관심사(Cross-cutting concerns)

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption><p>Cross-Cutting Concerns(Source: <a href="https://d2.naver.com/helloworld/3010710">Naver D2</a>)</p></figcaption></figure>

프로그램의 수행절차에 따라 구성된 관심사가 아니라, 프로그램의 수행절차를 횡단하여 갖게 되는 관심사

* 로깅, 보안, 권한 체크 등
* 필요한 것들은 대부분 스프링에서 구현이 되어있으므로 따로 구현할 일이 거의 없다.

## Dependency Injection

프로그램 실행에 필요한 의존 코드를 외부에서 주입한다. 스프링에서는 두가지 방법이 있다:

Setter Injection, Constructor Injection

```java
// Setter Injection 예시
@Autowired
private PostRepository postRepository;
```

```java
// Constructor Injection 예시
@Service
public class PostService {
    // 아래처럼 final 필드를 강력 권장
    private final PostRepository postRepository;
    
    public PostService(PostRepository postRepository) {
        this.postRepository = postRepository;
    }
}
```

## IoC(Inversion of Control)

> [제어 반전](https://ko.wikipedia.org/wiki/%EC%A0%9C%EC%96%B4\_%EB%B0%98%EC%A0%84)
>
> [Inversion of Control](https://martinfowler.com/bliki/InversionOfControl.html)
>
> [Dependency Injection](https://github.com/ahastudio/til/blob/main/oop/dependency-injection.md)
>
> [Inversion of Control Containers and the Dependency Injection pattern](https://martinfowler.com/articles/injection.html)

> **"Don't call us, we'll call you" (aka. Hollywood Principle)**

Method의 호출 시점이 개발자가 아닌, 프로그램이 필요한 시점에 불린다.

IoC는 프레임워크의 공통적인 특징이다.

## Factory

> [Factory (Object-oriented programming)](https://en.wikipedia.org/wiki/Factory\_\(object-oriented\_programming\))
>
> [Plugin](https://martinfowler.com/eaaCatalog/plugin.html)

객체를 직접 만들지 않고, 객체를 생성하는 책임만 가진 객체를 만들어서 쓴다.

* 팩토리를 이용해 객체를 싱글턴처럼 쓸 수 있다.
* 단일책임원칙(SRP; Single Responsibility Principle)\[[참고](https://en.wikipedia.org/wiki/Single\_responsibility\_principle)]

> SOLID Principles(Five Design Principle)\[[참고](https://en.wikipedia.org/wiki/SOLID)]

## Singleton Pattern

> [Singleton Pattern](https://ko.wikipedia.org/wiki/%EC%8B%B1%EA%B8%80%ED%84%B4\_%ED%8C%A8%ED%84%B4)

하나의 인스턴스를 보장하기 위해 사용.&#x20;

전역 상태를 관리함에 있어서 안티패턴으로 간주되기도 함.

SOLID 원칙 위배 (SRP, DIP, OCP)

## BeanFactory

> [BeanFactory](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/BeanFactory.html)
>
> [BeanDefinitionRegistry](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/support/BeanDefinitionRegistry.html)
>
> [GenericBeanDefinition](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/support/GenericBeanDefinition.html)
>
> [Given-When-Then](https://github.com/ahastudio/til/blob/main/blog/2018/12-08-given-when-then.md)

### Spring Bean

Spring이 관리하는 객체를 Bean이라고하고, 대게 "Spring Bean"이라고 정확히 예기한다.
