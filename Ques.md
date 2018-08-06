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









---

# java

갯수를 알면 for

모르면 while.



build path 읽기.

```java
// 기본 골격.
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;

public class DbTest1 {
	
	
	private Connection conn;	// db 연결 객체
	private java.sql.Statement stmt;	// sql 실행하는 클래스.
	private ResultSet rs;		// select 문의 결과 접근

}
```





jdbc

```java
try {
			// 1. Driver 클래스 로딩
			Class.forName("oracle.jdbc.driver.OracleDriver");	// class 와 Class 구별
		} catch (Exception e) {
			System.out.println("Driver 로딩 실패");
			return;
		}
		
		
		try {
			// 2. DB와 연결
			conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:orcl","scott","tiger");
		} catch (Exception e) {
			System.out.println("DB 연결 실패");
			
		}
		
		
		try {
			// 3. SQL문을 사용해 자료 읽기
			stmt = conn.createStatement();	// statements 객체 생성
			
			/*rs = stmt.executeQuery("select * from sangdata");
			rs.next();	// Record pointer 이동. 2개이상의 레코드는 안됨. 오로지 하나만됨, 이동했을때 해당 레코드가 있으면 true, 없으면 false 를 리턴함.
			
			String code = rs.getString("code");		// sql select*from sang 에 있는 column 명이름.
			String sangpum = rs.getString("sang");
			int su = rs.getInt("su");
			int dan = rs.getInt("dan");
			System.out.println(code + " " + sangpum + " " + su + " " + dan + " ");*/
			
			
			// 모든 자료 읽기.
			String sql = "select code,sang,su as 수량,dan 단가 from sangdata";	// as 생략가능.
			rs = stmt.executeQuery(sql);	// column 다쓰면 다뜸.
			
			int count = 0;
			
			while(rs.next()) {	// 자료가 있는 동안~~~~
				String code = rs.getString("code");		// sql select*from sang 에 있는 column 명이름.
				String sangpum = rs.getString("sang");	// 칼럼명에 따른 숫자대로 적어도됨. 1=code, 2=sang..
				int su = rs.getInt("수량");
				int dan = rs.getInt("단가");
				System.out.println(code + " " + sangpum + " " + su + " " + dan + " ");
				
				count += 1;
			}
			
			
			// 건수 구하기
			sql = "SELECT COUNT(*) FROM SANGDATA";
			rs = stmt.executeQuery(sql);
			rs.next();
			System.out.println("건수는 " + rs.getInt(1) + "건이넹");	// 1번째가 count(*)로 위에 설정 되어있어서 1로 적어도됨.
			System.out.println("건수는 " + count + "건이넹");	
			/*
			 * 자꾸 db접속하면 부하걸리니까 int=count =0; 으로 주고 count += 1;  이후에 sout 을 count로 바로줌.
			 */
			
		} catch (Exception e) {
			System.out.println("처리 실패");
			
		} finally {
			try {
				if(rs != null) rs.close();
				if(stmt != null) stmt.close();
				if(conn != null) conn.close();
			} catch (Exception e2) {
				
			}
		}
```



properties

```java

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.util.Properties;

Properties properties = new Properties();
		
		// read

		try {
			properties.load(new FileInputStream("C:\\work\\jsou\\java_inter\\src\\java_inter\\ex1.properties"));
			System.out.println(properties.getProperty("mes2"));
			System.out.println(properties.getProperty("mes1"));
		} catch (Exception e) {
			System.out.println("읽기 실패" + e);
		}
		
		
		
		// write
		
		try {
			properties.setProperty("mes1", "nice");
			properties.setProperty("mes2", "good");
			properties.setProperty("mes3", "hello");
			
			properties.store(new FileOutputStream("C:\\work\\jsou\\java_inter\\src\\java_inter\\ex1.properties"), null);
			System.out.println("저장 성공");
		} catch (Exception e) {
			System.out.println("쓰기 실패" + e);
		}
```

select 만 execuetQuery 씀.

secure coding

```java
package java_inter;

import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.util.Properties;

public class dbTest2 {

	// secure coding 작업: 별도 정보 파일 읽기.
	
	
	
	private Connection conn;	// db 연결 객체
	private java.sql.Statement stmt;	// sql 실행하는 클래스.
	private ResultSet rs;		// select 문의 결과 접근
	Properties properties = new Properties();
	
		
	
	
	
	
		
	
	private void dbtest2() {
	
		try {
			properties.load(new FileInputStream("C:\\work\\jsou\\java_inter\\src\\java_inter\\dbmeta.properties"));
		} catch (Exception e) {
			System.out.println("처리 오류:" + e.getMessage());
		} finally {
			try {
				if(rs != null) rs.close();
				if(stmt != null) stmt.close();
				if(conn != null) conn.close();
			} catch (Exception e2) {
				
			}
		}
	
	}
	
	public static void main(String[] args) {
		
		new dbTest2();

	}

}

```



