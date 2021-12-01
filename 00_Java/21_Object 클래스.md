## Object 클래스

#### 1. equals(Object obj)

`		equals`란 매개변수로 객체의 참조변수를 받아서 비교하여 그 결과를 `boolean` 타입으로 반환하는 역할을 한다. 여기서 비교를 할 때는 두 객체 참조변수의 주소값으로 판단하기 때문에, 서로 다른 두 객체를 비교하면 항상 `false`를 얻는다.

````java
public class Main{
	public static void main(String[] args) {
		A num1 = new A(10);
		A num2 = new A(10);
		
		if(num1.equals(num2)) {
			System.out.println("num1과 num2는 같다");
		} else {
			System.out.println("num1과 num2는 다르다");			
            // 다르다는 결과가 출력됨
		}
	}
}	

class A {
	int num;

	public A(int num) {
		this.num = num;
	}
}
````

여기서 `equals`를 이용해 두 참조변수에 저장된 값(주소값)이 아닌 그 변수가 가지고 있는 value값을 비교하려면 `equals` 메서드를 오버라이딩 하여 객체에 저장된 내용을 비교하도록 바꾸면 된다.

````java
public class Main{
	public static void main(String[] args) {
		A num1 = new A(10);
		A num2 = new A(10);
		
		if(num1.equals(num2)) {
			System.out.println("num1과 num2는 같다");
			// 같다라는 결과가 출력됨
		} else {
			System.out.println("num1과 num2는 다르다");			
		}	
	}
}	

class A {
	int num;

	public A(int num) {
		this.num = num;
	}
	
	@Override
	public boolean equals(Object obj) {
		if(obj != null && obj instanceof A) {
			return num == ((A)obj).num;
		} else {
			return false;
		}
	}
}
````

> 위의 A 클래스에 오버라이딩된 `equals` 메서드를 보자.  먼저 `if` 문에서 매개변수의 값이 빈 값이 아니고 A의 타입인지 확인한다. 그 확인된 값이 `true`라면 `num == ((A)obj).num` 의 값을 반환해주는데 전역변수에 저장된 num과 매개변수로 넘어온 Object 타입의 num이 같은지 비교하는 것이다. 이 때 비교를 위해 Object 타입인 obj를 A 타입으로 다운캐스팅 시켜준다.

#### 2. toString()

`toString()` 메서드는 객체에 대한 정보를 문자열로 제공할 목적으로 정의한 것이다. `toString()`을 사용하면 사용한 객체의 주소값이 반환되는데, 객체의 정보 문자열로 반환하고 싶으면 `toString()` 메서드를 오버라이딩 해서 사용하면 된다.

````java
public class Main{
	public static void main(String[] args) {
		A a = new A("자바", 3);	
		System.out.println(a.toString());
		// "practice.A@15db9742" 같이 어떠한 주소값이 출력됨	
	}
}	

class A {
	String str;
	int num;
	
	public A(String str, int num) {
		this.str = str;
		this.num = num;
	}
}
````

> `toString()`을 오버라이딩 하지 않았을 때

````java
public class Main{
	public static void main(String[] args) {
		A a = new A("자바", 3);	
		System.out.println(a.toString());
		// "str = 자바, num = 3" 으로 출력됨
	}
}	

class A {
	String str;
	int num;
	
	public A(String str, int num) {
		this.str = str;
		this.num = num;
	}
	
	// toString 재정의
	@Override
	public String toString() {
		return "str = " + str + ", num = " + num;
	}
}
````

> `toString`을 오버라이딩 하면 오버라이딩 한 형식으로 출력된다.

