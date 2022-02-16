## String 클래스

#### 1. 문자열의 비교

문자열을 만드는 방법은 문자열 리터럴을 지정하는 것과 String 클래스의 생성자를 사용하는것, 두가지가 있다.

```` java
String str1 = "java";
String str2 = "java";
````

> 위의 코드에서 변수 str1 과 str2에 같은 값인 "java"를 할당했다. 이 때 str1을 할당했을 때 문자열 리터럴 "java"가 생성 되었으므로 str2에 같은 값을 할당할 때 이미 생성되어 있던 리터럴을 재사용하게 된다. 따라서 두 변수가 같은 주소값을 바라보고 있으므로 `str1 == str2` 는 `true`가 된다.

````java
String str3 = new String("java");
String str4 = new String("java");
````

> 이번에는 String 클래스의 생성자를 이용해서 str3 과 str4에 "java"를 할당했다. 이 때 생성자를 이용하게 되면 `new` 연산자에 의해서 메모리 할당이 이루어지기 때문에 항상 새로운 String 객체가 생성된다. 따라서 두 변수는 각각의 생성된 객체의 주소값을 바라보고 있으므로 `str3 == str4`는 `false`가 된다.

하지만 `equals()` 메서드를 사용했을 때는 두 문자열의 내용("java")를 비교하기 때문에 둘 다 `true`가 된다.

#### 2. String 클래스의 여러 메서드

| 메서드                                | 설명                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| char charAt(idx)                      | 지정된 위치(idx)에 있는 문자를 알려준다. (index 0부터)       |
| int compareTo(str)                    | 문자열(str)과 사전순으로 비교한다. 같으면 0, 사전순으로 이전이면 음수, 이후면 양수를 반환한다. |
| String concat(str)                    | 문자열(str)을 뒤에 덧붙인다.                                 |
| boolean contains(s)                   | 지정된 문자열(s)이 있는지 검사한다.                          |
| boolean endsWith(suffix)              | 지정된 문자열(suffix)로 끝나는지 검사한다.                   |
| boolean equals(obj)                   | 문자열(obj)와 문자열을 비교한다.                             |
| boolean equalsIgnoreCase(str)         | 대소문자 관계없이 비교한다.                                  |
| int indexOf(ch, pos)                  | 주어진 문자(ch)가 문자열에 존재하는지 지정위치(pos)부터 확인하여 위치를 알려준다.  (못찾으면 -1을 반환하고, index는 0부터, pos는 생략가능) |
| int indexOf(str)                      | 주어진 문자열(str)이 존재하는지 확인하고 위치를 알려준다. (못찾으면 -1을 반환하고, index는 0부터) |
| int lastIndexOf(str)                  | 지정된 문자(ch)나 문자열(str)을 문자열의 오른쪽 끝에서 부터 찾아서 위치를 알려준다. (못찾으면 -1 반환) |
| int length()                          | 문자열의 길이를 반환한다.                                    |
| String replace(old, nw)               | 문자열중의 문자열이나 문자(old)를 새로운 문자열이나 문자(nw)로 바꾸고, 바뀐 문자열을 반환한다. |
| String replaceAll(regex, replacement) | 문자열중에서 지정된 문자열(regex)와 일치하는 것을 모두 새로운 문자열 (replacement)로 바꾼다. (String replaceFirst는 첫 번째 것만 변경) |
| String[] split(regex)                 | 문자열을 지정된 분리자(regex)로 나누어 문자열 배열에 담아 반환한다. |
| boolean startsWith(prefix)            | 주어진 문자열(prefix)로 시작하는지 검사한다.                 |
| String substring(begin, end)          | 시작위치(begin)부터 끝위치(end)안에 포함된 문자열을 반환한다. (end는 생략가능, 시작위치는 포함되지만 끝위치는 포함 안됨.) |
| String toLowerCase()                  | 문자열을 모두 소문자로 변환하여 반환한다.                    |
| String toUpperCase()                  | 문자열을 모두 대문자로 변환하여 반환한다.                    |
| String toString()                     | String객체에 저장되어 있는 문자열을 반환한다.                |
| String trim()                         | 문자열 양쪽 끝에 있는 공백을 제거하고 반환한다. (가운데 공백은 제거 안함.) |
| static String valueOf(x)              | 지정된 값을 문자열로 변환하여 반환한다. 참조변수의 경우, toString()의 형식으로 반환한다. |
| String join(regex, arr)               | 배열(arr)의 문자열을 지정된 결합자(regex)로 구분해서 결합한다. |
| String format("", x)                  | 형식화된 문자열을 만들어낸다. (printf()와 사용법이 같음)     |

#### 3. 기본형과 String 사이의 형변환.

- 기본형 값을 String으로 변환

  ````java
  int num = 5;						// 5
  String str1 = num + "";				// "5"
  String str2 = String.valueOf(num);	// "5"
  ````

  > 위의 두 방법이 기본형 값을 String으로 변환하는 방법이다. 성능면에서는 valueOf()가 더 좋지만 성능향상이 필요한 경우가 아니면 더 간편하게 빈 문자열을 더해주는 방식이 좋다.

- String을 기본형 값으로 변환

  ````java
  String strNum = "5";					// "5"
  int num1 = Integer.parseInt(strNum);	// 5
  int num2 = Integer.valueOf(strNum);		// 5
  ````

  > 위의 두 방법이 String을 기본형 값으로 변환하는 방법이다.  여기서 `valueOf()`의 반환 타입은 Integer인데 오토박싱이 일어나 int로 자동 형변환 된다. 두 방법 모두 반환 타입만 다른 동일한 메서드이기 때문에 더 익숙한 것을 사용하면 된다.

