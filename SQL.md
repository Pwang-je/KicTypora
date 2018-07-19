---
Date : 
Languate : SQL Query
---

[TOC]

## Type of SQL



|      | DDL                                         | DML                                           | DCL                                      |
| ---- | ------------------------------------------- | --------------------------------------------- | ---------------------------------------- |
|      | Data Definition Language<br />데이터 정의어 | Data Manipulation Language<br />데이터 조작어 | Data Control Language<br />데이터 제어어 |
|      | CREATE<br />ALTER<br />DROP<br />TRUNCATE   | SELECT<br />INSERT<br />UPDATE<br />DELETE    | GRANT<br />REVOKE                        |



### DDL

> 데이터베이스를 정의하는 언어. 데이터 생성 및 수정, 삭제.
> **DROP**은 테이블 삭제, **DELETE**는 값을 삭제하지만 `COMMIT` 과 `ROLLBACK` 이 가능함. **TRUNCATE**도 삭제는 가능하지만 자동 `COMMIT` 이라서 `ROLLBACK` 불가능.

|            |                                         |
| ---------- | --------------------------------------- |
| `CREATE`   | 데이터베이스, 테이블 등을 생성하는 역할 |
| `ALTER`    | 테이블을 수정하는 역할                  |
| `DROP`     | 데이터베이스, 테이블을 삭제하는 역할    |
| `TRUNCATE` | 테이블을 초기화 시키는 역할             |

* SCHEMA, DOMAIN, TABLE, VIEW, INDEX 를 정의하거나 변경할때 사용함.
* 데이터베이스 관리자나 데이터베이스 설계자가 사용.



### DML

> 데이터 조작어, 정의된 데이터베이스에 입력된 레코드를 **조회**하거나 **수정** 및 **삭제** 하는 역할. 

|          |                        |
| -------- | ---------------------- |
| `SELECT` | 데이터를 조회하는 역할 |
| `INSERT` | 데이터를 삽입하는 역할 |
| `UPDATE` | 데이터를 수정하는 역할 |
| `DELETE` | 데이터를 삭제하는 역할 |

* 데이터베이스 사용자가 조작어를 통해 실질적 데이터를 처리하는데 사용.
* 데이터베이스 사용자와 관리 시스템간의 인터페이스 제공.



### DCL

> 데이터베이스에 접근하거나 객체에 권란을 주는 등의 역할.

|            |                                                              |
| ---------- | ------------------------------------------------------------ |
| `GRANT`    | 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한 부여  |
| `REVOKE`   | 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 박탈 및 회수 |
| `COMMIT`   | 트랜잭션의 작업이 정상적으로 완료됐음을 관리자에게 알림      |
| `ROLLBACK` | 트랜잭션의 작업이 비정상적으로 종료 되었을 때 원래대로 복구  |



## Terms

|                                                              |                                                 |
| ------------------------------------------------------------ | ----------------------------------------------- |
| `CREATE TABLE TABLE_NAME(var PRIMARY KEY, var VARCHAR2(N));` |                                                 |
| `INSERT INTO TABLE_NAME(var1, var2, var3). . .`              |                                                 |
|                                                              |                                                 |
| `DROP TABLE TABLE_NAME;`                                     | 테이블 삭제                                     |
| `DELETE FROM TABLE_NAME var;`                                | 값 삭제. `COMMIT` `ROLLBACK`                    |
| `TRUNCATE TABLE TABLE_NAME`                                  |                                                 |
| `DESC TABLE_NAME`                                            | 테이블 확인                                     |
|                                                              |                                                 |
| `QUIT`                                                       | `QUIT`로 빠질 땐 무조건 `COMMIT`된 상태로 빠짐. |
| `COMMIT`                                                     |                                                 |
| `ROLLBACK`                                                   | 클라이언트에서 작업한 모든 것들이 취소          |
| `UPDATE TABLE_NAME SET (var) = ;`                            | 모든 자료 수정                                  |



## 정규화







## CONSTRAINT 제약조건

> 잘못된 자료의 입력을 막기 위한 제약 조건.

1. 기본키 제약 조건.

   ```MARKDOWN
   중복을 허용하지 않는 칼럼에 대해 PRIMARY KEY 설정.
   중복자료 입력 불가. NOT NULL, INDEX 생성.
   ```

2. 사용자 정의 제약 조건

   ```markdown
   	CHECK, UNIQUE, FOREIGN KEY . . . 
   ```




### NOT NULL

> '필수 입력 사항'을 의미함.

- NOT NULL은 INSERT 시, **데이터 입력시에 누락이 되어서는 안되는 부분**을 의미.
- NOT NULL 값이 기본값이므로, 컬럼2와 3은 동일하다.

