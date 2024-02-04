# DB 내장함수

데이터베이스 관리 시스템(DBMS)에서 제공하는 내부적으로 구현된 함수로 데이터베이스에서 데이터를 처리하고 분석하는 데 사용된다.

1. 집계 함수: 데이터에서 여러 레코드의 일부 속성을 설명하는 단일 값을 반환하는 함수
  
  - SUM: 주어진 열의 값을 모두 더한 총합을 반환
  - AVG: 주어진 열의 값의 평균을 계산하여 반환
  - COUNT: 주어진 열에서 값이 존재하는 행의 수를 반환
  - MAX: 주어진 열에서 가장 큰 값을 반환
  - MIN: 주어진 열에서 가장 작은 값을 반환
2. 문자열 함수: 문자열을 조작하고 처리하기 위한 함수
  
  - CONCAT: 두 개 이상의 문자열을 결합하여 하나의 문자열로 반환
  - SUBSTRING: 주어진 문자열에서 일부 문자열을 추출하여 반환
  - UPPER: 주어진 문자열을 모두 대문자로 변환하여 반환
  - LOWER: 주어진 문자열을 모두 소문자로 변환하여 반환
3. 날짜 및 시간 함수: 날짜와 시간을 다루는 함수
  
  - DATE: 날짜와 시간 정보를 포함하는 데이터 형식
  - TIME: 시간 정보를 포함하는 데이터 형식
  - YEAR: 주어진 날짜나 시간에서 년도를 추출하여 반환
  - MONTH: 주어진 날짜나 시간에서 월을 추출하여 반환
  - DAY: 주어진 날짜나 시간에서 일을 추출하여 반환
4. 변환 함수: 데이터 형식을 변환하기 위한 함수
  
  - CAST: 데이터의 형식을 다른 형식으로 변환
  - CONVERT: 데이터의 형식을 다른 형식으로 변환
  - TO_CHAR: 주어진 데이터를 문자열로 변환하여 반환
5. 조건 함수: 조건을 평가하고 기반으로 결과를 반환하는 함수
  
  - IF: 조건식이 참인 경우에는 특정 값을, 그렇지 않은 경우에는 다른 값을 반환
  - CASE: 여러 조건을 평가하고, 해당하는 조건에 따라 결과 값을 반환
  - COALESCE: 주어진 값들 중에서 NULL이 아닌 첫 번째 값을 반환

# 프로시저

데이터베이스에서 실행 가능한 절차적인 코드 블록이다. 프로시저는 일련의 SQL 문과 제어 구문으로 구성되어 있으며, 데이터베이스 내에서 재사용 가능한 로직을 구현하는 데 사용된다. 주로 데이터베이스의 데이터를 처리하고 조작하는 작업을 수행하는 데에 활용된다.

## 장점

- 하나의 요청으로 여러 SQL문을 실행시킬 수 있다. 
  
- 네트워크 소요 시간을 줄여 성능을 개선할 수 있다.
  
- 여러 어플리케이션과 공유가 가능하다. (API처럼 제공가능)
  
- 기능 변경이 편하다. (특정 기능을 변경할 때 프로시저만 변경하면 됨)
  

## 단점

- 문자나 숫자열 연산에 사용하면 java보다 느린 성능을 보일 수 있다.
- 프로시저가 앱의 어디에 사용되는 확인이 어렵다 → 유지보수가 어려움

## 프로시저 예제

```plsql
CREATE OR REPLACE PROCEDURE InsertEmployeeInsertEmployee (
    employeeId IN NUMBER,
    firstName IN VARCHAR2,
    lastName IN VARCHAR2,
    success OUT VARCHAR2,
    error OUT VARCHAR2
)
IS
    localVariable VARCHAR2(100);
BEGIN
    BEGIN
        INSERT INTO Employees (EmployeeId, FirstName, LastName)
        VALUES (employeeId, firstName, lastName);

        success := '직원이 성공적으로 추가되었습니다.';
        error := NULL;
        localVariable := '로컬 변수 값';
    EXCEPTION
        WHEN OTHERS THEN
            success := NULL;
            error := '오류가 발생했습니다: ' || SQLERRM;
            localVariable := NULL;
    END;

    DBMS_OUTPUT.PUT_LINE('로컬 변수 값: ' || localVariable);
END;
/
```

- CREATE : 구문 생성
  
- OR REPLACE : 같은 프로시저가 있을 때, 기존 프로시저를 무시하고 새로운 내용으로 덮어쓰기
  
