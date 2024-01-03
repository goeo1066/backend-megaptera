# Data Access

### new&#x20;

내부에 있는 컬렉션을 바깥에 바로주는것은 좋지 않다.&#x20;

```java
return new ArrayList(list);
```

```java
return new ArrayList(list);
```

### DAO

FindAll, Find, Save, Delete

여러 데이터를 관리하는 방법은 하나가 아니다.

1. List
2. Map

PostDAO라는 인터페이스를 만들고, PostListDAO와 PostMapDAO로 구현한다(daos 패키지).
