# 1. SQL(DB 언어)

DB에서 원하는 데이터를 추출하고 분석하는데 도움을 주는 쿼리 언어

## 1-1. SQL을 사용하는 이유

SQL을 사용하기 전, 데이터 분석은 엑셀을 사용하거나 수작업으로 진행되었다. 이것은 시간도 많이 소요되고 데이터무결성 문제도 있었다. 그래서 DB에 저장된 데이터를 효율적으로 추출하고 분석하기 위해 SQL을 사용하고 있고 빅데이터를 다루기 위한 필수 언어로 자리잡았다.

## 1-2. 대표적인 관리 시스템(RDBMS)

1.   Oracle
  
  - 대규모 기업용 데이터베이스 시스템
    
  - 유닉스/리눅스 환경에서 가장 많이 사용되는 RDBMS
    
  - 안정성과 확장성이 높음
    
2. MySQL
  
  - 오픈 소스 기반의 관계형 데이터베이스 관리 시스템
    
  - 빠른 속도와 높은 성능을 지원
    
  - 가벼운 설치와 사용이 가능하며, 웹 애플리케이션과 소규모 비즈니스에 많이 사용됨
    
3. MY SQL(Microsoft SQL Server)
  
  - Microsoft가 개발한 관계형 데이터베이스 관리 시스템
    
  - Windows 운영 체제에 친화적인 시스템
    
  - 편리한 관리 도구와 호환성이 높은 특징으로 기업용 솔루션으로 많이 사용됨
    

# 2. SQL Injection

악의적인 사용자가 보안상의 취약점을 이용하여 임의의 SQL문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위이다. 공격이 비교적 쉽지만 큰 피해를 입힐 수 있는 공격이다.

## 2-1. 진행 시나리오

<img width="763" alt="스크린샷 2024-01-30 오후 6 33 09" src="https://github.com/NaKyongRyul/BaekjoonHub/assets/67616146/ade9a724-c4c2-4521-8faf-7b135be38630">

클라이언트(회원)들이 자격증 번호를 조회할 수 있는 시스템이 있다. SQL 진행은 anjinma라는 클라이언트가 '자격증 번호 조회'를 클릭하여 anjinma라는 이름이 웹 서버에 들어가고 DB에 입력한 값이 있는지 확인 후 존재한다면 자격증 DB를 출력해준다. 여기서 이름이 blackhat이라는 클라이언트가 자신의 blackhat을 조회해야 하는데 SQL 구문을 변경하여 anjinma라는 클라이언트의 자격증 번호를 조회한다.

예를 들어서 '자격증 번호 조회'를 클릭하면 url이 `http://license.com/mylicense?=anjinma`가 된다고 가정하자. 그럼 공격자의 조회는 `http://license.com/mylicense?=blackhat` 이렇게 된다. 여기서 공격자는 뒤에 blackhat을 anjinma로 변경해야 하는데 그냥 변경으로는 현재 로그인된 자신과는 다르기 때문에 웹서버에서 인정하지 않는다. 그러므로 특정 쿼리문을 넣어준다. anjinma or 1=1 이렇게 넣게 되면 구문 1과 1은 같다는 참이므로 or 진행으로 해당 구문은 참이되어 결과를 출력해준다.

## 2-2. 종류

### 2-2-1. Error based SQL Injection

논리적 에러를 이용한 SQL 인젝션

### 예시

올바른 로그인 SQL

```sql
SELECT * FROM client WHERE id='anjinma' and password='1111'; -- 올바른 로그인sql
```

SQL 인젝션

```sql
SELECT * FROM client WHERE id='anjinma' --' and password='입력한 password'; -- sql 인젝션
SELECT * FROM client WHERE id='입력한 id' OR 1=1 --' and password='1111'; -- 올바른 로그인
```

첫번째 경우는 user의 id를 아는 경우이다.

select * from client where id = 'anjoinma'' -> 여기서 sql syntax error 발생

'는 sql 문법의 일부이기 때문에 이런 문법 에러가 발생한다. 그리고 --는 sql에서 주석을 의미한다.

그래서 id를 입력하는 곳에 anjoinma' -- 라고 입력하면 id는 제대로 들어가고 뒤에 비밀번호를 받는 조건이 주석처리되기 때문에 로그인이 가능하다.

