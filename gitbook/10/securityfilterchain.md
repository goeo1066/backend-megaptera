# SecurityFilterChain

간단한 설정으로 기본 인증을 비활성화하고, 원하는 인증 절차를 추가할 수 있다.

```java
@Configuration
@EnableWebSecurity
public class WebSecurityConfig {
  @Bean
  public SecurityFilterChain securityFilterChain(HttpSecuriy http) 
          throws Exception {
      http.authorizeHttpRequests(authorize -> {
          authorize.anyRequest().authenticated();
      });
      
      return http.build();
  }
}
```

401 Unauthorized가 발생했지만, 이제부터는 403 Forbidden이 발생하게 된다. 기본 인증을 사용한다고 세팅하지 않았기 때문에, 자연스럽게 기본 인증이 비활성화 된다.

## OncePerRequestFilter

SecurityFilterChain은 HTTP 요청에 대래 여허 Filter를 먼저 실행할 수 있게 만들어져있다.

jakarta.servlet.FIlter는 3개의 메서드를 구현해야 하는 interface.

Spring Web은 OncePerRequestFilter으로 간단히 doFIlterInternal만 구현하면 된다.

```java
@Component
public class AccessTokenAuthenticationFilter extends OncePerRequestFilter {
    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) 
            throws ServletException, IOException {
        // 인증처리
        
        filterChain.doFilter(request, response); // 다음 필터 실행
    }
}
```

작성된 인증 필터를 기본 인증 필터보다 먼저 실행되도록 추가하면 된다.

```java
@RequiredArgsConstructor
@Configuration
@EnableWebSecurity
public class WebSecurityConfig {
    private final AccessTokenAuthenticationFilter authenticationFilter;
    
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http)
            throws Exception {
        http.addFilterBefore(
            authenticationFilter, BasicAuthenticationFilter.class);
        
        http.authorizeHttpRequests(authorize -> {
            authorize.anyRequest().authenticated();
        );
        
        return http.build();
    }
}
```

AccessTokenAuthenticationFIlter에서 인증처리

```java
Authentication authentication = UsernamePasswordAuthenticationToken.authenticated(
    "Username", "Credential", List.of()
);

SecurityContextHolder.getContext().setAuthentication(authentication);

filterChain.doFilter(request, response);
```

SecurityContext로 SpringSecurity의 인증 여부 등을 관리하고 Controller 등에 전달한다.&#x20;

UsernamePasswordAuthenticationToken 클래스로 간단히 Authentication 객체를 만들 수 있다.

일반적으로 Principal로 사용자를 지정하고, Authorities에 권한을 지정한다.



AccessTokenService
