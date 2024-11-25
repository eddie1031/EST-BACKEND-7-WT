# 9주차 정리 정답
1-3. 다음의 파일 내용을 보고 빈 칸에 알맞은 정답을 기재해주세요.  
- `db.sql`
```sql
grant all privileges
on *.*
to `est-test`@`localhost`
identified by 'Est1!'
;

drop database if exists `est_jdbc`;
create database `est_jdbc`;
use `est_jdbc`;

drop table if exists `member`;
create table `member` (
    member_id int(10) not null primary key auto_increment,
    username varchar(15) not null,
    password varchar(100) not null
);
```

- `ConnectionUtil.java`
```java
public static class MariaDbConnectionConstant {
    public static final String URL = (1);
    public static final String USERNAME = (2);
    public static final String PASSWORD = (3);
}
```

1. 상기 `sql`과 `java` 파일을 미루어 보았을 때 (1)에 들어갈 수 있는 값은 (`jdbc:mariadb://localhost:3306/est_jdbc`) 입니다.  
2. 상기 `sql`과 `java` 파일을 미루어 보았을 때 (2)에 들어갈 수 있는 값은 (est-test) 입니다.  
3. 상기 `sql`과 `java` 파일을 미루어 보았을 때 (3)에 들어갈 수 있는 값은 (Est1!) 입니다.  
  
4. (JDBC)를 사용하면 관계형 데이터베이스 벤더들이 제공하는 (Driver) 객체를 이용하여 어떠한 관계형 데이터베이스를 이용하더라도 통일된 방법으로 연결을 획득할 수 있게 됩니다.  
5. (JPA 또는 Hibernate)에서는 트랜잭션 환경 하에서 (쓰기지연)을 지원하는데, 이것을 이용하여 (변경감지)가 가능합니다. 따라서 `update()` 혹은 `save()`와 같은 메서드를 호출하지 않더라도 변경된 부분이 자동으로 데이터베이스에 반영됩니다.  
  
6. 다음의 SQL을 참고하여 `Post`라는 이름의 객체에 `JPA`에서 제공하는 어노테이션을 이용하여 엔티티 클래스를 매핑한 결과를 작성해주세요. 

```sql
create table article(
	id int not null primary key auto_increment,
	title varchar(100) not null,
	contents varchar(100)
);
```

```java
@Entity
@Table(name = "article")
public class Post {
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;
	
	private String title;
	private String contents;
}
```

7. `@GeneratedValue` 어노테이션은 기본 키(Primary Key)를 추가하는 방식을 결정하는 어노테이션입니다. 각각의 데이터베이스 별로 기본 키를 관리하는 방법이 다르기 때문에 옵션을 부여해서 사용하는데, 시퀀스가 없는 데이터베이스에서 시퀀스를 흉내내기 위해 사용하는 전략은 (Table) 전략입니다.  

8-10. 다음의 파일을 확인하여 알맞은 정답을 작성해주세요.  

- `db.sql`
```sql
create table teams(
	team_id int not null primary key auto_increment,
	name varchar(50) not null
);

create table players(
	player_id int not null primary key auto_increment,
	name varchar(50) not null,
	team_id int not null,
	foreign key(team_id) references teams(team_id)
);
```
  
8. `teams` 테이블을 `JPA`에서 제공하는 어노테이션을 이용해서 매핑한 클래스를 작성해주세요.  
```java
@Entity
@Table(name = "teams")
public class Team {
	@Id
	@Column(name = "team_id")
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Integer id;

	@Column(nullable = false)
	private String name;

}
```
  
9. `players` 테이블을 `JPA`에서 제공하는 어노테이션을 이용해서 매핑한 클래스를 작성해주세요. 이 때, 연관관계 없이 필드 그대로 매핑해주세요.  
```java
@Entity
@Table(name = "players")
public class Player {
	
	@Id
	@Column(name = "players_id")
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Integer id;
	
	@Column(nullable = false)
	private String name;
	
	@Column(nullable = false)
	private Integer teamId;
	
}
```

10. `Players` -> `team` 다대일 연관관계를 포함한 엔티티 클래스를 `JPA`에서 제공하고 있는 어노테이션을 이용하여 매핑한 `Player` 클래스를 작성해주세요.  
```java
@Entity
@Table(name = "players")
public class Player {
	
	@Id
	@Column(name = "players_id")
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Integer id;
	
	@Column(nullable = false)
	private String name;
	
	@ManyToOne
	private Team team;
	
}
```

