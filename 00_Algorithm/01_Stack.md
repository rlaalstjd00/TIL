## 스택

- 한쪽 끝에서만 자료를 넣고 뺄 수 있는 자료구조
- LIFO (Last In First Out)
- 연산
  - push : 자료 넣기
  - pop : 자료 빼기
  - top : 가장 위에 있는 자료 보기
  - empty : 스택이 비어있는지 확인 (비었으면 1, 아니면 0)
  - size : 자료 개수 확인

#### 스택의 구현

- 배열로 구현
- 배열의 크기를 size라고 했을 때
  - push는 stack[size] 에 값을 넣고, size += 1
  - pop은 stack[size-1] 의 값을 지우고, size -= 1

