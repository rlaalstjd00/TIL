## 래퍼(wrapper) 클래스

프로그래밍을 하다보면 기본 자료형을 어쩔 수 없이 객체로 다뤄야 하는 경우가 있다. 이 때 사용되는 것이 래퍼 클래스이며 기본형을 대표하는 8개의 래퍼 클래스가 있다.

> 자바는 8개의 기본 자료형을 객체로 다루지 않는데, 이는 객체지향 언어에 반하는 것이지만 보다 높은 성능을 얻을 수 있다.

#### 기본 자료형과 래퍼클래스

| 기본형  | 래퍼클래스 |
| :-----: | :--------: |
| boolean |  Boolean   |
|  char   | Character  |
|  byte   |    Byte    |
|  short  |   Short    |
|   int   |  Integer   |
|  long   |    Long    |
|  float  |   Float    |
| double  |   Double   |

> 대부분은 앞글자만 대문자로 바꾸면 되지만 `Character` 과 `Integer` 는 다름을 주의하자.

#### 문자열을 숫자로 변환

문자열을 숫자로 변환하는 방법은 여러가지가 있는데 대표적으로 아래 세 가지가 있다.

````java
int i1 = new Integer("10").intValue();
int i2 = Integer.parseInt("10");
Integer i3 = Integer.valueOf("10");
````

> 모두 문자열 "10"을 숫자 10으로 바꿔주는 것이고, 두번째 방법인 `Integer.parseInt()` 를 주로 사용한다.

#### 오토박싱 & 언박싱

**오토박싱 :** 컴파일러가 자동으로 기본형 값을 래퍼 클래스의 객체로 변환해주는 것.

**언박싱 :** 오토박싱의 반대과정, 자동으로 래퍼 클래스의 객체를 기본형 값으로 변환해주는 것.

````java
int a = 5;
Integer b = new Integer(4);

int sum = a + b;	// 9
// 컴파일 후의 코드 : a + b.intValue();
````

> 위의 코드를 보자. `int` 타입인 a와 `Integer` 타입인 b를 더하는 연산을 했는 오류가 발생하지 않는다.
>
> 이는 컴파일 단계에서 컴파일러가 자동으로 `Integer` 객체를 `int`타입의 값으로 변환하는 `intValue()` 를 추가해주기 때문인데 이를 언박싱이라고 한다.

````java
ArrayList<Integer> list = new ArrayList<Integer>();

list.add(10);	// 오토박싱
int value = list.get(0);	// 언박싱
````

> `list.add(10) ` 에서는 `Integer` 타입의 배열에 기본형인 10을 넣었는데 잘 들어간다. 이는 오토박싱이 일어나 `int` 타입의 10이 `Integer` 타입으로 변환되기 때문이다.
>
> 그리고 `int value = list.get(0)` 에서 `int` 타입인 value 변수에 `Integer` 타입인 list의 0번째 값 10을 대입했다. 이 때 자동으로 언박싱이 일어나 잘 들어가는 것을 볼 수 있다.

