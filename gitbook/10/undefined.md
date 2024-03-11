---
description: 인증/인가/암호화
---

# 애플리케이션 수준의 보안

## 인증(Authentication)

> 로그인 요청 등을 통해 통신 상에서 보내는 사람의 디지털 정체성을 확인하는 시도의 과정이다.

신원/신분을 검증하고 증명하는과정.

Username(한국에서는 주로 ID라고 함), Password, OTP 등의 인증 시스템을 활용하게 됨

HTTP는 무상태 프로토콜이고, 매 요청마다 인증을 하게 됨

* 세션이나 토큰 등을 통해, 사용자 경험 관점에서는 처음에 한번 인증을 하고, 세션이 유지되는 동안에는  다시 인증을 하지 않음

## 인가(Authorization)

> [인가](https://ko.wikipedia.org/wiki/%ED%97%88%EA%B0%80\_\(%EC%BB%B4%ED%93%A8%ED%84%B0\_%EA%B3%BC%ED%95%99\))

인가는 허가의 문제이다.&#x20;

일반적으로 인증과 인가는 함께 사용된다.

* 관리자임을 증명하고(인증), 관리자가 아닌 사용자는 접근 거부(인가)
* 사용자 입장에서, 로그인 페이지를 통해 인증을 완료하면 이후에는 접근이 거부 될 때 인가 과정이 있었다는 것을 알 수 있게 된다.
* 클라이언트(주로 브라우저) 입장에서는, 로그인 과정을 통해 토큰이나 세션ID 등을 얻게 되고 이를 쿠키나 LocalStorage 등으로 관리하면서, 매 요청마다 서버로 전달. 매 요청마다 인가 과정이 있다고 가정한다.
* 서버입장에서는 모든 요청에 대해 인증 작업이 수행된다. 로그인 등을 통해 발행한 토큰 등을 매 요청 바다 확인하고 사용자가 누구인지 알아낸다.(인증) 인증 후 적절한 접근 권한이 있는지 확인하고 접근을 허용 또는 금지한다.(인가)

Spring Web MVC에서는 HandlerInterceptor, Spring Security에서는 Security Filter Chain을 통해 원하는 코드를 먼저 실행할 수 있다.

> * [HandlerInterceptor](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/servlet/HandlerInterceptor.html)
> * [SecurityFilterChain](https://docs.spring.io/spring-security/reference/servlet/architecture.html#servlet-securityfilterchain)

## 암호화(Encryption)

> [암호화](https://ko.wikipedia.org/wiki/%EC%95%94%ED%98%B8%ED%99%94)
>
> [해시 함수](https://ko.wikipedia.org/wiki/%ED%95%B4%EC%8B%9C\_%ED%95%A8%EC%88%98)
>
> [암호화 해시 함수](https://ko.wikipedia.org/wiki/%EC%95%94%ED%98%B8%ED%99%94\_%ED%95%B4%EC%8B%9C\_%ED%95%A8%EC%88%98)
>
> [Bcrypt](https://ko.wikipedia.org/wiki/Bcrypt)
>
> [Scrypt](https://en.wikipedia.org/wiki/Scrypt)
>
> [Argon2](https://ko.wikipedia.org/wiki/Argon2)
>
> [Balloon hashing](https://en.wikipedia.org/wiki/Balloon\_hashing)

원래 값을 남들이 알기 어렵도록 변환하여 암호문을 만드는 작업

암호화/복호화: 평문 <> 암호문

단방향 암호화: 평문 <> 암호문 (비가역적)



단 방향 암호화를 위해 암호학적 해시 알고리즘을 사용하고, 암호학적 해시 알고리즘은 다음의 성질을 갖는다.

1. 역상 저항성 (Preimage resistance)
   1. 역상 추측에 저항하는 성질
   2. 해시 값에서 원래 값을 찾을 수 없어야 한다.
2. 제2 역상 저항성
   1. 역상 추측에 저항하는 성질
   2. 최초의 입력 값이 확인된 상태에서 동일한 해시 값이 나오는 다른 입력 값을 찾는 것이 불가능
3. 충돌 저항성
   1. 서로 다른 입력 값 추측에 저항하는 성질
   2. 확인된 정보가 없는 상태에서, 동일한 해시 값의 서로 다른 입력 값을 찾는 것이 불가능

* 제2 역상 저항성 Vs. 충돌 저항성
  * 제2 역상 저항성
    * 해시 값을 보고 동일한 해시 값을 내는 다른 입력 값을 계산 할 수 없어야 한다.
    * 예) 해시 값 3을 보고, 13, 23, 33 등 값은 해시 값을 내는 입력 값을 찾을 수 없어야 함
  * 충돌 저항성
    * 서로 다른 입력 값에 대해 동일한 해시 값이 나오면 안 된다.
    * 예) 서로 다른 1, 11, 21에 대해 같은 해시 값, 1이 나오면 안 됨

BCrypt나 SCrypt를 많이 사용했는데, 최근에는 Argon2나 Balloon을 사용한다.

Argon2는 2015년 Password Hashing Competition에서 우승했고, Spring Security에서도 지원함

> [Argon2PasswordEncoder](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/crypto/argon2/Argon2PasswordEncoder.html)
