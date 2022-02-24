## 컬렉션 프레임워크 (Collection Framework)

컬렉션 프레임워크란 데이터 그룹을 저장하는 클래스들의 표준화된 설계이다.

데이터 그룹이 크게 3가지 타입이 존재한다고 정의하여 각각의 인터페이스들을 정의했다.

#### 3가지 데이터타입의 인터페이스

1. List
   - 순서가 있는 데이터의 집합. 데이터의 중복을 허용한다.
   - 구현 클래스 : ArrayList, LinkedList, Stack, Vector ..
2. Set
   - 순서를 유지하지 않는 데이터의 집합. 데이터의 중복을 허용하지 않는다.
   - 구현 클래스 : HashSet, TreeSet ..
3. Map
   - key-value 구조로 이루어진 데이터의 집합. 순서는 유지되지 않으며 key값은 중복을 허용하지 않는다.
   - 구현 클래스 : HashMap, TreeMap, HashTable, Properties ..

> List와 Set을 구현하는 클래스들은 공통부분이 많아 공통부분을 뽑아 Collection이라는 상위 인터페이스를 추가로 정의했다.