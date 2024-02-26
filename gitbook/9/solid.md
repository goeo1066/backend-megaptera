---
description: 객체지향 설계 원칙
---

# SOLID

## SOLID

5가지 객체지향 설계 원칙 \
엉클 밥이 2003년 "클린 소프트웨어"에서 언급

1. SRP (Single Responsibility Principle, 단일 책임 원칙)
2. OCP (Open-Closed Principle, 개방-폐쇄 원칙)
3. LSP (Liskov Substitution Principle, 리스코프 치환 원칙)
4. ISP (Interface Segregation Principle, 인터페이스 분리 원칙)
5. DIP (Dependency Inversion Principle, 의존관계 역전 원칙)

전체적으로 한 모듈 수정이 전체 프로그램에 주는 영향이 최소화되도록 한다.

### SRP (Single Responsibility Principle)

> 1979년 톰 드마르코([_Structured Analysis and System Specification_](https://archive.org/details/structuredanalys0000dema/page/n9/mode/2up))와 메이릴 페이지 존스([Practical Guide to Structured Systems Design](https://www.goodreads.com/book/show/1441004.Practical\_Guide\_to\_Structured\_Systems\_Design))가 언급한 응집도를 다루는 설계 원칙.&#x20;

> 엉클밥은 SRP를 "각 소프트웨어 클래스(모듈)는 변경에 대한 이유를 하나만 가져야 한다" 라고 했다. _(_[_The Single Responsibility Principle (SRP) states that each software module should have one and only one reason to change_](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html)_)_

테스트하기 쉽고, 재사용하기 편하며, 더 작고 이해하기 쉬운 클래스를 얻게 된다.&#x20;

### OCP (Open-Closed Principle)

> [The Open-Closed principle](https://web.uettaxila.edu.pk/CMS/AUT2011/seSCbs/tutorial/Object%20Oriented%20Software%20Construction.pdf) (Bertrand Meyer)&#x20;

소프트웨어의 모듈은 확장에 대해 열려있고 수정에 대해서는 닫혀있어야 한다.

1. Open: 모듈의 기능을 변경할 수 있어야 한다.
2. Close: 변경이 다른 곳으로 퍼져나가지 않아야 한다.

추상화를 통해 달성가능하고 Java에서는 interface를 활용한다.

CartRepository라는 인터페이스를 만들고, JdbcCartRepository를 구현했다가 MongoCartRepository를 새로 구현을 해도 CartRepository를 사용한 곳은 수정이 필요없다.

### LSP (Liskov Substitution Principle)

> [Barbara Liskov](https://pmg.csail.mit.edu/\~liskov/)

데이터 추상화의 본질을 기술

“타입 S의 각 객체 o1과 타입 T의 각 객체 o2가 있을 때, T로 프로그램 P를 정의했음에도 불구하고, o2를 o1로 치환할 때 P의 행위가 변하지 않으면, S는 T의 서브타입이다.”

자식 클래스는 항상 부모 클래스의 역할을 충실히 수행하여야 한다.

#### 직사각형 - 정사각형 예제

```java
public class Rectangle {
    private double width;
    private double height;
    
    public void setWidth(double width) {
        this.width = width;
    }
    
    public void setHeight(double height) {
        this.height = height;
    }
    
    public double getArea() {
        return width * height;
    }
}

public class Square {
    public void setWidth(double width) {
        this.width = width;
        this.height = width;
    }
    
    public void setHeight(double height) {
        this.height = height;
        this.width = height;
    }
}

public class Main {
    public static void main() {
        Rectangle rectangle = new Square();
        rectangle.setHeight(4);
        rectangle.setWidth(5);
        assert rectangle.getArea() == 20; // 에러
    }
}
```

의존성 주입을 받는 상황이라면 에러의 원인을 더욱 찾기 힘들어진다.

Shape 인터페이스에 getArea()만을 명시하여, Rectangle, Square를 따로 구현을 해서 해결하거나,

상속을 없애 해결을 할수가 있다.



행위의 측면에서 Rectangle과 Square는 명확히 분리된다.

### ISP (Interface Segregation Principle)

사용하지 않는 메서드를 구현하도록 강제해서는 안된다는 것을 의미

응집력이 없는 커다란 인터페이스를 여러개의 작은 인터페이스로 나눌 것을 제안한다.

> A.K.A [Role Interface](https://martinfowler.com/bliki/RoleInterface.html)
>
> High Cohension Principle of [GRASP](https://en.wikipedia.org/wiki/GRASP\_\(object-oriented\_design\))

ISP는 시스템의 결합도를 낮추고, 리팩토링, 수정, 재배포를 용이하게 한다.

분산 시스템 설계에서 핵심 원칙

> [Six IDEALS principles](https://www.infoq.com/minibooks/reexamining-microservices/) for microservice design

> 로버트 C. 마틴이 제록스사에 컨설팅을 하다가 처음 사용되며 알려졌다. 제록스가 새로운 프린터 시스템을 만들었는데, 자동 스테이플링,  팩스 전송 같은 것들이었다. 소프트웨어는 바닥부터 만들어졌으며, 소프트웨어가 커짐에 따라, 수정이 매우 어려워졌고, 심지어 아주 작은 변화조차 재배포에 1시간이상 걸렸다. 이로 인해 배포작업이 거의 불가능해졌다.
>
> \
> 하나의 클래스가 대부분의 작업에서 사용되도록 했던 설계가 문제였다. 프린트 작업이나 스테이플링 작업을 수행할때도 그 클래스가 호출되었다. 결과적으로 다양한 구체적 구현체가 있는 하나의 'fat'클래스가 되었다. 이런 설계로 인해 스테이플링 작업도 사용하지도 않는 프린트 작업에 대해 모두 알게 되었다.\
> \
> 이때 마틴은 ISP를 솔루션으로 제안한다. 제록스 소프트웨어에 적용되었으며 필요한 클래스는 DIP를 적용하여 인터페이스를 필요로 하는 곳에 추가하였다.&#x20;

### DIP (Dependency Inversion Principle)

1. 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안된다. 둘 다 추상화에 의존해야 한다.
2. 추상화는 구체적인 사항에 의존해서는 안된다. 구체적인 사항은 추상화에 의존해야 한다.

AddProductToCartService가 JdbcCartRepository에 의존한다면, 비즈니스 로직에 가까운 Application Layer의 객체가 기술적인 문제를 다루는 Infrastructure Layer에 의존하게 된다. 기술적인 문제가 바뀔때마다 비즈니즈 로직 수정이 발생하게 된다. CartRepository를 Domain Layer에 배치하여 의존성 문제를 해결할수 있다.

변경 전: AddProductToCartService -> JdbcCartRepository

변경 후: AddProductToCartService -> CartRepository **<-** JdbcCartRepository

JdbcCartRepository로 향하던 화살표의 방향이 바뀌었다.

스프링을 이용하면 아주 쉽게 DI, DIP를 활용할 수 있게 된다.