두번째 경우는 user의 id, password를 모두 모르는 경우이다.

id를 입력하는 곳에 아무거나' or 1=1 -- 라고 입력하면 뒤에 'or 1=1'이 성립되면서 DB테이블에서 가장 위에 있는 계정으로 로그인된다. 보통의 DB 테이블은 admin 계정이 가장 위에 있을 확률이 높기 때문에 admin 계정이 해킹당할 수 있다.

### 2-2-2. UNION based SQL Injection

UNION 명령어를 이용한 SQL Injection

### 예시

```sql
SELECT * FROM artists WHERE artist = -1 
UNION SELECT 1, uname, pwd FROM users 
WHERE uname='test';


SELECT * FROM users WHERE id = 'test' UNION SELECT 1,1 --' and password='hello'
```

첫번째 경우는 해당 사이트에서  `http://artistcom/artists=1~n` 과 같은 경로로 어떤 작가의 정보를 가져다주는 페이지가 있다고 하자.

Union(All)은 여러 개의 SQL문을 합쳐 하나의 SQL문으로 만들어주는 방법이다. Union으로 합쳐지는 두 테이블은 컬럼 개수가 일치해야 오류가 나지 않는다. 그래서 order by를 사용해서 오류를 통해 컬럼의 개수를 파악한다.

url에 `http://artistcom/artists=-1 UNION SELECT 1, uname, pwd FROM users WHERE uname='test'` 이렇게 입력한다면 union 전의 쿼리는 성립하지 않고 뒤에 쿼리만 성립하므로 uname, pwd를 뽑을 수 있다.

두번째 경우는 id를 입력하는 곳에 test' union select 1,1라고 입력하면 users 테이블의 모든 정보가 출력된다.

### 2-2-3. Blind SQL Injection

공격자가 DB의 데이터를 직접 조회하지 않고, 참/거짓의 결과를 통해 정보를 추출하는 방법

## 2-3. SQL Injection 예방

### 2-3-1. PreparedStatement(파라미터 바인딩)

<img width="726" alt="스크린샷 2024-01-30 오후 9 24 59" src="https://github.com/NaKyongRyul/BaekjoonHub/assets/67616146/57491dea-deb2-47b5-a3e5-896139c8d31a">
기존의 코드가 이랬다면 sql 구문에 대한 검증이나 예외처리가 없다.

<img width="718" alt="스크린샷 2024-01-30 오후 9 26 21" src="https://github.com/NaKyongRyul/BaekjoonHub/assets/67616146/864c6207-aacf-4425-8e3b-4fa5e4d10ec5">
이렇게 setString()을 사용해서 데이터를 넣으면 결과가 다르다.

```sql
select * from user where id='user1' and pw='zz'' or ''1''=''1' -- 1번
select * from user where id='user1''; drop table user#' and pw='zz'' or ''1''=''1' -- 2번
```

`'`가 하나 더 붙어버리면서 or연산자나 # 주석처리나 모두 방어해버린다. 결국 PreparedStatement의 `setString()`을 통해서 검증을 함으로써 파라메터 바인딩이 된 것이다.

### 2-3-2. SQL 서버 오류 발생 시, 해당하는 에러 메시지 감추기

```sql
-- 원본 테이블 예시: Users
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(100),
    UserEmail VARCHAR(100)
);

-- 뷰 생성
CREATE VIEW PublicUsers AS
SELECT UserName, UserEmail
FROM Users;

-- 사용자는 이 뷰를 통해서만 데이터를 조회
SELECT * FROM PublicUsers;
```

view를 사용해서 원본 DB 테이블의 접근 권한을 높인다. 일반 사용자는 view로만 접근하여 에러를 볼 수 없도록 만든다.

### 2-3-3. 입력값에 대한 검증

검증 로직을 추가하여 미리 설정한 특수문자들이 들어왔을 때 요청을 막아낸다.

## 면접질문

1. sql injection 개념과 대응 방법
  
2. Union All과 Union의 차이
  
  - Union All - 테이블간의 중복값까지 모두 합쳐서 출력
    
  - Union - 테이블간의 중복값은 제거하고 출력
