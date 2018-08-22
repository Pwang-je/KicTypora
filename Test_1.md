---
Date : 08-20, 08-21
Name : Test_1
---

[TOC]



### 자바 버전 확인 명령

`java -version`



### ip 확인방법

`ipconfig`



### path 확인 (cmd)

`path`



### apache, java 환경변수

변수 이름 : CATALINA_HOME
변수 값 : C:\apache-tomcat-8.5.32

변수 이름 : JAVA_HOME
변수 값 : 자바폴더.

변수 이름 : Path
변수 값 : %JAVA_HOME%\bin' 추가.



### package 작성방법, 왜 만드는지.

클래스의 묶음, 클래스 또는 인터페이스를 포함할 수 있으며 서로 다른 클래스들끼리 그룹단위로 묶음으로써 효율적으로 관리하기 위함.

`package 패키지명;`



### 키보드를 통해 입력받을때 쓰는 클래스와 import방법

```java
import java.util.*

dto = new StuDto();

Scanner sc = new Scanner(System.in);
System.out.println("이름을 입력하세요");
String name = sc.next();	// 받은 이름을 name 에 저장.
dto.setName(name);	// 저장된 name 값을 set.
```



### tcp/ip 기반 네트워크 서버, 클라이언트간 통신 할때 사용하는 변수

서버 - 소켓을 생성 및 주소 할당, 데이터를 송.수신

클라이언트 - 소켓 생성 후 데이터 수신.

tcp/ip : 소켓.

udp : 데이타그램 소켓.

-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA 2018.2.1\bin\JetbrainsCrack.jar

### tcp/ip 와 udp의 특징 비교.

| tcp/ip                   | udp                      |
| ------------------------ | ------------------------ |
| 연결형 프로토콜.         | 비연결형 프로토콜.       |
| 신뢰성 있는 데이터 전송. | 실뢰성 없는 전송.        |
| 일대일 통신(유니캐스트)  | 일대일 통신, 다대다 통신 |



### 프로토콜이 무엇인지, 대표적인 종류에 대해.





### java compile 실행명령(cmd)

`javac`



### 메소드 오버라이딩 성립 조건

Overriding.

조상 클래스로부터 상속 받은 메서드의 내용을 변경하는 것.

```markdown
- 부모와 자식 관계에서만 성립.
- static은 상속 안됨
- private 도 상속 안됨
- interface를 구현할땐 반드시 public으로 해야됨
- final 은 오버라이딩 안됨
```



### 오버로딩은 무엇인가?

오버로딩 : 한 클래스 내에 같은 이름의 메소드를 여러 개 정의하는 것.

조건 : 메소드 이름은 같아야 하고 매개변수가 달라야 함.



### 표준 출력장치로 출력할 때의 명령어.

`System.out.println();`



### jdbc 할 때, class.forname, pstmt, rs의 역할

```java
Driver 클래스가 메모리로 로드함.
 Class.forName("oracle.jdbc.driver.OracleDriver");
pstmt - 작성한 sql문을 가져오는 것.
  rs - 가져온 sql문을 실행하는 것.
```



### 메소드 만들 때 반환형, 파라미터, 메소드 작성 유형

```java
public void,
int String.
  // 접근지정자 반환명 메소드명(매개변수) {}
```



### 형변환이 2개 있는데 설명하라.

Promotion 자동 형변환, Casting 강제 형변환.

```java
byte b1 = (byte1)128; // 강제 형변환

// String to Int.
String from = "123";
int to = Integer.parseInt(from);

```



### Private 멤버에게 값주는 방법

```java
// 간단하게 setter 와 getter 를 쓰면 됨.




```



### interface를 상속하고 구현하고

```java
public class CLASS_NAME implements INTERFACE_NAME {
  // 인터페이스에 있는 모든 메소드를 선언해야 컴파일 에러가 안남.
  인터페이스 변수 = new 인터페이스() {
    // 인터페이스에 선언된 추상 메소드의 실체 선언.
  }
  
  public void turnOn() {
    // 실행문
  }
  public void turnOff() {
    // 실행문
  }
  
}
```



### 상속에 대하여

```java
// 조상 클래스.
	parent, super, base.
  
// 자손 클래스.
  child, sub, derived.

// 부모 클래스가 가지고 있는 모든걸 자식클래스가 물려받아 같이 공유하며 확장하는 개념.
```



### pstmt 쓰는 방법

```java
try {
  accDb();
  String sql = "SELECT * FROM SANGDATA WHERE SANGPUM = ?";
  pstmt = conn.prepareStatement(sql);
  pstmt.setString(1, "codedragon");
  ResultSet rs = pstmt.executeUpdate();
} catch (Exception e) {
  system.out.println("err: " + e);
}
```



### Stringbuffer 문자열 더할 때 쓰는 메소드?

```java
public static void main(String[] args) {
  StringBuffer sb = new StringBuffer(); // 스트링버퍼
  sb.append("hello");
  sb.append("java");
  System.out.println(sb.toString());
}
// result = hellojava
```