```SQL
CREATE TABLE 테이블명
(
	컬럼명1 테이터타입 NOT NULL,
  컬럼명2 데이터타입 NULL,
  컬럼명3 데이터타입
);
```

```SQL
CREATE TABLE buser
(
	buser_no NUMBER(4) PRIMARY KEY,
 	buser_name VARCHAR(10) NOT NULL
);
```



### UNIQUE

> UNIQUE 는 **해당 테이블에 있어서 존재하는 값이 유일**해야 한다.

- PRIMARY KEY 와 비슷하지만 UNIQUE 의 경우 하나의 테이블에 여러개를 정의할 수 있다.
- UNIQUE 의 경우 NULL 값이 허용된다.
- PRIMARY KEY 처럼 바뀌지 않는 다른 값들을 사용하고 싶을때 사용.

```SQL
-- 단일 UNIQUE 조건

CREATE TABLE 테이블명
(
	컬럼명1 데이터타입 UNIQUE,
  컬럼명2 데이터타입
);

-- 복수 UNIQUE 조건

CREATE TABLE 테이블명
(
	컬럼명1 데이터타입 UNIQUE,
  컬럼명2 데이터타입,
  컬럼명3 데이터타입 UNIQUE,
  컬럼명4 데이터타입,
);
```



### PRIMARY KEY

> 기본키는 하나의 테이블에 있는 데이터들을 식별하기 위한 기준으로 인식되는 제약조건이다.

- 한개의 테이블에 하나만 생성 가능하다.
- NOT NULL + UNIQUE 의 2개의 속성을 기본적으로 가진다.

  ### CHECK

```SQL
CREATE TABLE 테이블명
(
	컬럼명1 데이터타입 PRIMARY KEY,
  컬럼명2 데이터타입
);
```

```SQL
CREATE TABLE my_family
(
	code NUMBER(4) PRIMARY KEY,
  gname VARVHAR2(10),
  birth DATE
);
```



### FOREIGN KEY

> 해당 컬럼에 참조하는 테이블로부터 존재하는 값들만 사용한다는 의미의 제약조건이다.

- 여러개의 컬럼에 **중복적으로 적용 가능**하다.
- 부모테이블과 자식테이블로 관계를 맺고 있을 시, **자식테이블이 참조하는 데이터는 부모 테이블에서 삭제가 불가**하다. (자식테이블부터 삭제 후 부모테이블 삭제 가능)

```SQL
CREATE TABLE 테이블명
(
	컬럼명1 데이터타입 REFERENCES 참조할테이블명(참조할테이블명의 칼럼명),
  컬럼명2 데이터타입
);
```

```SQL
CREATE TABLE student 
( 
  std_number NUMBER(4) PRIMARY KEY, 
  std_name   VARCHAR2(30) NOT NULL, 
  sub_name  NUMBER(4) REFERENCES lecture(lec_code), 
  std_grade  NUMBER DEFAULT 1 CHECK ( 1 <= std_grade AND std_grade >= 4) 
); 
```

#### PRIMARY KEY - FOREIGN KEY

- [PRIMARY KEY - FOREIGN KEY EXAMPLE](PRIMARY KEY - FOREIGN KEY.md )

### CHECK

> 조건에 부합하는 데이터만 입력이 가능하도록 하는 제약조건이다.

- 기본연산자나 비교연산자, IN, NOT IN 등등 사용 가능하다.

```SQL
CREATE TABLE 테이블명
(
	컬럼명1 데이터타입 CHECK (조건),
  컬럼명2 데이터타입
);
```

```sql
CREATE TABLE prof
(
	prof_code NUMBER PRIMARY KEY,
  prof_name VARCHAR2(30),
  prof_labo NUMBER CHECK(100 <= prof_labo AND prof_labo <= 500)
);
```



## DDL

### CREATE





### ALTER





### DROP





### TRUNCATE





## DML

### SELECT

> 데이터베이스 안에 있는 데이터를 조회하기 위해서 사용한다.

```SQL
SELECT 컬럼명1, 컬럼명2, ...
FROM 테이블명
WHERE 조건
ORDER BY 컬럼명;
```

```SQL
SELECT select_list [ INTO new_table ]
[ FROM table_source ]	[ WHERE search_condition ]
[ GROUP BY group_by_expression ]
[ HAVING search_condition ]
[ ORDER BY order_expression [ ASC | DESC ] ]
```



- 단독으로는 절대 사용될 수 없다. 필수로 FROM 이 따라오며, 그외 조건(WHERE) 이나 기타 다른 키워드를 사용할 수 있다.



