## Set

#### Set 인터페이스

Set 인터페이스는 중복을 허용하지 않고 저장 순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용된다. 

#### HashSet 클래스

Set 인터페이스를 구현한 가장 대표저 컬렉션.

#### HashSet의 메서드

|            생성자/메서드             |                        설명                         |
| :----------------------------------: | :-------------------------------------------------: |
|              HashSet()               |              HashSet 객체를 생성한다.               |
|        HashSet(Collection c)         |     주어진 컬렉션을 포함하는 HashSet 객체 생성      |
|     HashSet(int initialCapacity)     |   주어진 값을 초기용량으로 하는 HashSet 객체 생성   |
| HashSet(initialCapacity, loadFactor) |      초기용량과 load factor를 지정하는 생성자       |
|            add(Object o)             |            새로운 객체 저장. 성공시 true            |
|         addAll(Collection c)         |           주어진 컬렉션의 모든 객체 추가            |
|               clear()                |                   모든 객체 삭제                    |
|               clone()                |                    HashSet 복제                     |
|             cointains(o)             |                지정된 객체 포함 여부                |
|           containtsAll(c)            |         지정된 컬렉션의 모든 객체 포함 여부         |
|              inEmpty()               |              HashSet이 비어있는지 여부              |
|              iterator()              |                    Iterator 반환                    |
|              remove(o)               |             지정객체 삭제. 성공시 true              |
|             removeAll(c)             | 지정된 컬렉션에 저장된 모든 객체와 동일한 객체 삭제 |
|             retainAll(c)             |              교집합 부분을 남기고 삭제              |
|                size()                |               저장된 객체의 개수 반환               |
|              toArray()               |               객체배열의 형태로 반환                |
|         toArray(Object[] a)          |               객체배열 a 에 담아 반환               |

> load factor란 컬렉션 클래스에 저장공간이 가득 차기 전에 미리 용량을 확보하기위한 것이다.
>
> 예를 들어 이 값을 0.8로 지정하면 저장공간의 80%가 채워졌을 때 용량이 두 배로 늘어난다. (기본값 0.75)