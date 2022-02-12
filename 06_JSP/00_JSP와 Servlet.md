## JSP (Java Server Page)

JSP란 HTML을 중심으로 자바와 같이 연동하여 사용하는 웹 언어로, HTML 코드 안에 JAVA 코드를 작성할 수 있도록 도와준다.

## 서블릿 (Servlet)

JAVA 코드 안에서 HTML 문서를 작성할 수 있는 JAVA 프로그램이다.

- 클라이언트의 요청에 응답하는 역할의 자바 프로그램으로, 간단히 말해서 자바를 사용해 웹을 만들기 위한 기술이다.
- 일반적인 웹 페이지는 정적인 페이지만을 제공하는데, 동적인 페이지를 만들기 위해서 웹서버는 다른 곳에 도움을 요청해 동적인 페이지를 작성해야 한다. 이 때 도움을 주는 어플리케이션이 서블릿인 것이다.

#### 서블릿 동작 방식

1. 사용자가 URL 요청
2. 서블릿 컨테이너가 HttpServletRequest, HttpServletResponse 객체 생성
3. web.xml에 매핑해놓은 서블릿 찾기
4. 해당하는 서블릿의 클래스로 요청 전송
5. Thread에 의해 `service()` 호출
6. 요청 방식에 따라 `doGet()` 혹은 `doPost()` 호출
7. 처리 및 HttpServletRequest, HttpServletResponse 객체 소멸

이 때 서블릿 규칙은 꽤 복잡하기 때문에 JSP를 사용하는데, JSP를 사용해도 내부적으로는 WAS(Web Application Server)에 의해 서블릿으로 변환되어 실행된다.

