---

---

[TOC]

### create table~ 조건이 들어감. 초기치 주는 조건. check 조건. 중복 안되게.

```SQL
1. CHECK : 특정 칼럼의 입력자료에 대해 값 검사.
2. UNIQUE : 동일 값 입력 불허.
3. DEFAULT : 초기값 부여하기. 따로 설정 안하면 DEFAULT 값이 자동으로 들어감.

CREATE TABLE AA (
	BUN NUMBER UNIQUE,
  IRUM CHAR(10),
  ADDR VARCHAR2(30) DEFAULT '강남구 역삼동'
);
```



### select. 조건 주는법. 범위. where~~. 3천이상5천이하 급여 뭐이런것들.

```SQL
SELECT JIKWON_PAY,
				JIKWON_NAME
				FROM JIKWON
				WHERE JIKWON_PAY >= 3000
				AND		JIKWON_PAY <= 5000;
        
AND =
IN = 
<> =
BETWEEN A AND B =
LIKE =
IS NULL, IS NOT NULL = 
```



### transaction. rollback 과 commit의 범위.

```sql
SAVEPOINT point_name;   -- 세이브 포인트 지정.

ROLLBACK TO SAVEPOINT point_name; -- 실행할 시, 해당 지점까지 처리한 작업이 취소됨.

```



### primary key 의 특성을 적으시오.

```SQL
1. 값이 중복되지 않음.
2. 반드시 값을 입력해야 함.
3. 테이블 데이터 고유의 인식번호.
```



### 정규화에 적으시오.

```SQL
1. (함수 종속성)을 이용하여 릴레이션을 (연관성이 있는 속성)들로만 구성하여 (이상 현상)이 발생하지 않도록 하는것.

2. 1정규형, 2정규형, 3정규형, BNCF형, 4정규형, 5정규형.
```



### 2013년 이전에 입사한 사원 중 연도별 직원수를 출력하시오.

```SQL
SELECT TO_CHAR(JIKWON_IBSAIL, 'YYYY') AS 입사년도,
				COUNT(*)	AS 직원수
FROM JIKWON
WHERE JIKWON_IBSAIL < '2014-01-01'
GROUP BY TO_CHAR(JIKWON_IBSAIL, 'YYYY');
```



### select 를 이용하여 create table 하는법.

```SQL
SELECT TABLE table_name_1
AS
SELECT * FROM table_name_2;
```



### join의 종류중 어떤걸 써야 하는지.

```SQL
INNER JOIN = 서로 연관되어 있는것만 가져옴,
LEFT OUTER JOIN,
RIGHT OUTER JOIN,
FULL OUTER JOIN,
FULL JOIN,
SELF JOIN
```



### 부서별 급여의 합 출력. join이 들어감. oracle 고유방법과 표준sql방법 2개 써야됨.

```SQL
-- 1. 표준 방법
SELECT BUSER_NAME 			AS 부서명,
				SUM(JIKWON_PAY) AS 급여합
FROM BUSER LEFT OUTER JOIN JIKWON
ON	BUSER_NO = BUSER_NUM
GROUP BY BUSER_NAME;

-- 2. oracle 방법
SELECT BUSER_NAME 			AS 부서명,
				SUM(JIKWON_PAY) AS 급여합
FROM BUSER, JIKWON WHERE BUSER_NO(+) = BUSER_NUM
GROUP BY BUSER_NAME;
```



### subquery. 한국인 직원과 직급이 같은 직원자료를 출력하시오.

```SQL
SELECT JIKWON_NAME,
				JIKWON_JIK
				FROM JIKWON
				WHERE JIKWON_JIK = ( SELECT JIKWON_JIK
                           			FROM JIKWON
                           			WHERE JIKWON_JIK = '한국인');
```

