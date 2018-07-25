---

---



```java

```



- [ ] file transfer





`substr(column, ~에서부터, ~몇째까지)`

`substr(jikwon_name, 2, 3) 직원이름의 2번째부터3번째까지 뽑아냄`

`substr(jikwon_name, '이')`



**case when.**

```sql
case 표현식 
	when 결과1 then
				처리문1;
  when 결과2 then
				처리문2;
	...
	else
			기타 처리문;
end case;
```

```sql
case when 표현식1 then
			처리문1;
		when 표현식2 then
			처리문2;
		...
		else
			기타 처리문;
end case;
```







-- 형변환, 공통변환함수
`to_date(), to_number(), to_char()`

-- 기타함수

`rank() over`

`nvl`

`nullif`

`case funtion`

`decode`



1. null 에 값 넣기.

   ```sql
   nvl(column, '임시직')
   ```

2. 입사일 기준으로 근무년수 구하는거.(년도별!!)

   ```sql
   to_char(sysdate,'YYYY') - to_char(column_ibsail, 'YYYY')
   ```

   



함수에 여러가지 쓰는거.

sum함수 쓰는거. 

xx와 xx사이.

where절.

부장과 과장만~ where jikwon_jik IN ('부장','과장')

sum 예시 https://devdoggo.netlify.com/post/sql/sql13/

group by 도 언제쓰는지 알아야됨.

group by rollup(buser_num, jikwon_jik)  -- rollup 은 마지막에 합을 구함. 10번부서의 합, 20번 부서의 합.. < 부서별 소계 구하기>

where절에 뒤에붙이는 함수에 순서가 있는가?

mindmap https://www.google.co.kr/search?q=Mindjet+MindManager+crack&source=lnms&tbm=isch&sa=X&ved=0ahUKEwiOltLSrrTcAhVJOJQKHfnNAxYQ_AUICygC&biw=944&bih=947#imgrc=_

select extract 년도, 달 뽑아내는 함수.

- having, having count().

- inner,outer,full join terms.

  `inner join table_name`

- in 연산자 (https://zetawiki.com/wiki/SQL_IN_%EC%97%B0%EC%82%B0%EC%9E%90)





**sql로 주민번호로 나이 뽑아내기**

---

07-24

- union. union all.

- sub query

1. 



07-25

1. view.

   ```sql
   create or replace view [view_name] as
   select column_1, column_2, column_3
   from [table_name]
   
   create view [view_name] as
   select column_1, column_2, column_3
   from	[table_name]
   
   -- view text보기
   select view_name, text
   from user_views;
   
   
   ```

   





```sql
-- 문1)총무부에서 관리하는 고객수 출력(고객 30살 이상만 작업에 참여) 
SELECT To_char(SYSDATE, 'YY') + 100 - 86 
  FROM dual; 

SELECT To_char(SYSDATE, 'YY') + 100 - ( Substr(gogek_jumin, 1, 2) ) AS result 
  FROM gogek; 

SELECT buser_name AS 부서명, 
       Count(*)   AS 고객수 
  FROM jikwon, 
       buser, 
       gogek 
 WHERE buser_num = buser_no 
       AND jikwon_no = gogek_damsano 
       AND To_char(SYSDATE, 'YY') + 100 - ( Substr(gogek_jumin, 1, 2) ) >= 30 
       AND buser_name = '관리부' 
 GROUP BY buser_name; 

SELECT buser_name AS 부서명, 
       Count(*)   AS 고객수 
  FROM jikwon 
       left outer join buser 
                    ON buser_num = buser_no 
       left outer join gogek 
                    ON jikwon_no = gogek_damsano 
 WHERE To_char(SYSDATE, 'YY') + 100 - ( Substr(gogek_jumin, 1, 2) ) >= 30 
       AND buser_name = '총무부' 
 GROUP BY buser_name; 

SELECT Extract(year FROM SYSDATE) 
  FROM dual; 

SELECT buser_name AS 부서명, 
       Count(*)   AS 고객수 
  FROM jikwon 
       left outer join buser 
                    ON buser_num = buser_no 
       left outer join gogek 
                    ON jikwon_no = gogek_damsano 
 WHERE Extract(year FROM SYSDATE) - ( Decode(Substr(gogek_jumin, 8, 1), '1', 
                                      '19', 
                                                                        '2', 
                                      '19', 
                                                                        '20') 
                                      || Substr(gogek_jumin, 1, 2) ) + 1 >= 30 
 GROUP BY buser_name 
HAVING buser_name = '총무부'; 


-- 문4. 부서와 직원명을 입력하면 관리고객 자료 출력
-- ~ where buser_name ='영업부' and jikwon_name='이순신'
SELECT jikwon_name AS 직원명, 
       buser_name  AS 부서명, 
       gogek_name  AS 고객명, 
       gogek_tel   AS 고객번호, 
       gogek_jumin AS 고객주민번호 
  FROM jikwon 
       inner join gogek 
               ON jikwon_no = gogek_damsano 
       left outer join buser 
                    ON buser_num = buser_no 
 WHERE buser_name = '영업부' 
       AND jikwon_name = '이순신'; 

-- 문3. 고객이 담당직원의 자료를 보고 싶을 때, 고객명을 입력하면 담당직원 자료 출력.
SELECT gogek_name  AS 고객명, 
       jikwon_name AS 직원명, 
       buser_name  AS 부서명, 
       buser_tel   AS 부서번호, 
       jikwon_gen  AS 직원성별 
  FROM jikwon 
       inner join gogek 
               ON jikwon_no = gogek_damsano 
       left outer join buser 
                    ON buser_num = buser_no 
 WHERE gogek_name = '이가은'; 
 

```



- 계정.

```sql
-- 	create user 계정명 identified by 비밀번호
--	drop user 계정명 [cascade]
--	alter user 계정명 identified by 비밀번호
```



`create user ID identified by PASS` id 와 pass 만들기

`grant connect to kbs;` kbs에게 계정 권한 부여.(read only)

`grant resource to kbs;` kbs에게 권한 부여 (read,write)

`grant connent,resource to kbs;`

`grant all on Table_name to Account_name;` 모든권한 한번에 주기.

` alter user kbs default tablespace users quota unlimited on users;` 테이블 권한주기.

`grant select on Table_name to Account_name;`

`revoke select on Table_name from Account_name;` 권한 취소.

`revoke all on Table_name from Account_name;` 모든권한 빼기

