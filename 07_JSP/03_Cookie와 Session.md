## Cookie와 Session

#### JSP 내장객체

객체화 없이 사용할 수 있는 객체이며, jsp 파일이 서블릿으로 변환될 때 웹 컨테이너가 자동으로 메모리에 할당해서 제공한다.

- request : 웹 브라우저의 요청 정보를 저장
- response : 웹 브라우저 요청에 대한 응답 정보를 저장
- out : JSP 페이지 body에 출력할 내용 정보를 저장
- session : 하나의 웹 브라우저의 정보를 유지하기 위한 세션 정보를 저장
- pageContext : JSP 페이지에 대한 정보를 저장
- config : JSP 페이지에 대한 설정 정보를 저장
- exception : JSP 페이지에서 예외가 발생한 경우 사용되는 객체

#### 쿠키 (Cookie)

웹 브라우저가 보관하고 있는 데이터로, 웹 서버에 요청을 보낼 때 쿠키를 헤더에 담아서 전송한다.

- **쿠키 생성** 
  - Cookie 객체명 = new Cookie("key", "value");

- **쿠키 저장** : 사용자 컴퓨터에 저장해야 하므로 응답을 통해서 생성한 쿠키를 보내줘야 한다.

  - response.addCookie(쿠키객체);

- **쿠키 사용** : 사용자가 요청할 때 함께 보내주는 헤더에서 쿠키를 꺼내 사용한다

  - request.getHeader("Cookie") : 헤더중에 Cookie라는 이름의 헤더가 있는지 확인 (null이라면 전송된 쿠키가 없다는 뜻)
  - request.getCookies() : 전송된 쿠키 객체들의 배열
  - 쿠키객체.getName() : 쿠키 이름(key 값)
  - 쿠키객체.getValue() : 쿠키값(value 값)

- **쿠키 삭제** : 쿠키의 유효기간을 설정해주는 방식으로 삭제할 수 있다.

  - 쿠키객체.setMaxAge(n) : n초만큼 유지하다가 쿠키 삭제하도록 설정

  > 쿠키를 수정하거나 삭제시 설정된 쿠키객체를 다시 response를 통해 사용자 컴퓨터에 추가해줘야 한다. 쿠키는 사용자의 컴퓨터에 저장되는 것이므로 서버에서 수정된 쿠키를 사용자의 컴퓨터의 쿠키에 덮어씌우기 위함.

- **쿠키사용 장단점** 

  - 장점 
    - 클라이언트의 일정 폴더에 정보를 저장하기 때문에 서버의 부하를 줄일 수 있다.
  - 단점
    - 클라이언트 컴퓨터에 데이터가 저장되기 때문에 보안의 위협을 받을 수 있다. (보안상 위험이 있는 정보는 쿠키에 담지 않는다.)
    - 데이터 저장 용량의 한계가 있다.
    - 브라우저 내 기능인 "쿠키차단"을 사용하면 무용지물이 된다.

  ````jsp
  <!-- setCookie.jsp -->
  <!-- ..생략.. -->
  <body>
      <%
         Cookie cookie = new Cookie("key1","value1");
         Cookie cookie2 = new Cookie("key2", "value2");
         response.addCookie(cookie);
         response.addCookie(cookie2)
      %>
      <a herf="getCookie.jsp">쿠키 확인하기</a>
  </body>
  ````

  ````jsp
  <!-- getCookie.jsp -->
  <!-- ..생략.. -->
  <body>
      <%
      	String check = request.getHeader("Cookie");
      	if(check != null){
              Cookie[] cookies = request.getCookies();
              for(Cookie cookie : cookies){
                  out.println(cookie.getName()+" : ");
                  out.println(cookie.getValue()+"<br>");
                  
                  // key1 쿠키 수정
                  if(cookie.getName().equals("key1")){
                      cookie.setValue("value99");
                      // response.addCookie를 이용해 사용자 컴퓨터에 덮어쓰기 한다.
                      response.addCookie(cookie);
                  }
              }
          }
      %>
      <a href="checkUpdateCookie.jsp">수정된 쿠키 확인하기</a>
  </body>
  ````

  ````jsp
  <!-- checkUpdateCookie.jsp -->
  <!-- 생략 -->
  <body>
      <%
      	String check = request.getHeader("Cookie");
      	if(check != null){
              Cookie[] cookies = request.getCookies();
              
              for(Cookie cookie : cookies){
                  out.println(cookie.getName()+" : ");
                  out.println(cookie.getValue()+"<br>");
                  
                  // key2 쿠키 삭제
                  if(cookie.getName().equals("key2")){
                      // 쿠키 0초 유지 (삭제)
                      cookie.setMaxAge(0);
                      response.addCookie(cookie);
                  }
              }
          }
      %>
      <a href="getCookie.jsp">쿠키 삭제 확인하기</a>
  </body>
  ````

  > 위의 코드의 흐름을 보자.
  >
  > 1. setCookie.jsp 에서 key1 쿠키와 key2 쿠키를 생성한다. 버튼 누르면 getCookie.jsp로 이동
  >
  > 2. getCookie.jsp 에서 for문을 이용해 받아온 쿠키배열을 출력한다. 
  >
  >    [(JSESSIONID, ..생략..), (key1, value1), (key2, value2)]
  >
  >    그리고 key1 쿠키의 value 값을 "vlaue99" 로 수정한다. 버튼 누르면 checkUpdateCookie.jsp로 이동
  >
  > 3. checkUpdateCookie.jsp 에서 for문을 이용해 받아온 쿠키 배열을 출력한다. 
  >
  >    [(JSESSIONID, ..생략..), (key1, value99), (key2, value2)]
  >
  >    그리고 key2 쿠키를 삭제한다. 버튼 누르면 다시 getCookie.jsp로 이동
  >
  > 4. getCookie.jsp 에서 for문을 이용해 받아온 쿠키 배열을 출력한다.
  >
  >    [(JSESSIONID, ..생략..), (key1, value99)]
  >
  > 이 때 JSESSIONID 쿠키는 톰캣 서버에서 상태저장을 위해 생성하는 쿠키로, 신경쓰지 말자.

#### 세션 (Session)

내장객체로서 브라우저마다 한개씩 존재하고, 고유한 SessionID 생성 후 정보를 추출한다.

- 세션 사용의 장단점
  - 장점
    - JSP에서만 접근할 수 있기 때문에 보안성이 좋다.
    - 저장용량의 한계가 거의 없다.
  - 단점
    - 서버에 데이터를 저장하므로 부하에 걸릴 수 있다.

