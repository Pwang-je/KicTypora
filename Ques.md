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

   

- 계정.
- http://cafe.daum.net/flowlife

```sql
-- 	create user 계정명 identified by 비밀번호
--	drop user 계정명 [cascade]
--	alter user 계정명 identified by 비밀번호

-- grant create synonym to 계정명; synonym 부여
-- grant create public synonym to 계정명; 위에와 같음.
-- create synonym 가상테이블명 for 받아야될 계정명; -- 동의어생성

-- conn USER_ID/USER_PASS		계정 이동.

1. create user USER_ID identified by USER_PASS;
-- 생성
2. grant connect,resource to USER_ID;
-- 권한부여
2-1. grant select on TABLE_NAME to TARGET_ID;
-- select 권한을 target_id 에 부여.
3. drop synonym table_name;
-- 가상 테이블 삭제. 부여한 계정에서만 삭제 가능함.


```



#### 시작부터 다른 테이블에 권한 주기까지.

```sql
-- user SYSTEM.

1. create user USER_ID identified by USER_PASS;	-- 유저 생성.

2. create role ROLE_ID;	-- 롤 생성.

3. grant create session to USER_ID;	-- 세션 권한주기.

4. grant connect, resource to USER_ID;	-- 컨넥션,리소스 권한 주기.

5. grant broadcast to USER_ID;	-- 롤에 유저 권한 주기.

```

```sql
-- user MAIN_USER
6-1. grant select on TABLE_NAME to USER_ID;	-- 유저에게 테이블 권한 주기.
6-2. grant select on TABLE_NAME to ROLE_ID; -- 롤에 권한 주기.

-- 유저에게 권한을 주면 유저가 직접 컨트롤이 됨.
-- 롤에 권한을 줬을 때, revoke 를 롤에 주면 그 롤에 연결된 모든 계정이 쓸수 없음.
```

```sql
-- user USER_ID
7. select * from MAIN_USER.TABLE_NAME;	-- 메인유저 테이블을 조회.
```



### PL_SQL

```sql
- PL/SQL의 프로그램 단위는 블록(Block)

    DECLARE        <== 선택 : 변수와 상수, 프로시저와 함수 서브프로그램, 커서 등을 선언
          선언문
           .....
     -----------------------------------------------
     BEGIN         <== 필수 :  처리할 명령문들을 절차적으로 기술
                                   ▪ 모든 SQL문
          실행문                ▪ 대입문, 반복 처리문, 조건 판단문, 제어 흐름문
          .....                    ▪ 커서 처리문
     -----------------------------------------------
     EXCEPTION   <== 선택 : 오류 처리에 관한 예외처리 명령문을 기술

     
         예외처리문
         .....
    -----------------------------------------------
     END;         <==  필수

     /
```

#### pl/sql 함수

```sql
CREATE OR replace FUNCTION 함수이름 ( 매개변수1, 매개변수2, ...)
RETURN 데이터타입;
IS[AS]
	변수, 상수 등 선언
BEGIN
	실행부
	
	RETURN 반환값;
	[EXCEPTION
  	예외 처리부]
END [함수이름];
/
```

```sql
CREATE OR replace FUNCTION 함수이름
-- CREATE OR replace 구문을 사용하여 함수 생성.
매개변수1, 매개변수2, . . .
-- 함수로 전달되는 매개변수. "매개변수명 데이터타입" 형태로 명시함.
-- Ex. (bno NUMBER) (bname VARCHAR2(10))
```



















