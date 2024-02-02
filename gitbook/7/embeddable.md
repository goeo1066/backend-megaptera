# Embeddable

> [Configuring an Aggregate Mapping](https://docs.oracle.com/cd/E16439\_01/doc.1013/e13981/cmp30cfg011.htm)
>
> [Java Persistence/Embeddables](https://en.wikibooks.org/wiki/Java\_Persistence/Embeddables)

OOP에서는 Primitive Type대신 Value Object 사용을 적극 권장 (의미가 명확해짐)

```java
String name;
String gender;
```

String은 name과 gender의 의미를 명확히 하지 못한다.

```java
@Embeddable
class Gender {
   @Column(name = "gender")
   private string value;
   
   protected Gender() {
   }
   
   protected Gender(String value) {
      this.value = value;
   }
   
   public static Gender male() {
      return new Gender("남");
   }
   
   public static Gender female() {
      return new Gender("여");
   }
   
   @Override
   public String toString() {
      return value;
   }
}
```

```java
@Embedded
Name name;
@Embedded
Gender gender;
```