```SQL
SELECT	*
FROM		JIKWON;		-- JIKWON 테이블 조회

SELECT	JIKWON_NO,
				JIKWON_NAME
FROM		JIKWON;		-- JIKWON 테이블의 NO 와 NAME 조회.


SELECT	JIKWON_NO		AS 사번,
				JIKWON_NAME	AS 직원명
FROM		JIKWON;		-- JIKWON_NO 와 NAME 에 별명 부여.

SELECT	JIKWON_NO 	사번,
				JIKWON_NAME 직원명
FROM		JIKWON;		-- 상동


SELECT	JIKWON_NO
				|| JIKWON_NAME
FROM		JIKWON;		-- 연결연산자 사용 가능.

SELECT	JIKWON_NO
				|| JIKWON_NAME	AS 자료
FROM		JIKWON;		-- 연결연산자 + 별명.

SELECT	10,
				'안녕',
				12 / 3
FROM		DUAL;		-- DUMMY TABLE.

SELECT	JIKWON_NO,
				JIKWON_NAME,
				JIKWON_PAY
FROM		JIKWON;		-- 3개 가능

SELECT	JIKWON_NO,
				JIKWON_NAME,
				JIKWON_PAY
				* 0.012	AS TAX
FROM		JIKWON;		-- 연산 후 불러내기 가능. (PAY*0.012) NO,NAME,TAX 3가지 출력.

SELECT	JIKWON_NAME
				|| '님'
FROM		JIKWON;		-- 문자열도 연산 가능.

```



### INSERT





### UPDATE





### DELETE







### WHERE

```SQL
SELECT * 
FROM   jikwon 
WHERE  jikwon_jik = '대리';		-- 대리만 출력

SELECT * 
FROM   jikwon 
WHERE  jikwon_no = 3;		-- 3번에 해당하는 과장만 출력

SELECT * 
FROM   jikwon 
WHERE  jikwon_ibsail = '2011-03-03';		-- 입사일 11년3월3일인 사람 출력

SELECT * 
FROM   jikwon 
WHERE  jikwon_ibsail = '2011/03/03';		-- 상동

SELECT * 
FROM   jikwon 
WHERE  jikwon_no = 3
				OR jikwon_no = 5;			-- 직원넘버 3번,5번 출력
				
SELECT * 
FROM   jikwon 
WHERE  jikwon_jik = '사원'
				AND jikwon_gen = '여'
				AND jikwon_pay <= 3000;		-- 사원이면서 여자이면서 연봉3천 이하 출력
				
SELECT * 
FROM   jikwon 
WHERE  jikwon_no >= 5
				OR jikwon_no =< 10;			-- 직원넘버 5번에서 10번 사이 출력
				
SELECT *
FROM	 jikwon 
WHERE	 jikwon_ibsail 
				BETWEEN '2001-1-1' 
				AND '2005-12-31';			-- 2001-1-1 에서 2005-12-31 사이 입사한사람 출력
				
SELECT * 
FROM 	 jikwon 
WHERE  jikwon_no < 5 
				OR jikwon_no > 10;		-- 5 미만 10 초과애들만 나옴.
				
SELECT * 
FROM   jikwon 
WHERE  NOT (jikwon_no < 5 OR jikwon_no > 10);		-- 5 미만 10 초과애들.
				
SELECT * 
FROM 	 jikwon 
WHERE  jikwon_no BETWEEN 5 AND 10;		-- 5와 10 사이 직원 출력.				
				
SELECT * 
FROM 	 jikwon 
WHERE  jikwon_gen = '남';		-- 남자만 출력

SELECT * 
FROM 	 jikwon 
WHERE  jikwon_gen <> '남';		-- 여자만 출력

SELECT * 
FROM 	 jikwon 
WHERE  jikwon_name = '홍길동';		-- 홍길동 출력

SELECT * 
FROM 	 jikwon 
WHERE  jikwon_name = '홍';			-- 모든 홍 출력

SELECT * 
FROM 	 jikwon 
WHERE  jikwon_name = '김'
				AND jikwon_name <= '최';		-- 김씨와 최씨 출력
				
SELECT * 
FROM 	 jikwon 
WHERE  jikwon_name = '김' BETWEEN '김' AND '최';		-- 상동
				
SELECT * 
FROM 	 buser 
WHERE  buser_name IN ('총무부','전산부');		-- 총무부,전산부 출력

SELECT * 
FROM 	 jikwon 
WHERE  jikwon_jik IN ('대리','과장','부장');	-- 대리 과장 부장 출력

SELECT * 
FROM 	 jikwon 
WHERE  buser_num IN ('10','30')
				ORDER BY buser_num ASC;	-- 부서넘버가 10과 30인 모든애들 출력
```



