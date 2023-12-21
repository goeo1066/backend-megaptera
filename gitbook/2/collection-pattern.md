# Collection Pattern

## Collection Pattern

* REST의 원래 의미보다 오히려 더 중요하게 생각하는 경우도 있다
* Collection Pattern을 쓰지 않는 경우:
  * `/the-first-post`
  * `/test-post`
* Collection Pattern을 쓰는 경우:
  * `/posts` ⇒ 모든 게시물을 하나의 URI로 표현(게시물 목록으로도 활용 가능). 일반적으로 복수형을 사용한다.
  * `/posts/the-first`
  * `/posts/test`
  * `/posts/{id}` 또는 `/posts/:id`
    * 일반적인 형태로 쓸 수 있다. 여기서 {id}를 {post\_id}나 {postId} 등으로 표기할 수도 있다. 여기서는 그냥 Post ID라고 부를 예정.
* Resource ID == URI == URL

그룹명은 복수(Plural)로 단수형을 지정할때도 복수형을 쓴다.

* /items/1 => 맞음
* /item/1 => 쓸수는 있지만 컬렉션 패턴에서는 복수형을 쓴다.
* /posts/{post\_id}/comments
  * 연관된 포스트를 알수 있다.
  * /comments?post\_id={post\_id} => 가능 Post ID로 필터링 하는 느낌
* /comments/{comment\_id}
  * 연관된 포스트를 알수 없다.
* /posts/{id}/edit
  * 이렇게 쓰지마라 (프론트에서는 쓸수 있겠지만)
* 그룹이 아닌 경우라면 단수사용 가능
  * /session 세션은 하나만 유지된다. /sessions/1 같은 접속이 있으면 안된다

## 참고

Web API 디자인의 모범사례\[[Link](https://learn.microsoft.com/ko-kr/azure/architecture/best-practices/api-design#organize-the-api-design-around-resources)]
