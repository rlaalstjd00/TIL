## 자바빈즈 (Java Beans)

#### 자바빈즈

자바 빈즈(자바 객체)란 JSP 표준 액션 태그를 통해 접근할 수 있는 자바 클래스로, 필드변수와 getter, setter, 메서드로 이루어져 있다. 여러 데이터들을 포장해서 가지고 있는 형태로 구성되어 있다.

#### 자바빈즈 개발 규약

1. 패키지화 (default 패키지 인식 불가)
2. 필드 변수 접근자는 private로 설정 (접근은 메서드로만 가능하게 하기 위함)
3. getter, setter 메서드는 반드시 public으로 설정한다.

#### 자바빈즈 태그

- 객체 생성

  <jsp:useBean class="패키지명.클래스명" id="객체명">

- 객체 필드 세팅

  <jsp:setProperty property="필드명" value="세팅값" name="객체명">

- 객체 필드값 접근

  <jsp:getProperty property="필드명" name="객체명">

````html
<!-- beanTest.jsp -->
<!-- ..생략.. -->
<body>
	<form action="beanResult.jsp">
		정수 데이터 <input name="intdata"><br>
		문자열 데이터 <input name="strdata"><br>
		실수 데이터 <input name="doubledata"><br>
		<input type="submit">
	</form>
</body>
````

````java
// test.TestDTO
package test;

public class TestDTO {
	private int intdata;
	private String strdata;
	private double doubledata;
	
	public int getIntdata() {
		return intdata;
	}
	public void setIntdata(int intdata) {
		this.intdata = intdata;
	}
	public String getStrdata() {
		return strdata;
	}
	public void setStrdata(String strdata) {
		this.strdata = strdata;
	}
	public double getDoubledata() {
		return doubledata;
	}
	public void setDoubledata(double doubledata) {
		this.doubledata = doubledata;
	}	
}
````

```` html
<!-- beanResult.jsp -->
<!-- ..생략.. -->
<body>
	<jsp:useBean class="test.TestDTO" id="bean"/>
	<jsp:setProperty property="intdata" name="bean"/>
	<jsp:setProperty property="strdata" name="bean"/>
	<jsp:setProperty property="doubledata" name="bean"/>
	
	<%
		out.println(bean.getIntdata());
		out.println(bean.getStrdata());
		out.println(bean.getDoubledata());
	%>
</body>
````

> beanTest.jsp 에서 intdata, strdata, doubledata를 써서 넘기면 beanResult.jsp에서 받아와 그 값들을 bean이라는 이름을 가진 자바빈즈에 세팅한다. 
>
> 값 세팅시 사용하는 `<jsp:setProperty /> ` 는 외부에서 날아온 파라미터중 같은 name을 가지고 있는 것이 있다면 value 속성을 작성하지 않더라도 값이 자동으로 들어간다. 
>
> 따라서 `out.println`으로 출력해보면 작성한 값이 잘 출력 되는 것을 확인할 수 있다.

