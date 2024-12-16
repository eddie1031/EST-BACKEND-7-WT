# 11주차 정리 정답
**1-10. 다음의 상황을 확인하여 올바르게 동작하도록 명령어를 작성하여 주십시오.**  
- 상황
```text
1. AWS의 `EC2`서비스 중 `t2.micro` 인스턴스를 `Ubuntu 24.04` 운영체제로 시작하여 다음 항목의 `키 페어`를 발급받았습니다. 
   > 키 페어 항목
   > `id_rsa.pem`
   > 키 페어 저장 디렉토리
   > `C:\Users\est_week_10\.ssh\week11`
2. 인스턴스의 공용 IPv4는 `10.152.0.16`이고, 기본 유저는 `ubuntu`로 설정되었습니다.
3. `apt`와 `apt-get`은 업데이트 및 업그레이드가 안되어있는 상태입니다.
4. 기본 계정을 사용하지 않고 새로운 계정을 다음의 항목대로 생성하여 사용하기로 하였습니다.
   > 계정명 : est_week_11
   > 비밀번호 : est_week_11!
5. `ssh` 포트는 `22` 로서 작업용 컴퓨터 IP에서만 접근 가능하도록 설정하였습니다.
6. 새로운 계정을 위한 SSH 키는 작업용 컴퓨터 로컬에서 생성합니다. 다음과 같은 명세로 키를 생성합니다.
   > 키 페어 이름
   > `id_rsa`
   > 키 페어 저장 디렉토리
   > `C:\Users\est_week_10\.ssh\week11\app1`
```
- 문제
a. 로컬 컴퓨터 터미널
```sh
# 최초 접속 상황
ssh -i (1) (2)@(3)

# 새로운 계정을 위한 키 생성
cd (4)
ssh-keygen -t (5) -f ./id_rsa
```
 
b. `ec2@10.152.0.165` 터미널
```sh
# 최초 접속 [ubuntu]
# apt, apt-get 업데이트 및 업그레이드
ubuntu@172.0.0.0$ sudo (6) update
ubuntu@172.0.0.0$ sudo (7) upgrade
ubuntu@172.0.0.0$ sudo apt-get update
ubuntu@172.0.0.0$ sudo apt-get upgrade

# est_week_11 계정 생성
ubuntu@172.0.0.0$ sudo (8) (9)

# sudo 권한 부여
ubuntu@172.0.0.0$ sudo vim /etc/sudoers

# 계정 전환
ubuntu@172.0.0.0$ sudo (10) - est_week_11
est_week_11@172.0.0.0$ 
```

1. (1)에 들어갈 명령어를 작성해주세요
```sh
C:\Users\est_week_10\.ssh\week11\id_rsa.pem
```

2. (2)에 들어갈 명령어를 작성해주세요
```sh
ubuntu
```

3. (3)에 들어갈 명령어를 작성해주세요
```sh
10.152.0.16
```

4. (4)에 들어갈 명령어를 작성해주세요
```sh
app1

C:\Users\est_week_10\.ssh\week11\app1
```

5. (5)에 들어갈 명령어를 작성해주세요
```sh
rsa
```

6. (6)에 들어갈 명령어를 작성해주세요
```sh
apt
```

7. (7)에 들어갈 명령어를 작성해주세요
```sh
apt
```

8. (8)에 들어갈 명령어를 작성해주세요
```sh
adduser
```

9. (9)에 들어갈 명령어를 작성해주세요
```sh
est_week_11
```

10. (10)에 들어갈 명령어를 작성해주세요
```sh
su
```

**11-15. 다음의 상황을 확인하여 올바르게 동작하도록 코드를 작성하여 주십시오.**  
- 상황
```text
1. Spring Boot 기반 백엔드 애플리케이션과 React.js 기반 프론트엔드 애플리케이션이 통신하는 구조입니다.
2. 사용자는 OAuth2.0 방식으로 인증할 수 있으며, 백엔드 애플리케이션과 프론트 애플리케이션은 JWT 기반으로 인증을 수행하고 있습니다.
3. 백엔드 애플리케이션을 위한 비밀키는 `application-prod.yml`에 설정되어 있고 정상적으로 주입되어 사용 가능합니다.
4. JWT 관련 설정은 다음과 같이 되어있습니다.
jwt:
  secret:
    app-key: ....
5. JWT 토큰에는 다음과 같은 내용이 포함될 예정입니다.
- sub : 회원 번호(PK)
- claim : "role" -> 회원 등급
```

- 문제
```java
@Service
@RequiredArgsConstructor
public class JwtTokenProvider {

	// JWT 관련 설정
    private final JwtConfiguration configuration;

    private String issue(Long memberId, String role, Long validTime) {
        return Jwts.builder()
            .subject((11))
            .claim((12), (13))
            .issuedAt(new Date())
            .expiration(new Date(new Date().getTime() + validTime))
            .signWith((14), Jwts.SIG.HS256)
            .compact();
    }

    private SecretKey getSecretKey() {
        return Keys.hmacShaKeyFor(configuration.getSecret().getAppKey().getBytes());
    }

    public boolean validate(String token) {
        try {
            Jwts.parser()
                .verifyWith((15))
                .build()
                .parseSignedClaims(token);
            return true;
        }  catch ( Exception e ) {
			// 예외 처리...
        }
        return false;
    }

}

```

11. (11)에 들어갈 코드를 작성해주세요
```java
memberId.toString()
```

12. (12)에 들어갈 코드를 작성해주세요
```java
"role"
```

13. (13)에 들어갈 코드를 작성해주세요
```java
role
```

14. (14)에 들어갈 코드를 작성해주세요
```java
getSecretKey()
```

15. (15)에 들어갈 코드를 작성해주세요
```java
getSecretKey()
```