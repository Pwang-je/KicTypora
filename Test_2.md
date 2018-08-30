---

---

[TOC]



### 부서별 근무직원 목록 출력. SELECT문

```sql
SELECT BUSER_NAME, JIKWON_NAME
FROM	JIKWON INNER JOIN BUSER
	ON BUSER_NUM = BUSER_NO
	ORDER BY BUSER_NAME;
```



### 계정잠금 푸는법 과 잠그는 이유

```sql
sqlplus system/oracle

ALTER USER SCOTT ACCOUNT UNLOCK;	-- 잠금해제

트랜잭션 중 데드락을 방지하기 위함임.
```



### 트랜잭션, COMMIT 과 ROLLBACK 왜쓰는지

```SQL
--트랜잭션은 SELECT, INSERT, UPDATE, DELETE 를 쓰기 위해 데이터베이스에 접근하는 것을 의미함. DML.

-- 트랜잭션의 처리 과정을 DB에 저장하기 위해 COMMIT 을 쓴다.

-- 트랜잭션 과정 중 발생한 변경사항을 취소하고 과정을 종료시키며, 이전 COMMIT 한 곳까지 복구시킴.
```



### 테이블 하나 만드시오.(CREATE TABLE~)

```SQL
CREATE TABLE EXAM_1 (
	ENO		VARCHAR2(10),
  ENAME	VARCHAR2(14),
  ELOC	VARCHAR2(10)
);
```



### DELETE 와 TRUNC 의 차이.

```SQL
DELETE는 값을 삭제하지만 COMMIT 과 ROLLBACK 이 가능함. TRUNCATE도 삭제는 가능하지만 자동 COMMIT 이라서 ROLLBACK 불가능.
```



### 계정 만드는법. 권한주는 법까지.

```sql
CREATE USER susan IDENTIFIED BY 123;

GRANT CONNECT, RESOURCE TO SUSAN;
GRANT CREATE SESSION TO SUSAN;
```



### 시노님 만드는법. 2가지 방법의 차이점.

```SQL
ALIAS 임. 객체(TABLE, VIEW, SEQUENCE, PROCEDURE)에 대한 직접적 참조라고 생각하면 됨.

1. PRIVATE SYNONYM = 특정 사용자만 이용할 수 있음
2. PUBLIC SYNONYM = 데이터베이스 안에 있는 모든 사용자가 공유함.

CREATE PUBLIC SYNONYM name FOR object_name;
create public synonym 만들_테이블이름 for 원본_테이블이름. 
```



### 뷰를 만들어서 권한을 주는 방법.

```SQL
-- 뷰를 만들 권한을 줌.
GRANT CREATE VIEW TO SCOTT;

CREATE OR REPLACE VIEW v_v ASㅊ
SELECT JIKWON_NAME
FROM SCOTT.JIKWON;

-- SYSTEM 이 뷰를 만들고 SCOTT 에게 그 뷰를 만질 권한을 줌.
in system,
CREATE OR REPLACE VIEW v_v AS
SELECT JIKWON_NAME
FROM SCOTT.JIKWON;

GRANT SELECT ON VIEW v_v TO SCOTT;
```



### 구조를 확인하는 명령어.

`DESC table_name;`

### CREATE TABLE 하는데 외래키 주는 방법.

```sql
CREATE TABLE DEPT (
	DNO VARCHAR2(10) ,
  DNAME VARCHAR2(14),
  CONSTRAINT PK_DEPT PRIMARY KEY (DNO),
  CONSTRAINT FK_DEPT2 FOREIGN KEY (LNO)
);
```



