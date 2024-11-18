# 20241112 LevelTest 정답

## 1. 다음의 요구사항을 확인 후 올바른 SQL을 작성하여 주시기 바랍니다.
1-1. `est_comunity` 데이터베이스가 존재한다면 삭제 후 생성해주세요.

```sql
# 기존에 community 데이터베이스가 존재 한다면 삭제
DROP DATABASE IF EXISTS `est_comunity`;
# 새 데이터베이스(`community`) 생성
CREATE DATABASE `est_comunity`;
# 새 데이터베이스(`community`) 선택
USE `est_comunity`;
```

1-2. 다음 형태의 게시물을 저장할 수 있는 테이블을 생성해주세요.
```sql
CREATE TABLE article (
    id INT,
    created_at DATETIME,
    title VARCHAR(100),
    `contents` TEXT
);
```

1-3. 생성한 테이블에 다음의 게시물들을 추가해주세요.
```sql
INSERT INTO `article`
  ( title, contents )
VALUES
  ( "제목", "내용" )
;
```

1-4. `번호` 에 해당하는 `열(Column)` 을 해당 테이블의 `주 키(Primary Key)`로 변경해주세요. 번호는 1번부터 매김합니다. 또한 자동으로 번호가 증가할 수 있도록 조치해주세요.
```sql
ALTER TABLE article MODIFY id INT(10) NOT NULL;

UPDATE 
  article
SET 
  id = 1
WHERE 
  id = 0
LIMIT 1
;

UPDATE 
  article
SET 
  id = 2
WHERE 
  id = 0;

ALTER TABLE article ADD PRIMARY KEY(id);
ALTER TABLE article MODIFY COLUMN id INT(10) NOT NULL AUTO_INCREMENT;
```

1-5. 테이블의 구조를 확인 후, 나머지 모든 `열(Column)`에 `NULL` 값이 올 수 없도록 조치해주세요.
```sql
DESC article;

ALTER TABLE article MODIFY COLUMN created_at DATETIME NOT NULL;
ALTER TABLE article MODIFY COLUMN title VARCHAR(100) NOT NULL;
ALTER TABLE article MODIFY COLUMN `contents` TEXT NOT NULL;
```

## 2. 다음의 요구사항을 충족하는 SQL문을 작성하여 주시기 바랍니다.
```sql
select
    st.sort as "종류",
    ct.name as "지역_이름",
    (sc.fee + sct.fee) as "비용"
from
    sort_table st
left join
    special_charge_table sct on st.is_rush = sct.is_rush
left join
    culture_table ct on ct.region = "B"
left join
    charge_table cht on cht.region = ct.region
where
        st.sort = '의약품'
    and
        ct.name = 'b-1'
;
```

또는

```sql
select
    (select st.sort from sort_table st where st.sort = '의약품') as "종류",
    c.name as "지역_이름",
    (
        (select sct.fee
         from special_charge_table sct
             left join sort_table s on sct.is_rush = s.is_rush
         where s.sort = '의약품')
        +
        (select ct.fee 
         from charge_table ct 
             left join culture_table t on ct.region = t.region 
         where t.region = 'B')
    ) as "비용"
from
    culture_table c
where
    c.region = 'B'
;
```

## 3. 다음 요구사항을 만족하는 Java 코드를 작성해주세요.
```java
public class Tests {

    @Test
    @DisplayName("level test 3")
    void a3() throws Exception {

        Aligator aligator = new Aligator();
        Human human = new Human();

        aligator.rest();
        human.rest();

        Shelter shelter = new Shelter();
        shelter.support(aligator);

        Animal target = shelter.getObj();
        System.out.println(target);

        shelter.support(human);

        target = shelter.getObj();
        System.out.println(target);

    }

    abstract class Animal {

        public String name;

        public Animal(String name) {
            this.name = name;
        }

        public abstract void rest();

        @Override
        public String toString() {
            return name + "!";
        }

    }

    class Aligator extends Animal {

        public Aligator() {
            super("악어");
        }

        @Override
        public void rest() {
            System.out.println("악어가 누워서 휴식을 취합니다.");
        }

    }
    class Human extends Animal {

        public Human() {
            super("사람");
        }

        @Override
        public void rest() {
            System.out.println("사람이 누워서 휴식을 취합니다.");
        }

    }

    class Shelter {

        Animal obj;

        public void support(Animal animal) {
            if (this.obj != null && !animal.equals(this.obj)) {
                System.out.println(this.obj.name + "은(는) 물러났습니다.");
            }
            this.obj = animal;
            System.out.println(animal.name + "이(가) 휴식처에서 휴식을 취하고 있습니다.");
        }

        public Animal getObj() {
            return obj;
        }

    }

}
```

## 4. 다음의 요구사항을 만족하는 Java 코드를 작성해주세요.
```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine());
StringBuilder sb = new StringBuilder();
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i; j++) {
        sb.append("*");
    }
    for (int j = 1; j <= 2*n-2*i; j++) {
        sb.append(" ");
    }
    for (int j = 1; j <= i; j++) {
        sb.append("*");
    }
    sb.append("\n");
}
for (int i = n-1; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        sb.append("*");
    }
    for (int j = 1; j <= 2*n-2*i; j++) {
        sb.append(" ");
    }
    for (int j = 1; j <= i; j++) {
        sb.append("*");
    }
    sb.append("\n");
}
System.out.print(sb);
```

```java
public static void main(String[] args) {
    int n = 5;
    StringBuilder sb = new StringBuilder();

    for (int i = 1; i <= n; i++) {
        appendLine(sb, i, 2 * n - 2 * i);
    }
    for (int i = n - 1; i >= 1; i--) {
        appendLine(sb, i, 2 * n - 2 * i);
    }

    System.out.print(sb);
}

private static void appendLine(StringBuilder sb, int stars, int spaces) {
    // Append left stars
    for (int j = 1; j <= stars; j++) {
        sb.append("*");
    }
    // Append spaces
    for (int j = 1; j <= spaces; j++) {
        sb.append(" ");
    }
    // Append right stars
    for (int j = 1; j <= stars; j++) {
        sb.append("*");
    }
    sb.append("\n");
}
```

## 5. 다음의 요구사항을 만족하는 Java 코드를 작성해주세요.

```java

public class LevelTests {

    static class CouldNotFindSuchElementException extends RuntimeException {
        public CouldNotFindSuchElementException() {
            super();
        }
        public CouldNotFindSuchElementException(String message) {
            super(message);
        }
        public CouldNotFindSuchElementException(String message, Throwable cause) {
            super(message, cause);
        }
        public CouldNotFindSuchElementException(Throwable cause) {
            super(cause);
        }
    }

    interface Storable<T> {

        T get();
        boolean isPresent();
        boolean isEmpty();

    }

    static class Container<T> implements Storable<T> {

        private final T data;

        private Container(T data) {
            this.data = data;
        }

        public static <T> Container<T> empty() {
            return new Container<>(null);
        }

        public static <T> Container<T> of(T data) {
            return new Container<T>(Objects.requireNonNull(data));
        }

        public static <T> Container<T> ofNullable(T data) {
            return data == null
                    ? new Container<>(null)
                    : new Container<>(data);
        }

        @Override
        public T get() {
            if ( data == null ) {
                throw new CouldNotFindSuchElementException();
            }
            return data;
        }

        @Override
        public boolean isPresent() {
            return data != null;
        }

        @Override
        public boolean isEmpty() {
            return data == null;
        }
    }

}
```
