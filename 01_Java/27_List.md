## List

#### List 인터페이스

List 인터페이스는 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용된다.

#### List  인터페이스에 정의된 메서드

|           메서드            |                             설명                             |
| :-------------------------: | :----------------------------------------------------------: |
|     add(index, element)     |    지정된 위치(index)에 객체(Object element)를 추가한다.     |
|         get(index)          |          지정된 위치(index)에 있는 객체를 반환한다.          |
|         indexOf(o)          |           지정된 객체(Object o)의 위치를 반환한다.           |
|       lastIndexOf(o)        |             indexOf와 같지만 찾는 방향이 역방향.             |
|       listIterator()        |       List 객체에 접근할 수 있는 ListIterator를 반환.        |
|        remove(index)        | 지정된 위치(index) 에 있는 위치를 삭제하고 삭제된 객체를 반환. |
|     set(index, element)     |                지정된 위치에 객체를 저장한다.                |
|           sort(c)           |       지정된 비교자(Comparator c) 로 List를 정렬한다.        |
| subList(fromIndex, toIndex) |        fromIndex부터 toIndex에 있는 객체를 반환한다.         |



#### ArrayList 클래스

List 인터페이스의 구현 클래스이다.

ArrayList는 배열을 이용해 데이터를 순차적으로 저장하고, 더 이상 저장할 공간이 없다면 보다 큰 배열을 생성해 기존의 내용을 새로운 배열로 복사해 저장한다.

#### ArrayList 클래스의 메서드

|          생성자/메서드          |                         설명                         |
| :-----------------------------: | :--------------------------------------------------: |
|           ArrayList()           |             크기가 10인 ArrayList  생성              |
|     ArrayList(Collection c)     |          컬렉션 c가 저장된 ArrayList  생성           |
| ArrayList(int initialCapacity)  |        지정된 초기용량을 갖는 ArrayList  생성        |
|          add(Object o)          |   ArrayList의 마지막에 객체 추가. 성공시 true 반환   |
|      addAll(Collection c)       |             컬렉션  c의 모든 객체를 저장             |
|        addAll(index, c)         |       지정 위치부터 컬렉션 c의 모든 객체 저장        |
|             clear()             |                  ArrayList  비우기                   |
|             clone()             |                    ArrayList 복제                    |
|       contains(Object o)        |        지정 객체 o가 포함되있는지 아닌지 확인        |
| ensureCapacity(int minCapacity) |        용량이 최소한 minCapacity가 되도록 함         |
|           get(index)            |             지정 위치에 저장된 객체 반환             |
|        indexOf(Object o)        |             지정 객체가 저장된 위치 반환             |
|            isEmpty()            |                   비어있는지 확인                    |
|           iterator()            |            ArrayList의 iterator 객체 반환            |
|      lastIndexOf(Object o)      |      객체가 저장된 위치를 끝부터 검색해서 반환       |
|         listIterator()          |           ArrayList의 ListIterator를 반환            |
|       listIterator(index)       | ArrayList의 지정 위치부터 시작하는 ListIterator 반환 |
|          remove(index)          |             지정된 위치에 있는 객체 제거             |
|        remove(Object o)         |            지정한 객체 제거. 성공시 true             |
|     removeAll(Collection c)     |    지정한 컬렉션에 저장된 것과 동일한 객체를 제거    |
|       set(index, element)       |           주어진 객체를 지정된 위치에 저장           |
|             size()              |               저장된 객체의 개수 반환                |
|       sort(Comparator c)        |               지정된 정렬기준으로 정렬               |
|   subList(fromIndex, toIndex)   |     fromIndex와 toIndex 사이에 저장된 객체 반환      |
|            toArray()            |         저장된 모든 객체를 객체 배열로 반환          |
|       toArray(Object[] a)       |      저장된 모든 객체를 객체배열 a에 담아 반환       |
|          trimToSize()           |                     빈공간 제거                      |