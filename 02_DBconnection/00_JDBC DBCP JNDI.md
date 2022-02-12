## Java와 DB의 연결

#### JDBC, DBCP, JNDI의 이해

- JDBC (Java DataBase Connectivity)
  - 자바에서 DB 프로그래밍을 하기 위해 사용되는 API이다.
  - JDBC는 데이터베이스풀 방식을 사용하지 않고 DB에서 정보를 가져올 떄마다 DB 연결을 열고 닫는다.
  
- DBCP (Database Connection Pool)
  - JDBC의 비효율적인 특징을 보완하기 위해 DBCP 방식을 사용한다.
  - 사용자의 요청이 있을 때마다 DB연결을 한다면 코드가 복잡해지며 많은 요청이 있을 때 속도가 저하될 수 있기 때문에, 미리 Connection을 만들어 두고 필요시 저장된 공간에서 가져다 쓰고 반납한다.
  
- JNDI (Java Naming and Directory Interface)
  - WAS단에 데이터베이스 커넥션 객체를 미리 네이밍해두는 방식이다.
  
  - 사용자 요청 > JNDI에 등록된 DB객체 검색 > 찾은 객체에서 커넥션 획득 > DB작업 종료 후 커넥션 반납
  
    

````xml
<!-- context.xml -->
<Resource
    name="jdbc/oracle"
    auth="Container"
    type="javax.sql.DataSource"
    driverClassName="driverName"
    url="jdbc:oracle:thin:.."
    username="dbusername"
    password="dbuserpw"
    maxActive="20"
    maxIdle="20"
    maxWait="-1"
/>
````

> name : dbcp를 이용하기 위한 name (key값)
>
> maxActive : 연결 최대 허용 개수
>
> maxIdle : 항상 연결 상태를 유지하는 개수 (보편적으로 maxActive와 같게)
>
> maxWait : 커넥션 풀에 연결가능한 커넥션이 없을 경우 대기하는 시간

````xml
<!-- web.xml -->
<resource-ref>
  	<description>Connection</description>
  	<res-ref-name>jdbc/oracle</res-ref-name>
  	<res-type>javax.sql.DataSource</res-type>
  	<res-auth>Container</res-auth>
</resource-ref>
````

대표적으로 위의 코드와 같이 context.xml과 web.xml 파일에 설정해준다.

그리고 아래와 같이 DB에 접근하는 코드를 작성할 수 있다.

````java
Context context = new InitialContext(null);
DataSource ds = (DataSource)context.lookup("java:comp/env/jdbc/oracle");
Connection conn = ds.getConnection();

String sql = "작성할 SQL문";

PreparedStatement ps = conn.prepareStatement(sql);
````