```sql
-- parameter type
-- in : 실행환경에서 program 으로 값을 전달.
-- out : program 에서 실행환경으로 값을 전달.
-- inout : 실행환경에서 program 으로 값을 전달하고,
--        다시 program 에서 실행환경으로 처리된 값을 전달.

-- proceduer 정리 실습.

create table person (id number (3), name varchar2(20),
weight number(3));
create sequence seq_id;
insert into person values (seq_id.nextval, '홍길동', 25);
insert into person values (seq_id.nextval, '신길동', 22);
select * from person;

-- insert
--create or replace procedure pro_1(name varchar2, weight number)
create or replace procedure pro_1(name in person.name%type, weight in person.weight%type)
is
begin
  insert into person values(seq_id.nextval, name,weight);
  commit;
exception when others then
  dbms_output.put_line('insert error!');
  rollback;
end;
/

execute pro_1('홍다희',65);
select * from person;

-- update
create or replace procedure pro_2(pid in person.id%type, pname in person.name%type)
is
begin
  update person set name=pname, weight=pweight
  where id=pid;
  commit;
exception when others then
  dbms_output.put_line('update error!');
  rollback;
end;
/

exec pro_2(3,'홍다희',23);
select * from person;

-- delete 
create or replace procedure pro_3(pid in person.id%type)
is
begin
  delete from person 
  where id=pid;
  commit;
exception when others then
  dbms_output.put_line('delete error!');
  rollback;
end;
/

exec pro_3(1);
select * from person;

-- select
create or replace procedure pro_4(vid in person.id%type)
is
  pid person.id%type;
  pname person.name%type;
  pweight person.weight%type;
begin
  select * into pid,pname,pweight from person where id=vid;
  dbms_output.put_line(pid || ' ' || pname || ' ' || pweight );
  commit;
exception when others then
  dbms_output.put_line('delete error!');
end;
/

exec pro_4(3);
select * from person;

-- select :복수 - 커서
create or replace procedure pro_5
is
  cursor cur is 
              select id, name, weight
              from person;
  pid person.id%type;
  pid person.name%type;
  pid person.weight%type;
begin
  open cur;
  loop
    fetch cur into pid,pname,pweight;
    exit when cur%notfound; -- 루프 빠져나가기.
      dbms_output.put_line(pid || ' ' || pname || ' ' || pweight );
  end loop; 
  close cur;
end;
/

exec pro_5;


-- open, fetch, close 없애기
create or replace procedure pro_6
is
  cursor cur is 
              select id, name, weight
              from person;
  pid person.id%type;
  pid person.name%type;
  pid person.weight%type;
begin
  
  for plist in cur loop
    dbms_output.put_line(plist.id || ' ' || plist.name || ' ' || plist.weight );
  end loop; 
  
end;
/

exec pro_6;

-- group by
create or replace procedure pro_7
is
  cursor cur is
                select buser_name, sum(jikwon_pay) tot, count(*) cnt
                from   jikwon inner join buser on buser_num=buser_no
                group by buser_name;
begin

  for jiklist in cur loop
    dbms_output.put_line(jiklist.buser_name);
    dbms_output.put_line(jiklist.tot);
    dbms_output.put_line(jiklist.cnt);

  end loop;
  exception when others then
    dbms_output.put_line('error!');
end;
/
exec pro_7;
```







```sql
-- 부서번호가 없으면 '임시직' 있으면 부서명을 반환하는 함수.

CREATE OR replace FUNCTION Func3 (bno NUMBER) 
RETURN VARCHAR2 
IS 
  bname VARCHAR2(20); 	-- IS 부서명 반환과 타입.
BEGIN 
    IF bno IS NULL THEN 
      RETURN '임시직'; 	-- 만약 bno가 null 이면 임시직 반환.
    ELSE 
      SELECT buser_name  -- buser 에서 buser_name 이라는 column 을 빼서
      INTO   bname 			 -- bname 에 넣는다.
      FROM   buser 
      WHERE  buser_no = bno; 

      RETURN bname; 
    END IF; 
END; 

/ 
SELECT jikwon_no, 
       jikwon_name, 
       buser_num, 
       Func3(buser_num) 
FROM   jikwon; 
```



- select * into 와 insert ino select 의 차이점.

  > http://egloos.zum.com/tit99hds/v/928582







`create user ID identified by PASS` id 와 pass 만들기

`grant connect to kbs;` kbs에게 계정 권한 부여.(read only)

`grant resource to kbs;` kbs에게 권한 부여 (read,write)

`grant connent,resource to kbs;`

`grant all on Table_name to Account_name;` 모든권한 한번에 주기.

` alter user kbs default tablespace users quota unlimited on users;` 테이블 권한주기.

`grant select on Table_name to Account_name;`

`revoke select on Table_name from Account_name;` 권한 취소.

`revoke all on Table_name from Account_name;` 모든권한 빼기

