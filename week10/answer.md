# 10주차 정리 정답
**1-10. 다음의 코드와 조건을 확인하여 올바른 코드를 작성해주세요.**
- `코드`: `SecurityConfiguration.java`
```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    return http
            .formLogin(Customizer.withDefaults())
            .logout(Customizer.withDefaults())
            .authorizeHttpRequests(
                    auth ->
                    auth.requestMatchers((1))
                            .(2)
                            .requestMatchers((3))
                            .(4)
                            .requestMatchers((5))
                            .(6)
                            .requestMatchers((7))
                            .(8)
                            .(9)
                            .(10)
            )
            .build();
}

```

- 조건
> 1. 회원가입 페이지(sign-up)과 로그인(login) 페이지는 `별도 인증 없이` 접근 가능하여야 합니다. 인증한 요청은 접근 불가하여야 합니다.
> 2. `/members` 하위 URL은 관리자와, 중간관리자, 회원 모두 접근 가능합니다.
> 3. `/mamangers` 하위 URL은 관리자와 중간관리자만 접근 가능합니다.
> 4. `/admins` 하위 URL은 관리자만 접근 가능합니다.
> 5. 회원 권한 체계는 다음과 같습니다.
>    1. 회원(MEMBER)
>    2. 중간관리자(MANAGER)
>    3. 관리자(ADMIN)
> 6. 그 밖의 모든 URL에 대해서는 로그인을 하여야 접근 가능합니다.

1. (1)에 들어갈 코드를 작성해주세요
   ```java
   auth.requestMatchers("/login", "/sign-up")
   ```
2. (2)에 들어갈 코드를 작성해주세요
   ```java
   .anonymous()
   ```
3. (3)에 들어갈 코드를 작성해주세요
   ```java
   .requestMatchers("/members/**")
   ```
4. (4)에 들어갈 코드를 작성해주세요
   ```java
   .hasAnyAuthority("MEMBER","MANAGER","ADMIN")
   
   // 또는
   
   .hasAnyRole("MEMBER","MANAGER","ADMIN")
   ```
5. (5)에 들어갈 코드를 작성해주세요
   ```java
   .requestMatchers("/managers/**")
   ```
6. (6)에 들어갈 코드를 작성해주세요
   ```java
   .hasAnyAuthority("MANAGER","ADMIN")
   
   // 또는
   
   .hasAnyRole("MANAGER","ADMIN")
   ```
7. (7)에 들어갈 코드를 작성해주세요
   ```java
   .requestMatchers("/admins")
   ```
8. (8)에 들어갈 코드를 작성해주세요
   ```java
   .hasAnyAuthority("ADMIN")
   
   // 또는
   
   .hasAnyRole("ADMIN")
   ```
9. (9)에 들어갈 코드를 작성해주세요
   ```java
   .anyRequest()
   ```
10. (10)에 들어갈 코드를 작성해주세요
    ```java
    .authenticated()
    ```

**11 - 15. 다음의 코드와 조건을 확인하여 올바른 코드를 작성해주세요.**
- `코드` : `MemberDetails.java`
```java
public class MemberDetails implements UserDetails {
	
	// ...

	@Override
	public Collection<? extends GrantedAuthority> getAuthorities() {
    		return List.of((11));
	}

	@Override
	public String getPassword() {
    		return this.password;
	}

	@Override
	public String getUsername() {
    		return this.username;
	}

	@Override
	public boolean isAccountNonExpired() {
    		return (12);
	}

	@Override
	public boolean isAccountNonLocked() {
    		return (13);
	}

	@Override
	public boolean isCredentialsNonExpired() {
    		return (14);
	}

	@Override
	public boolean isEnabled() {
    		return (15);
	}

}
```

- 조건
> 1. 권한은 관리자(ADMIN)만을 보유하고 있습니다.
> 2. 계정은 현재 다음과 같은 이유로 인증 불가한 상태입니다.
>    1. 계정이 만료되지는 않았습니다.
>    2. 비밀번호가 만료되었습니다.
>    3. 계정이 비활성화 되었습니다.
>    4. 2, 3의 이유로 계정은 현재 잠금(LOCK) 상태입니다

11. (11)에 들어갈 코드를 작성해주세요
    ```java
    new SimpleGrantedAuthority("ADMIN")
    ```
12. (12)에 들어갈 코드를 작성해주세요
    ```java
    true
    ```
13. (13)에 들어갈 코드를 작성해주세요
    ```java
    false
    ```
14. (14)에 들어갈 코드를 작성해주세요
    ```java
    false
    ```
15. (15)에 들어갈 코드를 작성해주세요
    ```java
    false
    ```