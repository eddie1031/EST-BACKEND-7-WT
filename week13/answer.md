# 13주차 정리 정답

**1-12. 다음의 상황을 확인하여 올바르게 동작하도록 명령어를 작성하여 주십시오.**  
- 상황
```text
- Spring Boot 기반 동적 웹 애플리케이션에서 `/api/hello`로 Fetch API를 통하여 요청을 보내고자 합니다.
- Spring Boot Application은 8080 포트에서 실행되고 있습니다.
- `/api/hello`에서는 JSON이 아닌 "문자열"응답을 내려주고 있습니다.
- 응답받은 문자열을 브라우저의 콘솔에 한번 출력 후 HTML 문서에 출력하고자 합니다.
- 오류가 있다면 오류를 콘솔에 출력 후, '에러!'라는 문자열을 경고(alert)으로 알리고자 합니다.
- 인증은 필요 없습니다.
```

- 문제  
static.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1 id="title"></h1>
</body>
</html>
```

api.js
```javascript
fetch((1))
        .(2)(
            resp => {
               (12) resp.(3);
            }
        )
        .(4)( data => {
            console.log((5));

            const h1El = (6);
            h1El.(7) = data;

        } )
        .(8)(
            err => {
                (9)
				(10)((11));
            }
        )
```


1. (1)에 들어갈 명령어를 작성해주세요.  
```javascript
'http://localhost:8080/api/hello'
```
2. (2)에 들어갈 명령어를 작성해주세요.  
```javascript
then()
```
3. (3)에 들어갈 명령어를 작성해주세요.  
```javascript
text()
```
4. (4)에 들어갈 명령어를 작성해주세요.  
```javascript
then()
```
5. (5)에 들어갈 명령어를 작성해주세요.  
```javascript
data
```
6. (6)에 들어갈 명령어를 작성해주세요.  
```javascript
document.getElementById('title');
```
7. (7)에 들어갈 명령어를 작성해주세요.  
```javascript
innerText
```
8. (8)에 들어갈 명령어를 작성해주세요.  
```javascript
catch()
```
9. (9)에 들어갈 명령어를 작성해주세요.  
```javascript
console.log(err);
```
10. (10)에 들어갈 명령어를 작성해주세요.  
```javascript
alert()
```
11. (11)에 들어갈 명령어를 작성해주세요.  
```javascript
'에러!'
```
12. (12)에 들어갈 명령어를 작성해주세요.  
```javascript
return
```

**13-15. 다음 빈칸에 알맞은 단어를 작성해주세요.**  
13. (데이터 조작 언어 || DML)은 관계형 데이터베이스 관리 시스템에서 데이터를 조작하는데 사용되는 명령어 집합입니다. 이것의 주된 목적은 데이터베이스 내의 데이터를 삽입, 수정, 삭제, 조회하는 것입니다.  
14. (데이터 제어 언어 || DCL)은 데이터베이스에서 데이터의 접근 권한과 보안을 관리하는 명령어 집합입니다. 이것은 데이터베이스 관리자가 특정 사용자나 그룹에 대하여 데이터베이스 객체에 대한 접근 권한을 부여하거나 철회하는데 사용됩니다. 
15. (데이터 정의 언어 || DDL)은 관계형 데이터베이스 관리 시스템에서 데이터이스의 구조를 정의하고 수정하는데 사용되는 명령어 집합입니다. 이것의 주요 목적은 데이터베이스의 객체를 생성, 수정, 삭제하는 것입니다.  
  