- MODE : 매개변수의 역할을 결정
  
  - IN : 입력 매개변수
    
  - OUT : 출력 매개변수
    
  - INOUT : 입출력 매개변수
    
- IS : PL/SQL 블록을 시작하고 BEGIN 뒤에 나올 SQL문에서 사용할 변수를 선언
  
- BEGIN : PL/SQL 블록의 시작
  
- EXCEPTION : SQL문 실행 도중 발생한 에러를 처리
  
- END : PL/SQL 블록의 끝
  

## 프로시저 실행 예제

```plsql
EXECUTE InsertEmployeeInsertEmployee insert(1, "길동", "홍");
```

# PL/SQL(Procedure Language)

Oracle 데이터베이스에서 사용되는 절차적인 프로그래밍 언어로, 프로시저를 작성하고 실행하기 위해 사용된다. 프로시저, 함수, 트리거 등을 작성할 수 있도록 지원한다.

## PL/SQL 특징

1. 커서 : PL/SQL은 커서라는 개념을 사용하여 데이터베이스 결과 집합을 처리할 수 있다. 커서를 사용하여 SQL 문의 실행 결과를 반복하거나, 특정 레코드에 접근할 수 있다. 이를 통해 데이터의 순회 및 조작이 가능하다.
  
2. 트리거 : PL/SQL은 데이터베이스 트리거를 작성할 수 있는 기능을 제공한다. 트리거는 데이터베이스의 특정 이벤트가 발생했을 때 자동으로 실행되는 코드 블록으로, 데이터의 일관성 유지, 제약 조건 검사, 로깅 등 다양한 용도로 사용된다.
  

# 커서

특정 SQL 문장을 처리한 결과를 담고있는 영역을 가리키는 일종의 포인터로, 커서를 사용하면 처리된 SQL 문장의 결과 집합에 접든할 수 있다.

## 커서의 종류

### 1. 묵시적(암시적) 커서(Implicit Cursor)

오라클에서 자동적으로 선언해주는 SQL 커서

#### 1-1. 묵시적 커서 속성

SQL%FOUND - SQL 실행 시 데이터가 1건 이상 존재할 경우 True 반환

SQL%NOTFOUND - SQL 실행 시 데이터가 없을 경우 True 반환

SQL%ROWCOUNT - SQL 실행 시 영향받은 Row의 수, 없으면 0 반환

SQL%ISOPEN - 묵시적 커서 사용 시에는 항상 FALSE를 반환(이 속성으로 참조할 때는 이미 해당 묵시적 커서는 닫힌 상태 이후이기 때문)

#### 1-2. 묵시적 커서 예제

```plsql
DECLARE
  emp_name employees.last_name%TYPE;
  emp_salary employees.salary%TYPE;
BEGIN
  -- employees 테이블에서 salary가 5000 이상인 모든 레코드를 조회
  FOR emp_record IN (SELECT last_name, salary FROM employees WHERE salary >= 5000) 

  LOOP
    -- 조회된 데이터를 변수에 저장
    emp_name := emp_record.last_name;
    emp_salary := emp_record.salary;

    -- 변수 값을 출력
    DBMS_OUTPUT.PUT_LINE('Employee Name: ' || emp_name || ', Salary: ' || emp_salary);
  END LOOP;
END;
/
```

위 예제에서는 `employees` 테이블에서 `salary`가 5000 이상인 레코드를 조회하고, 조회된 데이터를 묵시적 커서인 `emp_record`에 저장한다. 그리고 `emp_record`의 각 레코드를 순회하면서 `emp_name`과 `emp_salary` 변수에 데이터를 저장하고 출력한다.

묵시적 커서는 `FOR...IN` 문을 사용하여 반복문을 실행하면서 데이터를 처리하는 편리한 방법이다. 커서를 명시적으로 선언하지 않고 사용할 수 있어 코드의 가독성을 향상시키고, 간단한 쿼리 결과를 처리할 때 유용하다.

### 2. 명시적 커서(Explicit Cursor)

사용자가 선언하는 커서

#### 2-1. 명시적 커서 속성

CURSOR%NOTFOUND - 커서 내 더 이상 데이터가 없을 경우 True 반환

CURSOR%FOUND - 데이터가 존재할 경우 True 반환

CURSOR%ROWCOUNT - 커서 실행 직후의 Rowcount로 Open 전에는 0을 반환

CURSOR%ISOPEN - 커서 오픈 여부를 확인하여 Open 되어 있으면 True 반환

