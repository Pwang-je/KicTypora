-   notify(); wait(); Thread.
-   DTO, 파일처리
-   Component 배치 레이아웃
-   추상클래스
    -   [ ] git location settings
    -   [ ] layout 정리
    -   [ ] extends Frame 및 implements  Action Listener.

 



- insert 는 무조건 1개씩만 됨.
- 정규표현식. 1,2,3
  - 연산으로 구할 수 있는 것은 칼럼으로 절대 만들지 않는다.
  - 1개의 테이블은 주제가 같은 칼럼들끼리만 갖는다.
  - 정보의 최소화



`create table  Table_Name;` (변수 primary key, 변수 varchar2(글자수));

`insert into Table_Name;` (변수1, 변수2, 변수3...)



`drop table Table_Name;` -> 테이블 삭제.

`DELETE FROM TABLE_NAME VAR` -> 값 삭제. 커밋과 롤백 가능.

`TRUNCATE TABLE TABLE_NAME` -> 값 삭제. 자동 커밋이라 롤백 불가.



`desc Table_Name;` -> (테이블 확인)

`select * from Table_Name;` 테이블 출력.	

`var VARCHAR2 not null;` not null 은 값을 생략할 수 없다.



insert ~~~~ not null -> 생략 불가능, primary key(pk) -> 중복될수 없다.



`commit`	을 해야지만 상대방에게 보여질 수 있음.

`quit` 으로 빠져나올땐 commit 을 무조건 하고 빠짐.

`rollback` 클라이언트에서 작업한 모든 것들이 취소.

`update Table_Name set (var) = ;` 모든 자료 수정.



primary key -> 테이블 안에 넣을 때는 foreign key 안씀.










