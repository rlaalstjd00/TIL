## MyBatis

모델과 DB의 매개체

자바 소스코드 안에 SQL문을 작성하면 코드가 길어지고 유지보수 및 분업이 쉽지 않다. 이러한 문제를 해결하기 위해 MyBatis를 사용하는데, MyBatis는 기존 JDBC 방식과는 다르게 SQL문을 XML  파일에 작성함으로써 코드가 줄어들고 SQL문 수정이 편해진다. 또한 DBCP를 사용하여 커넥션을 여러개 생성하기 때문에 JDBC만 사용하는 것보다 작업 효율과 가독성이 좋아진다.

> [JDBC DBCP가 뭐더라..? 클릭!](https://github.com/rlaalstjd00/TIL/blob/master/02_DBconnection/00_JDBC%20DBCP%20JNDI.md)

#### MyBatis 작동원리

1. SqlSessionFactoryBuilder는 SqlSessionFactory를 생성하기 위한 MyBatis 구성 파일을 읽는다.
2. 클라이언트가 응용 프로그램에 대한 프로세스를 요청한다.
3. Application은 SqlSessionFactoryBuilder을 사용하여 빌드된 SqlSessionFactory에서 SqlSession을 가져온다.
4. Application이 SqlSessioin에서 Mapper 인터페이스 구현 개체를 가져온다.
5. Application이 Mapper 인터페이스의 메서드를 호출한다.
6. Mapper 인터페이스의 구현 객체가 SqlSession 메서드를 호출하고 SQL문 실행을 요청한다.
7. SqlSession은 Mapping 파일에서 실행할 SQL을 가져와서 실행한다.

> [MyBatis 공식 문서 사이트](https://mybatis.org/mybatis-3/ko/index.html)

#### MyBatis의 사용

mybatis 패키지에 config.xml과 SqlMapConfig.java 설정파일을 만들어 사용한다.

- SqlMapConfig.java

  static 블럭을 사용해 최초 실행시 SqlSessionFactory를 생성한다.

- config.xml

  DB연결의 기본 설정을 하고 SQL문이 적힌 xml파일을 매핑한다.

DAO 클래스에서는 SQL문을 실행하는 메서드만 존재하고 SQL문은 모두 xml파일로 따로 뺀다.

- ..DAO.java

  ````java
  // 회원가입
  public boolean join(UserDTO newUser){
      int result = sqlsession.insert("User.join", newUser);
      return result == 1;
  }
  ````

  > 파라미터를 넘겨줄 때 ("namespace.id", 파라미터) 의 형식으로 넘겨주고, xml파일에 정의되어 있는 SQL문 중 일치하는 namespace와 id를 가진 SQL문이 실행된다.

- ...xml

  ````xml
  <!-- 회원가입 메서드 호출시 실행될 SQL문 -->
  <mapper namespace="User">
  	<insert id="join" parameterType="com.minsung.dto.UserDTO">
      	INSERT INTO MYBATIS_TEST_USER VALUES(#{userid}, #{userpw}, #{username})
      </insert>
  </mapper>
  ````

  > 넘겨받는 파라미터 타입이 UserDTO 타입인 newUser이기 때문에 parameterType은 그 UserDTO의 경로를 써준다. 이 때 경로가 너무 길어지는 것을 방지하기 위해 config.xml 파일에 `<typeAlias>` 태그를 통해 별칭을 설정해서 사용할 수 있다.
  >
  > 위의 예시코드에서는 insert문이기 때문에 parameterType밖에 없지만 select문 같은 경우에는 parameterType 뿐만 아니라 resultType까지 명시해 주어야 한다.

#### MyBatis 예제

- [MyBatis를 사용해 회원가입 및 로그인 구현](https://github.com/rlaalstjd00/Web_practice/tree/master/01_mybatis_prac)