#### 2-2. 명시적 커서 예제

```plsql
DECLARE
  CURSOR c_employee IS
    SELECT last_name, salary FROM employees WHERE salary >= 5000;
  v_employee_name employees.last_name%TYPE;
  v_employee_salary employees.salary%TYPE;
BEGIN
  OPEN c_employee; -- 커서 열기

  LOOP
    FETCH c_employee INTO v_employee_name, v_employee_salary; -- 데이터 가져오기
    EXIT WHEN c_employee%NOTFOUND; -- 더 이상 데이터가 없으면 종료
    
    -- 데이터 출력
    DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_employee_name || ', Salary: ' || v_employee_salary);
  END LOOP;

  CLOSE c_employee; -- 커서 닫기
END;
/
```

명시적으로 커서를 정의하고(CURSOR c_employee), 커서를 열고(OPEN c_employee), 루프를 사용하여 데이터를 가져오고(FETCH), 데이터를 출력한 후에는 커서를 닫는다(CLOSE c_employee).

커서를 열고 FETCH 문을 사용하여 데이터를 가져오는 동안, 루프는 조회된 모든 레코드를 반복하여 처리한다. EXIT WHEN 문은 더 이상 데이터가 없을 때 루프를 종료한다.

> 주의할점
> 
> 커서를 사용할 때는 반드시 먼저 커서를 열고 사용이 끝나면 닫아야 한다.
> 
> 이것은 메모리상에 존재하는 커서의 쿼리 결과를 소멸시키는 것을 의미한다.

# 트리거

DB 시스템에서 삽입, 갱신, 삭제 등 이벤트가 발생할 때마다 자동 수행되는 절차형 SQL이다. 무결성 유지, 로그 메시지 출력 등의 목적으로 사용한다. 구문에는 DCL을 사용할 수 없고 DCL이 포함된 프로시저나 함수 호출도 불가능하다.

## 트리거를 사용하는 이유

쇼핑몰에 어떤 회원이 있다고 가정해보자. 회원탈퇴를 한다면 회원 테이블에서 해당 회원을 delete하면 된다. 하지만 나중에 회원에서 탈퇴한 사람의 정보를 알 수 없다. 그래서 따로 탈퇴 회원 테이블을 만들 수 있는데 까먹고 넣지 않는다면 어떤 회원은 탈퇴 회원 테이블에 존재하고 어떤 회원은 존재하지 않게 된다. 이것을 막기 위헤 누군가가 탈퇴한다면 자동으로 탈퇴 회원 테이블에 추가를 하는 역할을 해주는 것, 이것이 트리거의 역할이다.

## 트리거의 장점

- 데이터 무결성의 강화 (참조 무결성)
- 트리거를 사용하면 트랜잭션에 의해 자동으로 다른 명령을 일으킴으로써 업무처리를 자동화
- 중간에 사용자가 개입하지 않고 구현된 규칙대로 알아서 실행

## 트리거의 단점

- 트리거를 과도하게 사용한다면 복잡한 상호 의존성을 야기
  - 예를 들어 하나의 트리거가 활성화되어 이 트리거 내의 SQL문이 수행되고, 그 결과로 인하여 다른 트리거가 활성화되어 그 트리거의 SQL문이 수행될 수 있음( 트리거의 연쇄 )

## 프로시저 vs 트리거

<img width="649" alt="스크린샷 2024-01-30 오후 6 14 18" src="https://github.com/NaKyongRyul/BaekjoonHub/assets/67616146/112647da-307e-4cfe-9921-e8ef14167c32">


## 트리거 예제

```plsql
CREATE TRIGGER myTrigger -- 트리거 이름 
    AFTER DELETE -- 삭제 후에 작동하도록 지정 
    ON trigger_table -- 트리거를 부착할 테이블 
    FOR EACH ROW -- 각 행마다 적용시킴(신경쓰지말고 예약어로 꼭 쓰기)
BEGIN
    SET @msg = "가수 그룹이 삭제됨";
END $$
DELIMITER;


DELETE FROM trigger_table WHERE id = 1;
SELECT @msg; -- "가수 그룹이 삭제됨" 출 
```

면접 질문

1. 트리거란?
  
  - 트리거는 특정 테이블에 대한 이벤트에 반응해 INSERT, DELETE, UPDATE 같은 DML 문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 작성된 프로그램입니다.
  - 사용자가 직접 호출하는 것이 아닌, 데이터베이스에서 자동적으로 호출한다는 것이 가장 큰 특징입니다.
