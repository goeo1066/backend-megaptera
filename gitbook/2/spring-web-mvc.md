# Spring Web MVC

### Spring Web MVC로 구현

하나의 컨트롤러로 하나의 리소스 Collection을 표현하는 게 일반적. 리소스를 잘 식별하는 게 중요함.

```java
@RestController
@RequestMapping("/posts")
public class PostController {
	@GetMapping("/")
	public String list() {
		return "게시물 목록";
	}

	@GetMapping("/{id}")
	public String detail(@PathVariable("id") String id) {
		return "게시물 상세: " + id;
	}

	@PostMapping("/")
	@ResponseStatus(HttpStatus.CREATED)
	public String create(@RequestBody String body) {
		return "게시물 생성: " + body;
	}

	@PatchMapping("/{id}")
	public String update(@PathVariable("id") String id, @RequestBody String body) {
		return "게시물 수정: " + id + " with " + body;
	}

	@DeleteMapping("/{id}")
	public String delete(@PathVariable("id") String id) {
		return "게시물 삭제: " + id;
	}
}
```

> Post Response Status Code = 201 (Created)

### 에러 핸들링

```java
// Some code
@ExceptionHandler(Exception.class)
```

Bulk 수정/삭제 등은 별도 패턴이 없으니 알아서 만들고 문서를 정확하게 만듬

* query를 쓴다던지
* 컨트롤러를 너무 크지 않게 유지하자

PostController안에서 Comment 컨트롤을 하지말자

### 참고

#### 서적

* [RESTful Web API](http://aladin.kr/p/zGUKk)
* [웹 API 디자인](http://aladin.kr/p/byC7Y)
