---
TITLE : PRIMARY KEY - FOREIGN KEY
LANGUAGE : ORACLE SQL
---

## [PF] PRIMARY KEY - FOREIGN KEY

```SQL
CREATE TABLE student 
  ( 
     std_number NUMBER(4) PRIMARY KEY, 
       std_name VARCHAR2(30) NOT NULL, 
       sub_name NUMBER(4) REFERENCES lecture(lec_code), 
      std_grade NUMBER DEFAULT 1 CHECK ( 1 <= std_grade AND std_grade >= 4) 
  ); 

CREATE TABLE lecture 
  ( 
     lec_code NUMBER(4) PRIMARY KEY, 
     lec_name VARCHAR(30) UNIQUE, 
     txt_book VARCHAR(30), 
     lec_prof NUMBER REFERENCES prof(prof_code) 
  ); 

CREATE SEQUENCE seq_lec 
  MINVALUE 1 
  INCREMENT BY 1 
  START WITH 1; 

CREATE TABLE prof 
  ( 
     prof_code NUMBER PRIMARY KEY, 
     prof_name VARCHAR(30), 
     prof_labo NUMBER CHECK (100 <= prof_labo AND prof_labo <= 500) 
  ); 
  
  -- INSERT 
  INSERT INTO prof 
     VALUES (15, 
             'T이', 
             300); 
```

