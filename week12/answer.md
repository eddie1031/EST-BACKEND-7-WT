# 12주차 정리 정답
**1-12. 다음의 상황을 확인하여 올바르게 동작하도록 명령어를 작성하여 주십시오.**  

- 상황
<그림 1> `TASKS` 테이블  
![ERD](https://github.com/user-attachments/assets/e995afc8-6b42-4a10-982d-796b97bfb61c)  
```text
1. <그림 1> 을 참고하여 테이블과 매핑할 Entity 클래스를 구성해주세요.
2. 생성에 제한을 두기 위하여 기본 생성자(Constructor)의 접근 제어자는 `protected`로 설정합니다.
3. 프로젝트에 `Lombok`은 주입 되어있습니다. 
4. Spring Data JPA(Hibernate)를 기준으로 작성해주세요.
5. 기본 키(Primary Key) 생성 전략은 자동키 생성(auto increment) 전략입니다.
6. `task_code` 컬럼은 `unique` 제약조건이 있습니다.
7. `start_time`과 `end_time` 컬럼은 날짜(Date)만 저장합니다.
8. `created_at`과 `updated_at` 컬럼은 날짜와시간(Datetime)을 저장합니다.
```

- 문제
```java
@Getter
@(1) 
@(2)  
@(3) 
class Task {
	
	@(4)
	@Column(name = (5))
	@GeneratedValue(strategy = GenerationType.(6))
	private Long id;

	@(7)
	private String code;
	
	private String title;
	
	@(8)
	private String description;

	private Integer priority;

	private (9) startTime;
	private (10) endTime;

	private (11) createdAt;
	private (12) updatedAt;

}
```

1. (1)에 들어갈 명령어를 작성해주세요.
```java
@Entity
```
2. (2)에 들어갈 명령어를 작성해주세요.
```java
@Table(name = "tasks")
```
3. (3)에 들어갈 명령어를 작성해주세요.
```java
@NoArgsConstructor(access = AccessLevel.PROTECTED)
```
4. (4)에 들어갈 명령어를 작성해주세요.
```java
@Id
```
5. (5)에 들어갈 명령어를 작성해주세요.
```java
"tasks_id"
```
6. (6)에 들어갈 명령어를 작성해주세요.
```java
IDENTITY
```
7. (7)에 들어갈 명령어를 작성해주세요.
```java
@Column(name = "task_code", unique = true, nullable = false)
```
8. (8)에 들어갈 명령어를 작성해주세요.
```java
@Column(columnDefinition = "TEXT") 
```
9. (9)에 들어갈 명령어를 작성해주세요.
```java
LocalDate
```
10. (10)에 들어갈 명령어를 작성해주세요.
```java
LocalDate
```
11. (11)에 들어갈 명령어를 작성해주세요.
```java
LocalDateTime
```
12. (12)에 들어갈 명령어를 작성해주세요.
```java
LocalDateTime
```

**13-15. 다음 빈칸에 알맞은 단어를 작성해주세요.**  
13. JavaScript에서 (FetchAPI)는 비동기적으로 HTTP 요청을 보내고 응답을 처리할 수 있게 해주는 인터페이스로서, 이전에 사용하던 (XMLHttpRequest) 객체에 비해 사용이 간편하고 유연한 기능을 제공합니다.  
14. Promise 객체에는 Pending, Fulfilled, Rejected 총 3가지 상태가 존재합니다. 이 중 초기 상태로서 비동기 작업이 아직 완료되지 않았거나 결과가 확정되지 않은 상태는 (Pending)상태 입니다.  
15. `fetch()`에서는 우선 Response 객체를 반환합니다. 이 객체는 서버의 응답을 나타내며, 응답코드, 응답 본문 등의 내용을 포함하고 있습니다. 따라서 첫 번째 (then())에서는 이를 처리하여 본문을 (json())을 통해서 객체형식으로 파싱하고, 그 결과를 두 번째 (then())에서 처리합니다.  
