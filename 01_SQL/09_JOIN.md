## JOIN

#### 여러 테이블에 흩어져 있는 정보중 사용자가 필요한 정보만 가져와서 가상의 테이블처럼 만들어 결과를 보여주는 것

#### 1. 내부조인 (INNER JOIN)

조건이 일치하는 값이 두 테이블에 모두 존재할 때 사용 (INNER 은 생략 가능하다.)

> USER1 테이블
>
> | USER_ID  | USER_NAME | USER_AGE |
> | :------: | :-------: | :------: |
> | abc1234  |  홍길동   |    23    |
> | qwer5678 |  가나다   |    33    |
>
> PURCHASE 테이블
>
> | USER_ID | PURCHASE_ITEM |
> | :-----: | :-----------: |
> | abc1234 |     사과      |
> | xyz7890 |    바나나     |

````sql
SELECT * FROM USER1
JOIN PURCHASE ON(USER1.USER_ID = PURCHASE.USER_ID);
````

> USER1 테이블의 USER_ID와 PURCHASE 테이블의 USER_ID 값이 같은 모든 컬럼 가져오기.
>
> | USER_ID | USER_NAME | USER_AGE | USER_ID | PURCHASE_ITEM |
> | :-----: | :-------: | :------: | :-----: | :-----------: |
> | abc1234 |  홍길동   |    23    | abc1234 |     사과      |

#### 2. 외부조인 (OUTER JOIN)

두 테이블 중 한쪽은 조건이 거짓이더라도 모든 정보가 검색되어야 할 때 사용

- LEFT OUTER JOIN : 조인문의 왼쪽에 있는 테이블의 모든 결과를 가져온 후 오른쪽 테이블의 데이터 비교

  ```` sql
  SELECT * FROM USER1
  LEFT OUTER JOIN PURCHASE
  ON USER1.USER_ID = PURCHASE.USER_ID
  ````

  > USER1 테이블의 모든 결과와 PURCHASE 테이블을 비교한다.
  >
  > | USER_ID  | USER_NAME | USER_AGE | USER_ID | PURCHASE_ITEM |
  > | :------: | :-------: | :------: | :-----: | :-----------: |
  > | abc1234  |  홍길동   |    23    | abc1234 |     사과      |
  > | qwer5678 |  가나다   |    33    | `null`  |    `null`     |

- RIGHT OUTER JOIN : 조인문의 오른쪽에 있는 테이블의 모든 결과를 가져온 후 왼쪽 테이블의 데이터 비교

  ````sql
  SELECT * FROM USER1
  RIGHT OUTER JOIN PURCHASE
  ON USER1.USER_ID = PURCHASE.USER_ID
  ````

  > PURCHASE 테이블의 모든 결과와 USER1 테이블을 비교한다.
  >
  > | USER_ID | USER_NAME | USER_AGE | USER_ID | PURCAHSE_ITEM |
  > | :-----: | :-------: | :------: | :-----: | :-----------: |
  > | abc1234 |  홍길동   |    23    | abc1234 |     사과      |
  > | `null`  |  `null`   |  `null`  | xyz7890 |    바나나     |

- FULL OUTER JOIN : 양쪽 모두 조건이 일치하지 않는 것까지 모두 결합해 출력

  > 두 테이블을 결합해 출력한다.
  >
  > | USER_ID  | USER_NAME | USER_AGE | USER_ID | PURCHASE_ITEM |
  > | :------: | :-------: | :------: | :-----: | :-----------: |
  > | abc1234  |  홍길동   |    23    | abc1234 |     사과      |
  > |  `null`  |  `null`   |  `null`  | xyz7890 |    바나나     |
  > | qwer5678 |  가나다   |    33    | `null`  |    `null`     |
