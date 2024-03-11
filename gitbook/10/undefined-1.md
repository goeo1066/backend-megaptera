# 사용자 입장에서 기본 인증/인가

대부분 Username(또는 E-mail)과 Password를 이용해서 로그인

국제적으로나 기술적으로  Username이 주로 사용되지만, 국내에서는 Username을 ID로 표현하는 경우가 많음

Spring Security 의존성을 추가하면 HTTP 기본 인증, 인가가 적용된다.

> [Authentication](https://developer.mozilla.org/ko/docs/Web/HTTP/Authentication)

아무런 설정을 하지 않으면 개발 용으로 사용할 수 있는 패스워드가 발급된다. username은 'user'

직접 지정하고 싶다면 application.yml에 다음 내용을 추가하면 된다.

```yaml
spring:
  security:
    user:
      name: tester
      password: password
```

HTTPie로 확인

```bash
http :8080
```

\-> 401 Unauthorized (인증되지 않음)

```bash
http -a <username>:<password> :8080
```

\-> 200 OK

기본 인증 방식은 매번 username과 password를 전달하므로 탈취당할 위험이 크다. 토큰 같은 임시 키를 사용해야 한다.&#x20;

> [rfc6750](https://www.rfc-editor.org/rfc/rfc6750) (Bearer Token Usage)

```bash
http -A beare -a <accessToken> :8080
```

