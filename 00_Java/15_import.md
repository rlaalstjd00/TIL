## import

- 코드를 작성할 때 다른 패키지의 클래스를 사용하려면 패키지명이 포함된 클래스 이름을 사용해야 한다. 따라서 그러한 불편함을 줄이기 위해 import문을 선언해준다.

  ````java
  package practice;
  
  import practice2.ImportTest;
  
  public class Main {
  	public static void main(String[] args) {
  		ImportTest it = new ImportTest();
  		it.age = 10;
  		it.name = "자바";
  		
  		System.out.println(it.name);		// 자바
  		System.out.println(it.ageUp());		// 11
  	}
  }
  ````

  ````java
  package practice2;
  
  public class ImportTest {
  	public int age;
  	public String name;
  	
  	public int ageUp() {
  		return ++age;
  	}
  }
  ````

  > 위의 코드에서 practice2 패키지에 있는 ImportTest 클래스를 main 메서드가 있는 practice 패키지로 가지고 와서 사용해보자. 따라서 `import practice2.ImportTest;`를 제일 위에 선언해 practice2 의 ImportTest  클래스를 import 시킨다. 그렇게 하면 마치 같은 패키지 안에 있는 클래스 처럼 객체를 만들어 사용할 수 있게 된다. 참고로 practice2 패키지에 있는 모든 클래스를 사용하기 위해서는 `import practice2.*`의 형식으로 import한다.

- static import 문

  static import문을 선언하면 static 멤버를 호출할 때 클래스의 이름을 생략할 수 있다.

  ````java
  package practice;
  
  import static practice2.ImportTest.*;
  
  public class Main {
  	public static void main(String[] args) {
  		age = 10;
  		name = "자바";
  		
  		System.out.println(name);
  		System.out.println(ageUp());
  	}
  }
  ````

  ````java
  package practice2;
  
  public class ImportTest {
  	public static int age;
  	public static String name;
  	
  	public static int ageUp() {
  		return ++age;
  	}
  }
  ````

  > 위의 코드에서 `import static practice2.ImportTest.*` 을 하게 되면 parctice2 패키지의 ImportTest의 모든 static 변수와 메서드를 클래스이름 없이 사용할 수 있다. 