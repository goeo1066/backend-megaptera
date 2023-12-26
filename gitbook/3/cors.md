---
description: Cross-Origin Resource Sharing
---

# CORS

[CORS](https://github.com/ahastudio/til/blob/main/http/20201205-cors.md), [Same-Origin Policy](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin\_policy), [MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)(CORS), [Access-Control-Allow-Origin](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)

웹 브라우저가 처리하는 보안정책

* 서버에서는 이미 처리를 끝내고 결과를 준 상태
* 리소스의 출처가 Front-end의 주소가 다르면 접근 할수 없게 하는 보안 정책
* 출처에는 Port가지 포함된다.

## JSONP

[Link](https://ko.wikipedia.org/wiki/JSONP)

\<script>태그는 동일 출처를 따지지 않는다. JSON을 직접 전달하지 않고 실행되는 자바스크립트 코드를 전달한다.

```html
<script>
	window.success = (data) => {
		// 얻은 데이터를 처리하는 코드
		console.log(data);
	}
</script>

<script src="<http://server/posts?callback=success>"></script>
```

서버에서는 JSON이 아니라 JavaScript 코드를 생성.

```javascript
“callback” query parameter로 들어온 콜백 함수명([
	{ id: '1', title: '제목', content: '내용' }
]);
```

이제는 그냥 CORS를 활용하자

## Access-Controll-Allow-Origin

Back-end에서 안전한 접근이라고 알려주는 방식

### 응답 메시지

```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://ahastudio.com
(...자세한 헤더는 생략…)
(빈 줄)
[
	{
		"id": "123",
		"title": "재밌는 이야기",
		"content": "는 다음 기회에…"
	}
]
```

## Spring Web MVC에서의 CORS

### [HttpServletResponse](https://javaee.github.io/javaee-spec/javadocs/javax/servlet/http/HttpServletResponse.html)

```java
@GetMapping
public List<PostDto> list(
	HttpServletResponse response
) {
	response.addHeader("Access-Control-Allow-Origin", "<http://localhost:3000>");
```

Origin과 무관하게 모든 요청을 허용

```java
response.addHeader("Access-Control-Allow-Origin", "*");
```

### [@CrossOrigin](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/CrossOrigin.html)

Spring Web에선 @CrossOrigin 애너테이션을 써주면 된다. 클래스, 메서드 모두 지정 가능.

```java
@CrossOrigin("http://localhost:3000")
```

모든 요청을 허용할 거라면 마찬가지로 “\*”로 잡아주면 된다.

```java
@CrossOrigin("*")
```

아무 것도 안 써도 동일함.

```java
@CrossOrigin
```

### WebMvcConfigurer

WebMvcConfigurer 인터페이스에 대한 Spring Bean으로 환경 설정.

```java
@Bean
	public WebMvcConfigurer webMvcConfigurer() {
		return new WebMvcConfigurer() {
		
		@Override
		public void addCorsMappings(CorsRegistry registry) {
			registry.addMapping("/**")
							.allowedMethods("GET", "POST", "PATCH", "DELETE", "OPTIONS")
							.allowedOrigins("<http://localhost:3000>");
		}
	};
}
```

마찬가지로 “\*”을 쓰거나 allowedOrigins 메서드를 따로 써주지 않으면 모든 요청을 허용할 수 있다.
