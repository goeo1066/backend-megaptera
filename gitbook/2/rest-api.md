# REST API

하나의 시스템으로 만들기도 하고 여러 부분(Tier, Layer)으로 만들기도 한다.

* Tier는 물리적인 부분
* Layer는 논리적인 부분
* Front-end(F/E): 사용자에 가까운 부분
* Back-end(B/E): 사용자에게서 먼 부분
* F/E B/E 연결:
  * HTTP, 정확히는 웹기술
    * REST API, SOAP, GraphQL
* 백엔드를 만든다기 보다, 서비스를 제공하기 위한 부분들을 쓴다.
* GraphQL: 스프링에서 지원하기는 하는데 아직 불편하다
* [API](https://ko.wikipedia.org/wiki/API)
* [정보 은닉](https://en.wikipedia.org/wiki/Information\_hiding)
* [GoF의 디자인패턴 1.6](https://github.com/ahastudio/til/blob/main/oop/glossary.md)
* [Web API](https://en.wikipedia.org/wiki/Web\_API)
* API
  * Interface
    * 연산의 시그니처: 연산의 이름, 매개변수로 받아들이는 객체, 연산의 반환값
    * Interface는 객체가 받아서 처리할 수 있는 연산의 집합
    * Communication: 서로간의 소통
    * Specification: 소통을 위한 명세
    * Information Hiding (Principle): 정보은닉 (내부? 어딘가의 뒤로, 숨기는 것을 의미)
    * Encapsulation (Technique): 캡슐화 한곳에 묶는다. 내부와 외부를 연결하는 인터페이스를 통해서만 무언가를 처리한다
    * Implementation: 분명히 무언가를 구현해줘야 된다.
    * 쓰는 방법이 원칙을 따르면 좋다.
      * 그중에 하나가 REST (로이필딩): 아키텍처를 위한 아키텍처 스타일

### [REST](https://ko.wikipedia.org/wiki/REST) (Representational State Transfer)

> **Roy Fielding** - “[Architectural Styles and the Design of Network-based Software Architectures](https://www.ics.uci.edu/\~fielding/pubs/dissertation/top.htm)” (2000)

해당 논문의 5장 - [Representational State Transfer (REST)](https://www.ics.uci.edu/\~fielding/pubs/dissertation/rest\_arch\_style.htm)

#### \[ 제약 조건 ]

1 **Starting with the Null Style**

2 **Client-Server**

3 **Stateless**

4 **Cache**

5 **Uniform Interface → 핵심!**

1. “The **central feature** that distinguishes the REST architectural style from other network-based styles is its emphasis on a **uniform interface** between components”
2. “By applying the **software engineering principle of generality** to the component interface, the overall system architecture is **simplified** and the **visibility** of interactions is improved.”
3. “**Implementations** are **decoupled** from the services they provide, which encourages **independent evolvability**.”
4. “The **trade-off**, though, is that a uniform interface **degrades efficiency**, since information is transferred in a **standardized form** rather than one which is specific to an application\`s needs.”
5. “The REST interface is designed to be efficient for **large-grain hypermedia data transfer**, optimizing for the **common case of the Web**, but resulting in an interface that is not optimal for other forms of architectural interaction.”
6.  **필딩 제약 조건** 1. Four Interface Constraints

    &#x20;Identification of Resources → URI 등으로 리소스를 식별할 수 있다. Manipulation of Resources through Representations → 표현으로 리소스를 조작한다. Self-descriptive Messages → 메시지는 자기서술적이기 때문에 여러 레이어에서 처리/변환 가능하다.

    > JSON 같은 범용 포맷을 작게 사용하면 어떻게 해석해야 하는지 알 수 없기 때문에 자기서술적이기 어렵다. 뒤에서 다룰 MIME 타입으로 설명한다면, application/json이 아니라 application/dns+json 같은 타입을 써야 한다.

    > REST API를 이야기할 때 까다로운 부분 중 하나.

    &#x20;Hypermedia as the Engine of Application State → 줄여서 HATEOAS라고 부른다. REST API를 이야기할 때 까다로운 부분 중 하나.

```
2. 아키텍처 요소(5.2)에서 리소스와 표현을 구분
```

```
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> Resource → 추상. ⇒ 특정 시점의 스냅샷이 아니라, 모든 시간에 통용되는 엔티티 집합. 객체지향에서 말하는 Entity라고 생각하면 편하다. <객체지향의 사실과 오해>의 표현을 빌린다면, “앨리스”라는 리소스는 키가 커지던 작아지던 항상 “앨리스”다.
    
    </aside>
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> Representation → Data + Metadata + Meta-metadata… ⇒ 사실상 HTTP 메시지라고 보면 됨. 예를 들어, 리소스를 어떻게 조작할 것인가는 HTTP Method로 표현하게 되고, 리소스를 무엇으로 조작할 것인가는 Content-Type과 Body로 표현하게 된다.
    
    </aside>
    
3. URI 파트(6.2)에서 리소스에 대해 다시 강조
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> “The resource is not the storage object. The resource is not a mechanism that the server uses to handle the storage object.”
    
    </aside>
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> 리소스, 표현, 실제 데이터 등은 전부 구분된다.
    
    </aside>
    
4. 아키텍처 데이터 뷰(5.3.3)에서 HATEOAS에 대해 언급.
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> 마지막 문단의 첫 문장: “The model application is therefore an **engine** that moves from one state to the next by examining and **choosing** from among the alternative **state transitions** in the current set of **representations**.”
    
    > 이렇게 하려면 표현에 선택 가능한 상태 전환이 포함돼야 한다.
    > 
    
    > 이게 바로 하이퍼미디어 링크.
    > 
    </aside>
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> 대부분은 효율 문제로 표현에 링크를 넣지 않고, 클라이언트 개발자가 API 문서를 활용해 처리한다. 표현에서 상태 전환을 선택하는 게 아니라, API 문서를 참조해서 상태 전환을 강제하는 것.
    
    </aside>
    
    <aside>
    <img src="/icons/arrow-right_gray.svg" alt="/icons/arrow-right_gray.svg" width="40px" /> [Richardson Maturity Model](https://martinfowler.com/articles/richardsonMaturityModel.html)
    
    > <RESTful Web API>의 공저자인 레오나르드 리처드슨은 Hypermedia Control(대표적인 게 바로 링크)을 강조.
    > 
    
    > 성숙한 REST라면 표현에 하이퍼미디어 컨트롤(링크)이 포함되어야 한다.
    > 
    </aside>
    
```

6️⃣ **Layered System**

7️⃣ **Code-On-Demand**

REST는 API를 위한 아키텍처 스타일이 아니다. 논문에서 밝힌 것처럼 “common case of the Web”에 특화된 방법이다. 하지만 API를 만들 때 유용하게 활용할 수 있다.

로이 필딩은 필딩 제약 조건을 지키지 않는 API를 REST API라고 부르는 것에 반대하겠지만, 업계에서 그냥 리처드슨 성숙도 모델의 레벨 2만 만족해도 REST API라고 부르고 있기 때문에 여기서도 그냥 REST API라고 이야기할 예정.
