## Garbage Collector (GC)

---

### GC란?

- GC란 메모리 관리를 위해 힙 영역에서 더 이상 사용하지 않는 객체를 메모리에서 제거하는 것이다.

<br>

### GC의 동작 원리

- JVM에서 GC의 스케쥴링을 담당하여 자바 개발자에게 메모리 관리의 부담을 덜어준다.
- 데몬스레드로 돌며 더 이상 사용하지 않는 객체들을 메모리에서 제거한다.
  - 메모리 영역 중 힙 영역에서 참조되지 않는 객체를 제거한다.
  - 메모리 영역에 관한 정보는 [JVM과 메모리 구조](https://github.com/rlaalstjd00/TIL/blob/master/01_Java/45_JVM%EA%B3%BC%20%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EA%B5%AC%EC%A1%B0.md) 참조

<br>

### GC가 발생한는 Heap 영역에 대해 알아보자

<img src="../99_img_src/01_Java_GC.png">

- Young Generation
  - Eden
    - 새로 생성된 객체들이 위치한다.
    - Minor GC 발생
  - Survivor 1, 2
    - Eden 영역에서 GC 후 살아남은 객체들이 위치한다.
    - Minor GC 발생 (1, 2 영역을 여러번 오가며 GC 가 발생한다.)
- Old Generation
  - Survivor 영역에서 GC 후 살아남은 객체들이 위치한다. (객체의 크기가 아주 크다면 Eden 영역에서 바로 넘어올 수도 있다.)
  - Major GC(Full GC) 발생

<br>

### GC의 방식

JDK 7 이상에서는 5 가지의 GC 방식이 존재한다.

- **Serial Collector**
  - 하나의 CPU 사용
  - 단일 스레드 환경을 위한 GC
  - Young 영역과 Old 영역이 시리얼(연속적)하게 처리되는데, 이를 수행할 때 애플리케이션 수행이 정지된다. (Stop-the-world)
  - Mark-sweep-compact 컬렉션 알고리즘 사용
    - 표시 단계 : Old 영역으로 이동한 객체중 살아있는 객체 식별
    - 스윕 단계 : Old 영역의 객체를 훑으며 불필요한 객체 식별
    - 컴팩션 단계 : 필요없는 객체를 지우고 살아있는 객체를 한 곳으로 모음
- **Parallel Collector**
  - 멀티 CPU 환경에서 사용
  - Java 8의 기본 GC
  - Mark-sweep-compact 컬렉션 알고리즘 사용
  - 시리얼 컬렉터와 달리 Young 영역에서의 컬렉션을 병렬로 처리해 GC 부하를 줄인다.
- **Parallel Compacting Collector**
  - 멀티 CPU 환경에서 사용
  - Young 영역에 대한 GC는 동일하다.
  - Old 영역에서의 GC
    - 표시 단계 : 살아있는 객체를 식별
    - 종합 단계 : 이전에 GC를 수행하여 컴팩션된 영역에 살아있는 객체 위치 조 (여러 스레드가 Old 영역을 분리해 훑는다.)
    - 컴팩션 단계 : 컴팩션 수행. 수행 후에는 컴팩션된 영역과 빈 영역으로 나뉜다.
- **Current Mark-Sweep(CMS) Collector**
  - 중단시간을 아주 짧게 하기 위해 설계된 GC
  - 응용 프로그램의 스레드와 동시에 수행하여 일시 중지를 최소화
  - 힙 메모리 영역의 크기가 클 때 적합
  - Parallel GC보다 Full GC 처리 시간을 빠르지만, `Concurrent mode failure`가 발생하면 다른 Parallel보다 느려진다.
    - CMS는 기본적으로 Compaction 작업을 수행하지 않기 때문에, 넣을 객체보다 큰 공간이 남아있는데도 이 공간이 연속적이지 못해 객체를 넣지 못할 수도 있다. 이 때 `Concurrent mode failure` 이라는 경고가 발생하며 Compaction 작업이 수행된다.
  - Young 영역에 대한 GC는 동일하다.
  - Old 영역에서의 GC
    - 초기 표시 단계 : 매우 짧은 대기시간으로 살아있는 객체를 찾는 단계
    - 컨커런트 표시 단계 : 서버 수행과 동시에 살아있는 객체에 표시 해놓는 단계
    - 재표시 단계 : 컨커런트 표시 단계를 수행하는 동안 변경된 객체에 대해 재표시하는 단계
    - 컨커런트 스윕 단계 : 표시되어있는 쓰레기를 정리하는 단계
- **Garbage First(G1) Collector**
  - 대용량 메모리 공간 (4Gb 이상)이 있는 멀티 프로세서 시스템에서 실행되는 응용 프로그램을 위해 설계
  - 중단시간이 짧은 새로운 수집기로 설계, CMS보다 튜닝이 쉽다.
  - JDK 7에서 처음 등장 후, JDK 9 부터 기본 GC로 사용

<br>

>### 참조
>
>- [wooody92's blog - GC 동작원리](https://wooody92.github.io/java/GC-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC/)
>- [J-log - Java의 GC는 어떻게 동작하나?](https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html)
>- [김효재 - GC(Garbage Collector)](https://www.hyojae.info/8d060d31-bd1d-442b-a914-9312e6106d2d#5d2e0512-3955-4dbe-8803-fa6a495ac6c2)
>- [Naver O2 이상민 - Garbage Collector 튜닝](https://d2.naver.com/helloworld/37111)



