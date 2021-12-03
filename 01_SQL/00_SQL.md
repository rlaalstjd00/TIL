## SQL

SQL (Structured Query Language)이란 구조적 질의 언어로, 관계형 데이터베이스 시스템 ( RDBMS )에서 자료를 관리 및 처리하기 위해 설계된 언어이다. SQL은 인터프리터 언어로, 번역문이 따로 존재하지 않는다. 

**SQL 명령어**

- DDL ( Data Definition Language ) : 데이터 정의어로, 테이블에 관련된 쿼리문이 포함된다.
- DML ( Data Manipulation Language ) : 데이터 조작어로, 실질적으로 데이터들을 CRUD 하는 언어이다.
- DCL ( Data Control Language ) : 데이터에 접근할 수 있는 권한을 관리하는 언어이다.
- TCL ( Transaction Control Language ) : 트랜잭션을 다루는 언어이다.

**자료형 **

- 숫자

  - NUMBER(n) :  n자리 정수

  - NUMBER(n, m) : n (전체 자리수) / m(소수점 자리수)

    ex) NUMBER(4,2) --> 12.45 같은 수

- 문자열

  - CHAR(n) : n바이트의 문자열(고정형), 빈 자리는 그대로 남겨둔다.

    ex) CHAR(4) --> [    ] --> 'A' 를 넣음 --> [A   ]

  - VARCAHR(n)/ VARCHAR2(n) : n바이트의 문자열(가변형), 빈자리는 할당 해제한다.

    ex) VARCHAR2(4) --> [    ] --> 'A' 를 넣음 --> [A]

- 시간(날짜)

  - DATE : 한 순간에 대한 시간 정보를 저장하는 타입.
  - TIMESTAMP : 연도, 월, 일, 시, 분, 초(밀리초) 까지 입력 가능.

