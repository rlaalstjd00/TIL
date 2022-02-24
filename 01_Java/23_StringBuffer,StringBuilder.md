## StringBuffer 클래스와 StringBuilder 클래스

StringBuffer 클래스는 String 클래스와 다르게 객체를 생성할 때, 지정된 문자열을 변경할 수 있다.

StringBuffer  객체가 생성될 때, char형 배열이 생성되며 이 때 생성된 배열을 value 라는 변수가 참조하게 된다.

#### StringBuffer의 생성자

StringBuffer의 객체를 생성할 때는 생성자를 사용해 문자열의 길이를 충분히 고려해 여유있는 크기로 지정하는 것이 좋다.
버퍼의 크기가 부족할 때는 내부적으로 더 긴 배열을 새로 만들어 기존의 값을 복사해야하기 때문이다.

> 버퍼의 크기를 지정하지 않으면 16개의 문자를 저장할 수 있는 크기 생성

````java
public StringBuffer(intlength){
    value = new char[length];
    shared = false;
}

public StringBuffer(){
    this(16);
}

public StringBuffer(String str){
    this(str.length() + 16);
    append(str);
}
````

> 위의 코드는 StringBuffer 클래스 구현부분의 일부분이다.
>
> 아무것도 안넘겨주면 버퍼의 크기가 16으로 설정되는 것을 볼 수 있다.
>
> 그리고 지정된 문자열의 길이보다 16 더 크게 버퍼를 생성하는것도 확인할 수 있다.

#### StringBuffer의 변경

문자열을 추가하는 `append()` 라는 메서드를 사용해서 StringBuffer를 변경한다고 생각해보자. `append()` 메서드는 반환타입이 StringBuffer으로, 자신의 주소를 반환한다.

````java
StringBuffer sb = new StringBuffer("aaa");
sb.append("123").append("bbb");
````

> 위의 코드에서 `sb.append("123")`이 "aaa123" 이라는 문자열을 담고있는 sb 자신의 주소값을 반환하기 때문에 뒤에 `.append("bbb")` 를 연속적으로 호출할 수 있다.

StringBuffer 클래스는 위의 `append()` 처럼 객체 자신을 반환하는 메서드들이 있으며 아래의 메서드 파트에서 알아보자.

#### StringBuffer의 비교

앞서 String 클래스의 비교에서는 `equals` 를 오버라이딩 해 문자열의 내용을 비교하도록 구현되어 있다고 했다.

그러나 StringBuffer 클래스는 `equals` 메서드는 오버라이딩하지 않기 때문에 오버라이딩 되어있는 `toString` 메서드를 이용해 비교해야 한다.

````java
StringBuffer sb1 = new StringBuffer("abc");
StringBuffer sb2 = new StringBuffer("abc");

System.out.println(sb1 == sb2);	// false
System.out.println(sb1.equals(sb2));	// false

// sb들을 문자열인 s로 변환해서 비교한다
String s1 sb1.toString();
String s2 sb2.toString();

System.out.println(s1.equals(s2));	// true
    
````

#### StringBuffer 클래스의 메서드

|         메서드         |                             설명                             |
| :--------------------: | :----------------------------------------------------------: |
|        append()        | 매개변수로 입력된 값을 문자열로 변환하여 StringBuffer 객체의 문자열 뒤에 덧붙인다. (반환타입 StringBuffer) |
|       capacity()       |          StringBuffer 객체의 버퍼 크기를 알려준다.           |
|        length()        |            버퍼에 담긴 문자열의 길이를 알려준다.             |
|        charAt()        |     매개변수로 넘겨준 index 위치에 있는 문자를 반환한다.     |
|   delete(start,end)    |       start 이상 end 미만 위치에 있는 문자를 제거한다.       |
|     deleteCharAt()     |     매개변수로 넘겨준 index 위치에있는 문자를 제거한다.      |
|     insert(pos, ?)     | ? 를 문자열로 변환해 pos 위치에 추가한다. (pos는 0부터 시작) |
| replace(start,end,str) | start 이상 end 미만 위치의 문자들을 주어진 문자열로 바꾼다.  |
|       reverse()        |        버퍼에 저장된 문자열의 순서를 거꾸로 나열한다.        |
|   setCharAt(idx,ch)    |        지정된 위치의 문자를 주어진 문자(ch)로 바꾼다.        |
|      setLength()       | 버퍼에 저장된 문자열의 길이를 매개변수로 넘겨준 길이로 변경한다. 길이를 늘릴때는 빈공간을 널문자로 채운다. |
|       toString()       |         버퍼에 저장된 문자열을 String으로 변환한다.          |
|  substring(start,end)  | start 이상 end 미만 위치의 문자열을 String 타입으로 뽑아서 반환한다. end는 생략 가능하며 생략시 끝까지 뽑아서 반환한다. |



#### StringBuilder

StringBuffer는 멀티쓰레드에 안전하도록 동기화 되어있다. 하지만 멀티쓰레드로 작성된 프로그램이 아닌 경우, 성능의 저하만 유발한다.

따라서 StringBuffer에서 동기화만 뺀 것이 StringBuilder이다. 이러한 차이만 있을 뿐, 나머지 사용법 및 기능은 모두 같다.
