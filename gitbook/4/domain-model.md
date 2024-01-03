# Domain Model

```java
public class Post {
  public Post(PostId id, String title, MultilineText content) {
    // 타입을 많이 잡아 놓을수록 하나하나가 명확해진다
  }
}
```

* ID나 MultilineText등 단순 문자열(혹은 다른 데이터 타입)이 아니라 온전한 역할을 하는 하나의 객체로 본다.
