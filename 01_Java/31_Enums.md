## 열거형 (Enums)

열거형이란 연관된 상수들을 편하게 선언하기 위한 것이다.

````java
class MemberLevel{
    static final int GOLD = 0;
    static final int PLATINUM = 1;
    static final int DIAMOND = 2;
    static final int VVIP = 3;
    
    final int level;
}
````

````java
class MemberLevel{
    enum Level{ GOLD, PLATINUM, DIAMOND, VVIP }
    
    final Level level;
}
````

> 첫 번째 코드의 멤버 등급 상수를 두 번째 코드에서 `enum`을 통해 열거했다. 여기서 level 을 통해 `GOLD`, `PLATINUM`, `DIAMOND`, `VVIP` 에 접근할 수 있다.
>
> 이 때 level 타입이 `int`가 아닌 `Level` 임에 주의하자.

열거형 상수간에는 `==` 연산자를 사용할 수 있기 때문에 `equals()` 보다 성능면에서 더 빠르게 비교가 가능하다.

그러나 `<`, `>` 연산자는 사용할 수 없기 때문에 `compareTo()` 를 사용해야 한다.

> compareTo()
>
> - 두 비교대상이 같으면 0, 왼쪽이 크면 양수, 오른쪽이 크면 음수 반환