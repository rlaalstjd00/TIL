## JSP의 태그

#### 주석

JSP 파일에서는 HTML 주석과 JSP 주석을 모두 사용할 수 있다.

- HTML 주석 : `<!--   -->` 내부의 코드도 모두 컴파일이 된 후 페이지에서 감춰진다.
- JSP 주석 : `<%-- --%>` 내부의 코드가 모두 무시된 채 컴파일된다.

따라서 특별한 이유가 없다면 JSP 주석 사용을 권장한다.

#### 스크립트 태그

HTML 내부에 자바 코드를 넣어 프로그래밍이 가능하도록 만들 수 있다.

1. 선언문(declaration)

   자바의 변수나 메서드를 정의하는데 사용되는 태그로 `<%!   %>` 형태로 사용한다.

   ````jsp
   <%@ page language="java" contentType="text/html; charset=UTF-8"
       pageEncoding="UTF-8"%>
   <!DOCTYPE html>
   <html>
   <head>
   <meta charset="UTF-8">
   <title>scriptTag1</title>
   </head>
   <body>
   	<h2>script tag 1</h2>
   	<%!
   		// 내부는 전부 자바의 문법
   		// 여기서 선언되는 count는 전역변수
   		int count = 3;
   		String sayHello(String data){
   			return "Hello " + data;
   		}
   	%>
   </body>
   </html>
   ````

   > 위의 코드는 HTML 문서지만  선언문 태그를 사용해 내부에 자바 문법으로 변수와 메서드를 선언할 수 있다. 선언문에서 선언된 변수는 전역변수로 사용된다.

2. 스크립틀릿(scriptlet)

   자바의 변수 선언 및 자바 로직 코드를 작성하는데 사용되는 태그로 `<%   %>` 형태로 사용한다.

   ````jsp
   <!-- ..생략.. -->
   <body>
   	<h2>script tag 1</h2>
   	<%
   		for(int i=1; i<=3; i++){
   			out.println(i+". Java Server Pages<br>");
   		}
   	%>
       <!--
   		1. Java Server Pages
   		2. Java Server Pages
   		3. Java Server Pages
   	-->
   </body>
   ````

   > 위의 코드는 스크립틀릿 태그를 이용해 HTML 문서 내부에서 자바 코드를 사용하는 것이다.

3. 표현문(expression)

   변수, 계산식, 메서드 호출의 리턴값 등을 표현해주는 태그로 `<%=   %>` 형태로 사용한다.

   내부에 작성한 값이 HTML 문서에 그대로 표현되며 타입은 문자열이다.

   ````jsp
   <!-- .. 생략 .. -->
   <body>
   	<h2>script tag 1</h2>
   	<%!
   		int count = 3;
   		String sayHello(String data){
   			return "Hello " + data;
   		}
   	%>
   	
   	sayHello("JSP")의 결과 : <%= sayHello("JSP") %>
       <!-- sayHello("JSP")의 결과 : Hello JSP -->
   </body>
   ````

   > 위의 선언문 태그에서 선언한 sayHello 메서드를 사용하기 위해 표현문 태그를 사용한다.
   >
   > `<%= sayHello("JSP")%>` 은 `"Hello JSP"` 로 출력이 될것이며, 표현문 태그는 `out.println(sayHello("JSP"));` 을 출력하는것과 같다고 생각하면 된다.
   >
   > 표현문 태그 사용시 세미콜론(;)은 쓰지 않는다는 것을 주의하자.

#### 디렉티브 태그

`<%@ page   %>` 의 형태이며, 현재 JSP 페이지에 대한 정보를 설정하는 태그이다. 되도록 페이지 최상단에 작성한다.

속성명 (import 속성을 제외하고 한번씩만 사용 가능하다.)

1. language : 사용할 프로그래밍 언어 (기본값 : java)
2. contentType : 생성할 문서의 콘텐츠 유형 (기본값 : text/html)
3. pageEncoding : 인코딩 설정 (기본값 : ISO-8859-1)
4. import : 사용할 자바 클래스 추가
5. session : 세션 사용 여부 설정 (기본값 : true)
6. info : 페이지에 대한 설명 작성 (주석처럼 이용)
7. errorPage : 예외 발생시 이동할 페이지 설정
8. isErrorPage : 오류 페이지로 설정할지에 대한 여부 (기본값 : false)

#### include 디렉티브 태그

`<%@ include file="파일명" %>` 

현재 JSP 페이지의 특정 영역에 외부 파일의 내용을 포함시키는 태그이다. 보통 대부분의 페이지에서 동일한 header와 footer를 외부 파일로 만든 후 include 하여 사용한다. 이를 통해 반복작업을 줄이고 유지보수가 용이해진다.

#### 액션태그

서버나 클라이언트에게 어떤 행동을 하도록 명령하는 태그

페이지나 페이지 사이를 제어하거나 다른 페이지의 실행 결과 내용을 현재 페이지에 포함시키거나 자바빈즈 등의 다양한 기능을 제공한다. 액션태그는 XML 형식인 `<jsp:   />` 을 이용한다.

1. `<jsp: forward/>` : 다른 페이지로 이동, 페이지의 흐름을 제어하기 위한 역할
2. `<jsp: param/>` : 현재 페이지에서 다른 페이지에 값을 전달하기 위한 역할
3. `<jsp: useBean/>` : 객체 생성을 위한 역할
4. `<jsp: setProperty/>` : 객체의 필드 세팅을 위한 역할
5. `<jsp: getProperty/>` : 객체의 필드값 접근을 위한 역할