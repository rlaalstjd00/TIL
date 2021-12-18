## 날짜 함수

1. SYSDATE : 서버의 현재 시간을 반환하는 함수

   ````sql
   SELECT SYSDATE FROM DUAL;
   ````

   > 서버의 현재 시간을 2021/12/18 14:09:24 같은 형식으로 반환한다.

2. MONTHS_BETWEEN : 두 날짜 사이의 개월수를 반환하는 함수

   ````sql
   SELECT MONTHS_BETWEEN(TO_DATE('20211218','YYYYMMDD'),TO_DATE('20211118','YYYYMMDD')) FROM DUAL;
   ````

   > 2021년 12월 18일과 2021년 11월 18일의 개월 차이인 1을 반환한다.

3. ADD_MONTHS : 개월수를 더하거나 빼는 함수

   ````sql
   SELECT ADD_MONTHS(TO_DATE('20211218','YYYYMMDD'),1) FROM DUAL;
   SELECT ADD_MONTHS(TO_DATE('20211218','YYYYMMDD'),-1) FROM DUAL;
   ````

   > 첫 번째 코드는 2021년 12월 18일부터 한달 뒤인 2022년 1월 18일을 반환한다.
   >
   > 두 번째 코드는 2021년 12월 18일부터 한달 전인 2021년 11월 18일을 반환한다.
   >
   > 이전달이나 다음달에 기준날짜의 일자가 존재하지 않으면 해당 월의 마지막 일자가 리턴된다. 예를 들어, 2021년 3월 31일의 이전달은 2021 2월 28일이 된다.

4. NEXT_DAY : 입력한 날짜를 기준으로 찾고자 하는 요일의 첫 번째 일자를 반환하는 함수

   ```` sql
   SELECT NEXT_DAY(SYSDATE,'일요일') FROM DUAL;
   SELECT NEXT_DAY(SYSDATE-8, '일요일') FROM DUAL;
   ````

   > 첫 번째 코드는 현재 서버 날짜기준 다음 일요일의 날짜를 반환한다.
   >
   > 두 번째 코드는 현재 서버 날짜에서 8일을 빼준 날짜의 다음 일요일을 반환한다. 즉, 현재 서버 날짜 기준 이전 일요일을 반환한다.
   >
   > `1`, `일요일`, `일`, `SUNDAY`, `SUN` 같은 형식으로 찾고자 하는 요일을 쓸 수 있다.

5. LAST_DAY :  기준 날짜의 마지막일을 반환하는 함수

   ````sql
   SELECT LAST_DAY(SYSDATE) FROM DUAL;
   ````

   > 현재 서버 날짜가 포함된 월의 마지막 날짜를 반환한다. 현재 서버 날짜가 2021년 12월 18일이라면 12월의 마지막날인 2021년 12월 31일이 반환된다.

6. ROUND  : 주어진 날짜를 반올림해 반환하는 함수

   ```` sql
   SELECT ROUND(SYSDATE) FROM DUAL;
   ````

   > ROUND 함수는 숫자 뿐만 아니라 날짜에도 사용가능하다.
   >
   > 현재 서버 날짜가 2021년 12월 18일 22시 28분 22초라면 2021년 12월 19일 00시 00분 00초를 반환한다.

## 형변환 함수

1. TO_CHAR : 문자로 형변환

   ````sql
   SELECT TO_CHAR(SYSDATE, 'YYYYMMDD') FROM DUAL;
   ````

   > 서버의 현재 날짜를 YYYYMMDD 형식의 문자열로 형변환해 반환한다.

2. TO_DATE : 날짜로 형변환

   ```` sql
   SELECT TO_DATE('20211218','YYYYMMDD') FROM DUAL;
   ````

   > '20211218'이라는 문자열을 YYYYMMDD 형식의 날짜로 형변환해 반환한다.

3. TO_NUMBER : 숫자로 형변환

   ````sql
   SELECT TO_NUMBER('123456') FROM DUAL;
   ````

   > '123456' 이라는 문자열을 123456이라는 숫자로 형변환해 반환한다.

#### 날짜 포멧

- Y : 연
- M : 월
- D : 일
- HH24 : 24 표기법 시
- MI : 분
- SS : 초

## NULL 처리 함수

1. NVL : 값이 null인 경우 지정한 값을 출력하는 함수

   ````sql
   SELECT NVL(USER_NAME,'이름없음') FROM USER1;
   ````

   > USER_NAME 값을 가져오되, null이라면 '이름없음'을 반환한다.

2. NVL2 : 값이 null이 아닌 경우 지정값1을 출력하고 null인 경우 지정값2를 출력하는 함수

   ````sql
   SELECT NVL2(USER_NAME,'Y','N') FROM USER1;
   ````

   > USER_NAME이 있으면 'Y', 없으면 'N'을 반환한다.