#### 마지막 작업한거. 풀어내야함.

```java
package java_inter;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class DbTest3_gui extends JFrame implements ActionListener {

	JButton btnAll = new JButton("전체");
	JButton btnM = new JButton("남");
	JButton btnF = new JButton("여");
	JTextArea txtResult = new JTextArea();
	
	// SQL 담당.
	Connection conn;
	Statement stmt;
	ResultSet rs;
	
	
	
	public DbTest3_gui() {
		
			setTitle("고객 테이블 출력");
			
			layInit();
			accDb();
			
			setBounds(200,200,300,250);
			setVisible(true);
			setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
	
	private void layInit() {
		JPanel panel = new JPanel();
		panel.add(btnAll);
		panel.add(btnM);
		panel.add(btnF);
		
		txtResult.setEditable(false);	// read only.
		JScrollPane pane = new JScrollPane(txtResult);
		
		add("Center", pane);
		add("North", panel);
		
		btnAll.addActionListener(this);
		btnM.addActionListener(this);
		btnF.addActionListener(this);
		
	}
	
	
	private void accDb() {
		
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
		} catch (Exception e) {
			System.out.println("드라이버 로딩 실패:" + e);
		}
		
		
		
	}
	
	
	
	@Override
	public void actionPerformed(ActionEvent e) {
		
		try {
			conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:orcl", "scott", "tiger");
			stmt = conn.createStatement();
			String sql = "";
			
			sql = "SELECT GOGEK_NO, GOGEK_NAME, GOGEK_JUMIN FROM GOGEK";
			
			if(e.getSource() == btnAll) {
				
			} else if (e.getSource() == btnM) {
//				sql += " WHERE GOGEK_JUMIN LIKE '%-1%'";
				sql += " WHERE SUBSTR(GOGEK_JUMIN, 8, 1)=1";
			} else if (e.getSource() == btnF) {
				sql += " WHERE SUBSTR(GOGEK_JUMIN, 8, 1)=2";
			}
			
			
			/*System.out.println(sql);	// 확인용.
*/			
			txtResult.setText(null);	// ""  처음에 깨끗하게 비우기용.
			
			rs = stmt.executeQuery(sql);
			int cou = 0;
			while(rs.next()) {
//				System.out.println(rs.getString(2));
				
				String str = rs.getString("GOGEK_NO") + "\t" +
								rs.getString("GOGEK_NAME") + "\t" +
								rs.getString("GOGEK_JUMIN") + "\n";
				txtResult.append(str);
				cou++;
				
			}
			txtResult.append("인원수 : " + cou + " 명");
		} catch (Exception e2) {
			System.out.println("actionPerformed err:" + e2);
		} finally {
			try {
				if(rs != null) rs.close();
				if(stmt != null) stmt.close();
				if(conn != null) conn.close();
			} catch (Exception e3) {
				
			}
			
		}
		
		
	}
	
	
	public static void main(String[] args) {
		
		new DbTest3_gui();

	}

}
```



```java
// stmt = conn.createStatement();  // rs.next() 만 가능함.
stmt = conn.createStatement(    // 이렇게 쓰면 역방향도 가능함.
    ResultSet.TYPE_SCROLL_INSENSITIVE,
    ResultSet.CONCUR_READ_ONLY
);
```



사번:	직원명:		직급:	

부서명:		부서번호:	

```java
JTextField 
사번 		txtNo_sa, txtName_sa, 
직원명	 txtNo_name, txtName_name, 
직급		txtNo_rank, txtName_rank,
부서명		txtNo_def, txtName_def,
부서번호 txtNo_bunum, txtName_bunum;
```

