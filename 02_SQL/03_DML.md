## DML (Data Manipulation Language)

DML이란 데이터 조작어로, 실질적으로 데이터들을 CRUD 하는 언어이다.

- 데이터 추가

  `INSERT INTO 테이블명 (컬럼명1, 컬럼명2, ..) VALUES(값1, 값2, ..)` 의 형식으로 사용한다.
  
  이 때 컬럼명은 생략 가능하며, 생략할 시 테이블의 구성 순서대로 값을 넘겨준다.

  ````sql
  -- 데이터를 추가할 USER1 테이블 만들기
  CREATE TABLE USER1(
      USER_ID VARCHAR(300),
  	USER_NAME VARCHAR(300),
      USER_AGE NUMBER(3),
      USER_ADDR VARCHAR(1000),
      CONSTRIANT USER1_PK PRIMARY KEY USER1(USER_ID)
  );
  -- 테이블에 값 추가 (컬럼명 포함)
  INSERT INTO USER1 (USER_ID, USER_NAME, USER_AGE) VALUES('xyz1234', '가나다', '15');
  -- 테이블에 값 추가 (컬럼명 생략)
  INSERT INTO USER1 VALUES('abc1234', '홍길동', 25, '성남시 분당구');
  ````
  
  > 위의 코드에서 먼저 컬럼명을 포함해 테이블에 값을 추가하는 문장을 보자. 컬럼 `USER_ID` 와 `USER_NAME` 과 `USER_AGE` 에 각각 'xyz1234', '가나다', '15'의 값을 추가했다. 이 때 이 데이터를 추가한 행이 생길 것이고 데이터를 추가하지 않는 `USER_ADDR`엔 `NULL` 값이 할당될 것이다.
  >
  > 다음으로 컬럼명을 생략해 값을 추가하는 문장을 보면, 테이블의 구성 순서인 아이디, 이름, 나이, 주소 순서대로 넘겨 데이터를 추가한 것을 볼 수 있다.
  >
  > 그리고 테이블에 값을 추가할 때, PK로 지정한 컬럼은 중복값을 허용하지 않으며, 비어있으면( `NULL` ) 안된다.

- 데이터 검색

  `SELECT 컬럼명1, 컬럼명2, .. FROM 테이블명 WHERE 조건식` 의 형식으로 사용한다.

  이 때 테이블 전체를 검색해오려면 컬럼명을 쓰는 곳에 `*` 을 사용하면 된다.

  ````sql
  -- USER1 테이블에서 아이디 와 이름 검색
  SELECT USER_ID, USER_NAME FROM USER1;
  -- USER1 테이블 모두 검색
  SELECT * FROM USER1;
  -- USER1 테이블에서 나이정보가 20살인 행의 아이디와 이름 검색
  SELECT USER_ID, USER_NAME FROM USER1 WHERE USER_AGE = 20;
  ````

- 데이터 수정

  `UPDATE 테이블명 SET 컬럼명1=바꿀값1, 컬럼명2=바꿀값2, ... WHERE 조건식` 의 형식으로 사용한다.

  ````sql
  -- USER1 테이블에서 이름정보가 '가나다'인 행의 아이디를 'qwe1234'로, 나이를 13으로 수정
  UPDATE USER1 SET USER_ID='qwe1234', USER_AGE='13' WHERE USER_NAME='가나다';
  ````

  > 데이터 추가와 마찬가지로 PK 값을 중복되게 바꿀 수 없다.

- 데이터 삭제

  `DELETE FROM 테이블명 WHERE 조건식` 의 형식으로 사용한다.

  ````sql
  -- USER1 테이블에서 나이정보가 22인 행을 삭제
  DELETE FROM USER1 WHERE USER_AGE=22;
  ````

  

#### ALIAS(별칭)

`SELECT` 문으로 결과를 검색할 때 컬럼에 `AS` 키워드를 사용하여 별칭을 줄 수 있다.

[USER2] 테이블

| column1 | column2 | column3 |
| :-----: | :-----: | :-----: |
|  철수   |   20    |  자바   |
|  영희   |   21    |  DBMS   |

> 위의 코드에서 데이터만을 보고서는 이 컬럼이 어떤 정보를 담고있는지 유추하기 힘들다. 따라서 이 때는 각 컬럼에 별칭을 주면 컬럼명으로 별칭이 출력되어 좀더 가독성을 높일 수 있다.
>
> 이 때 별칭이 키워드거나 띄어쓰기가 포함된 경우에는 쌍따옴표로 묶어준다.
>
> `AS` 키워드는 생략 가능하다.

````sql
-- column1에는 이름, column2에는 나이, column3에는 수강 과목 의 별칭을 주고
-- USER2 테이블에서 이름이 철수인 데이터 출력
SELECT column1 AS 이름, column2 AS 나이, column3 AS "수강 과목" 
FROM USER2
WHERE column1 = '철수';

-- AS 키워드 생략 가능
SELECT column1 이름, column2 "수강 과목"
FROM USER2
WHERE column3 = 'DBMS';
````

검색된 테이블

| 이름 | 나이 | 수강 과목 |
| :--: | :--: | :-------: |
| 철수 |  20  |   자바    |

| 이름 | 수강 과목 |
| :--: | :-------: |
| 영희 |   DBMS    |

