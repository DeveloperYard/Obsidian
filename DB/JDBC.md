> 자바 프로그래밍 언어로 만들어진 클래스와 인터페이스로 이루어진 API로서 ANSI SQL을 지원한다. SQL 문을 실행할 수 있는 함수 호출 인터페이스이다.


### JDBC 특징

- DBMS 종류에 독립적인 자바 프로그래밍 가능
- DB가 달라지더라도 ==동일한 API==를 사용 가능 (드라이버 및 URL만 수정하면 됨)
- 자바가 가지는 플랫폼에 독립적이라는 특성과 DBMS에 독립적인 특성을 가짐


### JDBC 기능

- DB에 연결 설정
- SQL문장을 DBMS에 전송
- SQL문장 전송 후 결과를 처리하게 해줌

### JDBC Interace

- DB를 만드는 업체에게 제공되는 인터페이스
- 프로그래머에게 제공되는 인터페이스

> 커넥션 정보는 드라이버 내에 있음!

### JDBC를 진행하는 순서

1. Driver class loading
2. DB 연결 -> Connection이라는 인터페이스에 객체를 생성
3. SQL 실행 준비 -> SQL문 작성, Statement 생성
4. SQL 실행 -> 
	1. executeUpdate() : 데이터 갱신, insert, update, delete
	2. executeQuery() : select
5. 접속 종료, Result set 닫고, statement 닫고, 커넥션 닫아야 함


### ==DB에 연결을 진행할 때는 비용이 크다.. 느림!==


## JDBC API

- Connection 
	- DB에 대한 하나의 세션을 표현한다.
		- 세션은 하나의 클라이언트가 서버에 요청을 하기 위해 연결을 맺은 상태를 의미한다.


### Statement

- statement
- PreparedStatement : statement 보다 보안도 좋고, 성능도 더 좋음!
- CallableStatement : DB에 대해 실제 SQL문을 실행하는 것이 아니라 저장된 프로시저를 호출한다.


#### ResultSet

- 쿼리에 대한 결과값 처리
- ResultSet 객체의 커서는 첫 번째 레코드보다 바로 이전을 가리킨다.
- getString, Int, Date() 등으로 데이터를 얻을 수 있다.


### cf )

==Connection을 미리 여러 개 만들어 놓음!==

>커넥션 풀은 **데이터베이스와 연결된 커넥션을 미리 만들어 놓고 이를 pool로 관리**하는 것이다. 즉, 필요할 때마다 커넥션 풀의 커넥션을 이용하고 반환하는 기법이다. 이처럼 미리 만들어 놓은 커넥션을 이용하면 Connection에 필요한 비용을 줄일 수 있다.






> JAVA와 DB(MySQL, Oracle, etc.)들 사이에서 중재 역할을 함

JDBC 내에 인터페이스를 가지며, 중간 단계에서 정의만 해줌.
껍데기 속 알맹이들은 DB 회사들이 채움. ex) classes etc. -> .jar


ex) 
DB와 관계 없이 getConnection()만 사용하면 연결할 수 있고, execute()만 사용하면 DB를 사용할 수 있다!




### Q. JDBC는 그럼 쿼리가 달라지면 다시 짜야하는 건가?

### Q. StringBuilder는 sysout에 넣었을 때 왜 toString을 안해도 출력이 될까?