```java
package db.pack1;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;

public class DbtestExam2 extends JFrame implements ActionListener{
	JButton btnF, btnP, btnN, btnL;
	JTextField txtNo, txtName, txtJik, txtBuName, txtBuTel;
	JTextArea txtGogek = new JTextArea();
	
	Connection conn;
	Statement stmtJik, stmtGogek;
	ResultSet rsJik, rsGogek;
	String sqlJik;
	
	public DbtestExam2() {
		setTitle("고객 정보 열람");
		
		layInit();
		accDb();
		
		setBounds(200, 200, 700, 450);
		setVisible(true);
		addWindowListener(new WindowAdapter() {
			@Override
			public void windowClosing(WindowEvent e) {
				try {
					if(rsJik != null) rsJik.close();
					if(stmtJik != null) stmtJik.close();
					if(rsGogek != null) rsJik.close();
					if(stmtGogek != null) stmtJik.close();
					if(conn != null) conn.close();
				} catch (Exception e2) {
				}
				System.exit(0);
			}
		});
	}
	
	private void layInit() {
		txtNo = new JTextField("", 5);
		txtName = new JTextField("", 8);
		txtJik = new JTextField("", 5);
		txtBuName = new JTextField("", 5);
		txtBuTel = new JTextField("", 10);
		
		JPanel panel1 = new JPanel();
		panel1.add(new JLabel("사번 : "));
		panel1.add(txtNo);
		panel1.add(new JLabel("직원명 : "));
		panel1.add(txtName);
		panel1.add(new JLabel("직급 : "));
		panel1.add(txtJik);
		panel1.add(new JLabel("부서명 : "));
		panel1.add(txtBuName);
		panel1.add(new JLabel("부서전화 : "));
		panel1.add(txtBuTel);
		
		add("North",panel1);
		
		btnF = new JButton("|<<");
		btnP = new JButton("<");
		btnN = new JButton(">");
		btnL = new JButton(">>|");
		
		JPanel panel3 = new JPanel();
		panel3.add(btnF);
		panel3.add(btnP);
		panel3.add(btnN);
		panel3.add(btnL);
		add("South",panel3);
		
		btnF.addActionListener(this);
		btnP.addActionListener(this);
		btnN.addActionListener(this);
		btnL.addActionListener(this);
		
		txtGogek.setEditable(false);
		JScrollPane pane = new JScrollPane(txtGogek);
		add("Center", pane);
	}
	
	private void accDb() {
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
			conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:orcl", "scott", "tiger");
			stmtJik = conn.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_READ_ONLY);
			sqlJik = "select jikwon_no, jikwon_name, jikwon_jik, buser_name, buser_tel "
					+ "from jikwon left outer join buser on buser_no = buser_num order by jikwon_no";
			
			rsJik = stmtJik.executeQuery(sqlJik);
			rsJik.next();
	
			display();
		} catch (Exception e) {
			System.out.println("accDb err : " + e);
		}
	}
	
	private void display() {
		try {
			txtNo.setText(rsJik.getString("jikwon_no"));
			txtName.setText(rsJik.getString("jikwon_name"));
			txtJik.setText(rsJik.getString("jikwon_jik"));
			txtBuName.setText(rsJik.getString("buser_name"));
			txtBuTel.setText(rsJik.getString("buser_tel"));	
			
			stmtGogek = conn.createStatement();
						
			displayGogek();
		} catch (Exception e) {
			JOptionPane.showMessageDialog(this, "자료의 처음 또는 마지막 입니다.");
		}
	}
	
	private void displayGogek() {
		try {
			String sqlGogek = "select gogek_no, gogek_name, " + 
					"case " + 
					"when substr(gogek_jumin,8,1)=1 then '남' " + 
					"else '여' end as gogek_gen, " + 
					"to_char(sysdate, 'yy')+101 - substr(gogek_jumin,1,2) as gogek_nai from gogek";

			sqlGogek += " where gogek_damsano = " +  rsJik.getString("jikwon_no");
			rsGogek = stmtGogek.executeQuery(sqlGogek);
			
			txtGogek.setText(null);
			
			txtGogek.append("고객번호\t고객명\t성별\t나이\n");
			
			int cou = 0;
			while(rsGogek.next()) {
				String str = rsGogek.getString("gogek_no") + "\t" + 
						rsGogek.getString("gogek_name") + "\t" + 
						rsGogek.getString("gogek_gen") + "\t" +
						rsGogek.getString("gogek_nai") + "\n";
				txtGogek.append(str);
				cou++;
			}
			
			txtGogek.append("인원 수 : " + cou + "명");
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	@Override
	public void actionPerformed(ActionEvent e) {
		try {
			if(e.getSource() == btnF) rsJik.first();
			else if(e.getSource() == btnP) rsJik.previous();
			else if(e.getSource() == btnN) rsJik.next();
			else if(e.getSource() == btnL) rsJik.last();
		
			display();
		} catch (Exception e2) {
		}
	}
	
	public static void main(String[] args) {
		new DbtestExam2();
	}
}

```

- 오라클 프로시져
- 

maria db

mysql -u root -h 127.0.0.1 0p

123

