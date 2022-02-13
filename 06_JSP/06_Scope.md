## 객체 범위 (Scope)

#### 객체 범위의 종류

1. **page 영역**
   - 하나의 JSP 페이지 내에서만 객체를 공유하는 영역이다.
     - JSP에 내장된 pageContext 객체는 page 영역에서만 유효하다.
     - JSP 파일에 스크립틀릿 태그 내부에 변수를 선언하면, 이 변수는 page 스코프에 정의되기 때문에 해당 JSP 파일 내에서만 유효하다.
2. **request 영역**
   - 요청을 받아서 응답하기까지 객체가 유효한 영역이다.
     - 서블릿에서 `request.setAttribute()` 를 통해 전달하고,
     - JSP에서는 `request.getAttribute()`로 받는다.
3. **session 영역**
   - 하나의 브라우저당 하나의 session 객체가 생성되므로, 같은 브라우저 내에서 요청되는 페이지들은 같은 객체를 공유하는데, 이를 세션 영역이라고 한다.
     - `request.getSession()` 를 통해 세션 영역의 객체를 얻을 수 있다.
   - 세션이 종료되면 객체는 반환된다.
4. **application 영역**
   - 하나의 어플리케이션당 하나의 application 객체가 생성되므로, 같은 어플리케이션 내에서 요청되는 페이지들은 같은 객체를 공유하는데, 이를 어플리케이션 영역이라고 한다.
     - `request.getServletContext()` 를 통해 어플리케이션 영역의 객체를 얻을 수 있다.
   - 어플리케이션이 종료되면 객체는 반환된다.

따라서 scope의 범위는 page < request < session < application 순서이다.