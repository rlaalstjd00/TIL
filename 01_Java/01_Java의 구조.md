## 자바의 구조



- 자바에서 모든 코드는 관련 코드를을 그룹화한 형태로 클래스 안에 존재해야 한다.
- 이러한 클래스들이 모여 자바 어플리케이션을 이룬다.
- 자바 어플리케이션 안에는 main 메서드가 반드시 하나 존재해야 하고, 이 main 메서드는 Java 어플리케이션의 시작점이다.

```java
class JavaEx {										// JavaEx 클래스
    public static void main(String[] args){			// main 메서드 선언
        System.out.println("자바 예제 입니다.");		// 실행할 문장을 메인메서드 안에 적음
    }
}
```

- 하나의 소스파일에 보통 하나의 클래스만을 정의하고, 소스파일의 이름은 public class의 이름과 일치해야 한다. 
- 하나의 소스파일에 둘 이상의 public class가 존재하면 안된다.

```java
public class JavaEx{}		// 하나의 public class만 존재함. 이때 소스파일의 이름은 JavaEx.java 
class JavaProj{}						
```

