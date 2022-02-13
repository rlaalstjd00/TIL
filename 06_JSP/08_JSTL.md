## JSTL (Jsp Standard Tag Library)

연산이나 조건문, 반복문을 편하게 처리할 수 있으며, JSP 페이지 내에서 자바코드를 사용하지 않고 로직을 구현할 수 있는 효과적인 방법을 제공한다.

라이브러리를 사용하기 위해 페이지 상단에 `<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>` 를 작성한다

#### JSTL core 태그

- 변수 세팅 : `<c:set var="key값(변수명)" value="세팅할 값" scope="세팅할 위치"/>`
- 변수 출력 : `<c:set out value="${변수명}"/>`
- if문 : `<c:if test="${조건식}">   </c:if>`
- switch문 : `<c:choose>   </c:choose>`
  - case : `<c:when test="${조건식}">   </c:when>`
  - default : `<c:otherwise>   </c:otherwise>`
- 반복문 : `<c:forEach>   </c:forEach>`

#### JSTL 변수

````jsp
<!-- ..생략.. -->
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<body>
    <!-- 변수 세팅 pageContext.setAttribute("userid","id1234"); 와 같음 -->
    <c:set var="userid" value="id1234"/>
    <!-- 아이디 : id1234 출력. ${userid}와 같음 -->
    아이디 : <c:out value="${userid}"/>
    
    <!--
		value 값은 태그 사이에 넣어서 쓰는것도 가능
		scope가 session 이므로 pageContext와 다르게 명시적으로 써줘야함
	-->
    <c:set var="userid" scope="session">id0000</c:set>
    <!-- 세션 아이디 : id0000 출력. 접근시에도 sessioniScope.userid 로 접근해줘야 함 -->
   	세션 아이디 : ${sessionScope.userid}
</body>
````

#### JSTL 조건문

````jsp
<!-- ..생략.. -->
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<body>
    <c:set var="num" value="30"/>
    
    <!-- if문 -->
    <c:if test="${num>50}">
    	이 수는 50보다 큰 수입니다.
    </c:if>
    
    <!-- choose문 (if~else문) -->
    <c:choose>
    	<c:when test="${num>50}">
        	이 수는 50보다 큰 수입니다.
        </c:when>
        <c:when test="${num>30}">
        	이 수는 30보다 크코 50보다 작거나 같습니다.
        </c:when>
        <c:when test="${num>10}">
        	이 수는 10보다 크고 30보다 작거나 같습니다.
        </c:when>
        <c:otherwise>
        	이 수는 10보다 작거나 같습니다.
        </c:otherwise>
    </c:choose>
</body>
````

#### JSTL 반복문

````jsp
<!-- ..생략.. -->
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<body>
   	<c:set var="arr" value="<%=new int[]{10,20,30,40,50}%>"/>
    
    <!-- for(int i=0; i<4; i) -->
    <c:forEach var="i" begin="0" end="4" step="1">
    	${arr[i]}
    </c:forEach>
    
    <!-- for(int data : arr) -->
    <c:forEach var="data" items="${arr}">
    	${data}
    </c:forEach>
</body>
````

