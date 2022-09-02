## Comparable과 Comparator

`Comparable`과 `Comparator` 의 차이점과 사용 방법에 대해 알아보자. 이들은 **객체의 비교**를 위해 사용되며, 나아가 비교의 응용인 정렬같은 곳에서도 사용할 수 있다.

기본 자료형은 부등호를 사용해 비교할 수 있지만, 직접 클래스를 만들어 생성된 객체는 단순 부등호를 사용해 비교하기에는 무리가 있기 때문에 `Comparable` 과 `Comparator` 을 사용하는 것이다.

```java
public class Main {
    public static void main(String[] args) {
        User userA = new User(100, 25);
        User userB = new User(101, 23);
    }
}

class User{
    int userNum;
    int age;

    public User(int userNum, int age) {
        this.userNum = userNum;
        this.age = age;
    }
}
```

예를 들어 위의 코드에서 `User` 라는 클래스를 통해 만든 객체인 `UserA`와 `UserB` 를 비교한다고 가정해보자. 이 때 `userNum`과 `age`중 어떤 값으로 비교해야 할까? 이렇게 부등호로 비교하기 애매한 객체의 비교를 위해 사용하는 것이다.

들어가기 앞서, 이 둘은 모두 인터페이스로 내부에 선언된 메서드를 구현해서 써야한다는 점을 짚고 넘어가자.

<br>

---

### Comparable

`Comparable` 을 사용하려면 `compareTo(T o)` 메서드를 재정의 해야한다. `compareTo(T o)` 메서드는 파라미터가 하나만 넘어오는데, 그럼 이 파라미터와 무엇을 비교하는 것일까? 

바로 자기 자신이다. 코드로 보는 것이 이해가 빠르니, 아래의 코드를 살펴보자.

```java
public class Main {
    public static void main(String[] args) {
        User userA = new User(100, 25);
        User userB = new User(101, 23);
        User userC = new User(102, 25);
        int isBig = userA.compareTo(userB);
        int isBig2 = userA.compareTo(userC);

        System.out.println("A, B 비교 : " + isBig);   // 1
        System.out.println("A, C 비교 : " + isBig2);  // -1
    }
}

class User implements Comparable<User> {
    int userNum;
    int age;

    public User(int userNum, int age) {
        this.userNum = userNum;
        this.age = age;
    }

    @Override
    public int compareTo(User o) {
        if (this.age > o.age) {
            return 1;
        } else if (this.age < o.age) {
            return -1;
        } else {
          	// userNum 은 중복이 없다고 가정
            if (this.userNum > o.userNum) {  	
                return 1;
            } else {
                return -1;
            }
        }
    }
}
```

아래의 `User` 클래스에서 `Comparable` 인터페이스를 상속받아 `compareTo()` 메서드를 재정의했다. 

재정의한 부분을 살펴보면 먼저 자기 자신의 나이 `this.age`와 파라미터로 들어온 객체의 나이 `o.age`로 먼저 비교를 한 후, 나이가 같으면 `userNum`으로 비교를 한다. 자신의 값이 크면 1을, 작으면 -1을 반환하게 된다.

`compareTo()` 메서드는 정수를 반환하는데, 꼭 -1, 0, 1을 반환할 필요는 없다. 

````java
@Override
public int compareTo(User o){
    return this.age - o.age;
}
````

위와 같이 두 값의 차를 반환하면 자연스럽게 음수, 0, 양수로 반환되므로 훨씬 간편하게 사용할 수 있다.

**하지만 위와 같이 두 값의 차를 구할 때 정수의 범위를 넘어가버릴 수 있으므로, 반드시 확인 후 사용하자!**

<br>

-----

### Comparator

`Comparator` 을 사용하려면 `compare(T o1, T o2)` 메서드를 재정의 해야한다. `compare(T o1, T o2)` 메서드는 매개변수가 두개로, 자기 자신의 값과는 무관하게 두 매개변수를 비교한다.

``` java
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {
        User userA = new User(100, 25);
        User userB = new User(101, 23);
        User userC = new User(102, 25);

        int isBig = userB.compare(userA, userC);

        System.out.println(isBig);	// -1
    }
}

class User implements Comparator<User> {
    int userNum;
    int age;

    public User(int userNum, int age) {
        this.userNum = userNum;
        this.age = age;
    }

    @Override
    public int compare(User o1, User o2) {
        if (o1.age > o2.age) {
            return 1;
        } else if (o1.age < o2.age) {
            return -1;
        } else {
            if (o1.userNum > o2.userNum) {
                return 1;
            } else {
                return -1;
            }
        }
    }
}
```

`compare()` 메서드 재정의 부분을 살펴보면 매개변수로 넘어온 `o1`과 `o2`를 `age`를 기준으로, 나이가 같으면 `userNum`을 기준으로 비교하는 것을 확인할 수 있다.

그리고 호출하는 부분에서 `userB.compare(userA, userC)` 을 했는데, 이는 `userB`와는 아무 관련 없이 `userA`와 `userC`만을 비교해 -1이 반환된다.

`compare()`도 `compareTo()`와 마찬가지로 두 값의 차를 반환해서 간략하게 나타낼 수 있다. 이 역시 정수의 범위를 벗어날 수 있음에 주의하자.

<br>

----

### 정렬

자바에서의 정렬은 오름차순이 기본값이다. 그럼 정렬이 되는 원리는 무엇일까?

`{3, 2}` 배열을 정렬한다고 생각해보자. 이 때 두 값을 비교해 차이가 양수면 자리를 바꾸는 것이다. 여기서 **두 값의 비교**가 위에서 배웠던 `Comparable` 이나 `Comparator`을 통해 이루어지는 것이다. 

반대로 생각해보면, 클래스에서 `compare()`이나 `compareTo()`을 적절하게 재정의한다면, 우리만의 객체 정렬 기준을 만들 수 있고 그에 따른 정렬도 가능하다는 것이다.

```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        ArrayList<User> users = new ArrayList<>();
      
        users.add(new User("userA", 109, 25));
        users.add(new User("userB", 110, 24));
        users.add(new User("userC", 106, 25));
        users.add(new User("userD", 108, 23));
        users.add(new User("userE", 107, 24));

        Collections.sort(users);

        for (User data : users){
            System.out.print(data.userName + " ");
        }
      	// userD userE userB userC userA 
    }
}

class User implements Comparable<User> {
    String userName;
    int userNum;
    int age;

    public User(String userName, int userNum, int age) {
        this.userName = userName;
        this.userNum = userNum;
        this.age = age;
    }

    @Override
    public int compareTo(User o) {
      	// int 범위를 넘어가는 것은 고려하지 않았음
        if(this.age == o.age){
            return this.userNum - o.userNum;
        }

        return this.age - o.age;
    }
}
```

`age`로 비교하되, 같으면 `userNum`으로 비교하도록 `compareTo()` 메서드를 재정의했다.

메인 메서드에서 `userA`부터 `userE` 까지를 `ArrayList<User>` 에 넣고 `Collections.sort()` 해 출력해보면, 재정의한 기준대로 `userD userE userB userC userA`가 잘 출력 되는 것을 확인할 수 있다.