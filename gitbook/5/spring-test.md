---
description: Integration Test
---

# Spring Test

## Integration Test

> [Testing](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html)
>
> [Testing improvements in Spring Boot 1.4](https://spring.io/blog/2016/04/15/testing-improvements-in-spring-boot-1-4)
>
> [Testing the Web Layer](https://spring.io/guides/gs/testing-web/)

Spring의 공식 문서에서는 크게 둘로 나눠서 설명함

* Unit Testing
* Integration Testing

Spring은 구조적으로 코드에 적게 개입함 -> 단위 테스트를 쉽게 작성 할 수 있다.

IoC 컨테이너나 Spring Web MVC를 활용하여 Spring의 통합 테스트를 진행할 수 있다.

### SpringBootTest

> "@Autowired"
>
> "@SpyBean"
>
> MockMvc
>
> MockBean
>
> "@WebMvcTest"

Spring Boot 1.4부터 @SpringBootTest Annotation을 써서 쉽게 테스트할 수 있다.

```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class PostFeatureTest {
	@Value("${local.server.port}")
	private int port;
	
	@Autowired
	private TestRestTemplate restTemplate;
	
	@Test
	public void post() {
		String url = "<http://localhost>:" + port + "/posts";
		
		PostDto postDto = new PostDto("ID", "새 글", "제곧내");
		
		restTemplate.postForLocation(url, postDto);
		
		String body = restTemplate.getForObject(url, String.class);
		
		assertThat(body).contains("새 글");
		assertThat(body).contains("제곧내");
		
		String id = findLastId(body);
		
		restTemplate.delete(url + "/" + id);
		
		body = this.restTemplate.getForObject(url, String.class);
		
		assertThat(body).doesNotContain("새 글");
	}
	
	private String findLastId(String body) {
		Pattern pattern = Pattern.compile("\\"id\\":\\"([^\\"]+)\\"");
		Matcher matcher = pattern.matcher(body);
		
		String id = "";	
		while (matcher.find()) {
			id = matcher.group(1);
		}		
		return id;
	}
}
```

#### MockMvc

MockMvc를 써서 HTTP 요청을 흉내낼 수 있다.

```java
@SpringBootTest
@AutoConfigureMockMvc
class PostControllerTest {
	@Autowired
	private MockMvc mockMvc;
	
	@Autowired
	private PostRepository postRepository;
	
	@Test
	public void list() throws Exception {
		this.mockMvc.perform(get("/posts"))
			.andExpect(status().isOk())
			.andExpect(content().string(
				containsString("테스트입니다")
			));
	}
	
	@Test
	public void create() throws Exception {
		String json = """
					{
						"title": "새 글",
						"content": "제곧내"
					}
					""";
		
		int oldSize = postRepository.findAll().size();
	
		this.mockMvc.perform(
			post("/posts")
				.contentType(MediaType.APPLICATION_JSON)
				.content(json)
			)
			.andExpect(status().isCreated());
		
		int newSize = postRepository.findAll().size();
	
		assertThat(newSize).isEqualTo(oldSize + 1);
	}
}
```

한글 관련 인코딩 문제 해결

```properties
# application.properties
server.servlet.encoding.charset=UTF-8
server.servlet.encoding.force=true
```

#### Spybean

> [SpyBean](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/mock/mockito/SpyBean.html)
>
> [TestDouble](https://martinfowler.com/bliki/TestDouble.html)

“Spies are stubs that also record some information based on how they were called.”

Post 개수를 세는 게 아니라, 그냥 PostRepository의 save를 호출했는지만 확인해 보자.

```java
@Test
public void create() throws Exception {
	String json = """
				{
					"title": "새 글",
					"content": "제곧내"
				}
				""";
				
	this.mockMvc.perform(
		post("/posts")
			.contentType(MediaType.APPLICATION_JSON)
			.content(json)
		)
		.andExpect(status().isCreated());
		
	verify(postRepository).save(any(Post.class));
}
```

전달한 값이 제대로 들어갔는지 확인할 수도 있다.

```java
@Test
public void create() throws Exception {
	String json = """
				{
					"title": "새 글",
					"content": "제곧내"
				}
				""";
				
	this.mockMvc.perform(
		post("/posts")
			.contentType(MediaType.APPLICATION_JSON)
			.content(json)
		)
		.andExpect(status().isCreated());
		
	verify(postRepository).save(argThat(post -> {
		return post.title().equals("새 글");
	}));
}
```

getter를 피하기 위해 Reflection을 쓸 수도 있다. (Overengineering?!)

```java
@Test
public void create() throws Exception {
	String json = """
				{
					"title": "새 글",
					"content": "제곧내"
				}
				""";
		
	this.mockMvc.perform(
		post("/posts")
			.contentType(MediaType.APPLICATION_JSON)
			.content(json)
		)
		.andExpect(status().isCreated());
		
		verify(postRepository).save(argThat(post -> {
			return getFieldValue(post, "title").equals("새 글");
		}));
	}
	
	private Object getFieldValue(Object object, String fieldName) {
		try {
			Field field = object.getClass().getDeclaredField(fieldName);
			field.setAccessible(true);
			return field.get(object);
		} catch (NoSuchFieldException | IllegalAccessException e) {
			throw new RuntimeException(e);
		}
	}
```

#### MockBean

더 빠르게 테스트를 실행하기 위해 전부 가짜로 채워넣을 수도 있다.

```java
@WebMvcTest(PostController.class)
class PostControllerTest {
	@Autowired
	private MockMvc mockMvc;
	
	@MockBean
	private GetPostsService getPostsService;
	
	@MockBean
	private GetPostService getPostService;
	
	@MockBean
	private CreatePostService createPostService;
	
	@MockBean
	private UpdatePostService updatePostService;
	
	@MockBean
	private DeletePostService deletePostService;
	
	@Test
	public void list() throws Exception {
		given(getPostsService.getPostDtos()).**willReturn**(List.of(
			new PostDto("1", "제목", "내용")
		));
		
		this.mockMvc.perform(get("/posts"))
			.andExpect(status().isOk())
			.andExpect(content().string(
				containsString("제목")
			));
	}
	
		@Test
		public void create() throws Exception {
			String json = """
				{
					"title": "새 글",
					"content": "제곧내"
				}
				""";
		
			this.mockMvc.perform(
					post("/posts")
						.contentType(MediaType.APPLICATION_JSON)
						.content(json)
					)
					.andExpect(status().isCreated());
				
			verify(createPostService)
				.createPost(new PostDto(null, "새 글", "제곧내"));
	}
}
```
