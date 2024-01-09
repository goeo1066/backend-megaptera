# Data Access

```java
return new ArrayList(list);
// 내부에 있는 컬렉션을 바깥에 바로주는것은 좋지 않다. 
```

### Repository

DDD에서 나온 개념, 영구 저장소의 개념이 아니라 Entity의 Collection의 개념.&#x20;

Entity에 대한 CRUD를 수행한다.&#x20;

내부적으로 List나 HashMap사용하는지 스토리지로 저장하는지 상관없다.

> Repository\[[Link](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/stereotype/Repository.html)]
>
> Indicates that an annotated class is a "Repository", originally defined by Domain-Driven Design (Evans, 2003) as "a mechanism for encapsulating storage, retrieval, and search behavior which emulates a collection of objects".

* FindAll
* Find
* Save
* Delete

### DAO

Repository와는 다르게 영속성을 위한 객체라는 것을 숨기지 않는다.&#x20;