```sql
-- maria DB
Class.forName("org.mariadb.jdbc.Driver");
conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "123");

-- oracle
Class.forName("oracle.jdbc.driver.OracleDriver");
      conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:orcl", "scott", "tiger");
```

```sql
String co = "1";  // 원래 외부값을 받아와야됨. 지금은 없으니 일단 만들어둠.
      /*sql = "SELECT * FROM SANGDATA WHERE CODE =" + co;   // 이렇게 쓰면 안댐.*/
      sql = "SELECT * FROM SANGDATA WHERE CODE =?"; // 이렇게 써야됨.
      pstmt = conn.prepareStatement(sql);
      pstmt.setString(1,co);  // =? 가 있을 때 써줌.
      rs = pstmt.executeQuery();
      if (rs.next()) {
        System.out.println(rs.getString(1));
        System.out.println(rs.getString("sang"));
        System.out.println(rs.getString("su"));
        System.out.println(rs.getString("dan"));
      } else {
        System.out.println("그런자료 없음");
      }
```

select
jikon_no, jikwon_name
from
jikwon
where
buser_num

select
gogek_name, gogek_tel, gogek_jumin
from gogek
where gogek_damsano

```java
-- db연동sample

Required Steps
The following steps are required to create a new Database using JDBC application −

Import the packages: Requires that you include the packages containing the JDBC classes needed for database programming. Most often, using import java.sql.* will suffice.

Register the JDBC driver: Requires that you initialize a driver so you can open a communications channel with the database.

Open a connection: Requires using the DriverManager.getConnection() method to create a Connection object, which represents a physical connection with a database server.

Execute a query: Requires using an object of type Statement for building and submitting an SQL statement to insert records into a table.

Clean up the environment: Requires explicitly closing all database resources versus relying on the JVM's garbage collection.
  
  //STEP 1. Import required packages
import java.sql.*;

public class JDBCExample {
   // JDBC driver name and database URL
   static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";  
   static final String DB_URL = "jdbc:mysql://localhost/STUDENTS";

   //  Database credentials
   static final String USER = "username";
   static final String PASS = "password";
   
   public static void main(String[] args) {
   Connection conn = null;
   Statement stmt = null;
   try{
      //STEP 2: Register JDBC driver
      Class.forName("com.mysql.jdbc.Driver");

      //STEP 3: Open a connection
      System.out.println("Connecting to a selected database...");
      conn = DriverManager.getConnection(DB_URL, USER, PASS);
      System.out.println("Connected database successfully...");
      
      //STEP 4: Execute a query
      System.out.println("Inserting records into the table...");
      stmt = conn.createStatement();
      
      String sql = "INSERT INTO Registration " +
                   "VALUES (100, 'Zara', 'Ali', 18)";
      stmt.executeUpdate(sql);
      sql = "INSERT INTO Registration " +
                   "VALUES (101, 'Mahnaz', 'Fatma', 25)";
      stmt.executeUpdate(sql);
      sql = "INSERT INTO Registration " +
                   "VALUES (102, 'Zaid', 'Khan', 30)";
      stmt.executeUpdate(sql);
      sql = "INSERT INTO Registration " +
                   "VALUES(103, 'Sumit', 'Mittal', 28)";
      stmt.executeUpdate(sql);
      System.out.println("Inserted records into the table...");

   }catch(SQLException se){
      //Handle errors for JDBC
      se.printStackTrace();
   }catch(Exception e){
      //Handle errors for Class.forName
      e.printStackTrace();
   }finally{
      //finally block used to close resources
      try{
         if(stmt!=null)
            conn.close();
      }catch(SQLException se){
      }// do nothing
      try{
         if(conn!=null)
            conn.close();
      }catch(SQLException se){
         se.printStackTrace();
      }//end finally try
   }//end try
   System.out.println("Goodbye!");
}//end main
}//end JDBCExample
```

```java
// try catch finally

try {
      
} catch (Exception e) {
      
} finally {
      try {
        if(rs != null) rs.close();
        if(pstmt != null) pstmt.close();
        if(conn != null) conn.close();
      } catch (Exception e2) {
       
      }
}
```



jtable

```java
sout("값: " + model.getValueAt(table))
  
열번호 고정하고 값 얻기.
  sout("열고정 값: " + model.getValueAt(table.getSelectedRow(), 1));
	// 1열 고정.



table.addMouseListener(new MouseAdapter() {
		@Override
		public void mouseClicked(MouseEvent e) {
			table = (JTable)e.getComponent();
			model = (DefaultTableModel)table.getModel();
		}
	});

```



`http://egloos.zum.com/sweeper/v/3002133  조인`

