## 큐 (Queue)

- 한쪽 끝에서만 자료를 넣고 다른 한쪽 끝에서만 뺄 수 있는 자료구조
- FIFO (First In First Out)
- 연산
  - push : 자료 넣기
  - pop : 자료 빼기
  - front : 큐의 가장 앞에 있는 자료 보기
  - back : 큐의 가장 뒤에 있는 자료 보기
  - empty : 큐가 비어있는지 확인 (비어있으면 1, 아니면 0)
  - size : 큐에 저장되어있는 자료의 개수 확인

#### 큐의 구현

- 배열로 구현
- 시작 인덱스를 begin, 마지막 자료 다음 인덱스를 end 라고 했을 때
  - push는 queue[end] 에 값을 넣고 end += 1
  - pop은 queue[begin] 을 지우고 begin += 1
  - size 는 end - begin
  - empty 는 begin = end 확인

> [큐의 구현 (python) 백준 10845](https://github.com/rlaalstjd00/Algorithm_Quiz/blob/master/Baekjoon/Data_Structures/10845.py)



## 덱 (Deque)

- 양 끝에서만 자료를 넣고 양 끝에서만 뺄 수 있는 구조
- Double-ended queue 의 약자
- 연산
  - push_front : 덱의 앞에 자료 넣기
  - push_back : 덱의 뒤에 자료 넣기
  - pop_front : 덱의 앞에서 자료를 빼기
  - pop_back : 덱의 뒤에서 자료 빼기
  - front : 덱의 가장 앞의 자료 보기
  - back : 덱의 가장 뒤의 자료 보기

