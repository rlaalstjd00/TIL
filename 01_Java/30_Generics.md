## 제네릭 (Generics)

제네릭이란 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입체크를 해주는 기능이다.

제네릭 클래스의 장점

- 타입 안정성을 제공한다.
- 타입체크와 형변환을 생략할 수 있으므로 코드가 간결해진다.

#### 제네릭 클래스의 선언

제네릭 타입은 클래스와 메서드에 선언할 수 있다.

- 클래스에 선언

  ````java
  class A<T>{
      T data;
      
      void setData(T data){
          this.data = data;
      }
      
      T getData(){
          return data;
      }
  }
  ````

  > 위에서의 T는 타입 변수라고 하며, Type의 첫 글자에서 따온 것이다. 단순히 미지의 값이라는 표현이므로 다른 것을 사용해도 된다. 타입 변수가 여러개 일때는 Map<K,V>와 같이 콤마를 구분자로 나열한다.

  ````java
  A<String> a = new A<String>();	
  
  a.setData("abcd");
  String data1 = a.getData();
  ````

  > 위의 코드는 앞서 선언된 제네릭 클래스를 사용하는 코드이다.
  >
  > `A<String> a = new A<String>();` 과 같이 사용할 때는 실제 타입을 지정해줘야 한다.
  >
  > `String` 타입으로 지정했으므로, `setData()` 도 문자열만 넣을 수 있고, `getData()` 시에도 별도의 형변환 없이 `String` 타입의 변수에 대입할 수 있다.

#### 제네릭의 제한

- `static` 멤버는 타입의 종류에 관계없이 동일한 것이어야 하기 때문에, 제네릭 클래스에 존재할 수 없다.

- 제네릭 타입의 배열을 생성할 수 없다. -> `new` 연산자로 배열을 생성할 때는 컴파일 시점에 타입 T가 뭔지 정확히 알아야 하는데, 제네릭 타입에선 알 수 없기 때문이다.

  ````java
  class A<T>{
      // static T data; -> 에러
      T[] itemArr;
      
      // T[] toArray(){
      // 		T[] arr = new T[itemArr.length]; -> 에러
  	// }
  }
  ````

제네릭 타입에 `extends` 키워드를 사용하면 특정 타입의 자손들만 담을 수 있게 제한할 수 있다.

````java
class A<T extends Fruit>{
    ArrayList<T> list = new ArrayList<T>();
}
````

> 위의 코드에서 제네릭을 `<T extends Fruit>` 이라고 했는데. 이는 `Fruit` 클래스와 그 자손들만 대입이 가능하다.
>
> 예를 들어 `Apple`, `Banana` 클래스가 `Fruit` 클래스를 상속받고 있다면, 이러한 타입들만 저장할 수 있는 것이다.

#### 와일드 카드

- `<? extends T>` : 와일드 카드의 상한 제한, T와 그 자손들만 가능
- `<? super T>` : 와일드 카드의 하한 제한, T와 그 조상들만 가능
- `<?>` : 제한 없음. 모든 타입이 가능. `<? extends Object>` 와 동일

