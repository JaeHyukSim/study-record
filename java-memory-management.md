# 자바 메모리 관리 - 스택 & 힙
### 참고 - <https://yaboong.github.io/java/2018/05/26/java-memory-management/>
#### 열공하잣!
----------

### 개요
- Java에서 메모리 관리는 어떻게 이루어지는지 알아보자
- Stack, Heap 영역 각 역할에 대해 알아본다
- 간단한 코드예제와 함께 실제 코드에서 어떻게 Stack과 Heap 영역이 사용되는지 살펴본다
- Wrapper Class와 Immutable Object에 대해 살짝 알아보자
- Garbage Collection이 무엇인지도 아주 살짝 알아본다.

### Java의 Stack과 Heap

#### Stack
- Heap 영역에 생성된 Object 타입의 데이터의 참조값이 할당된다. (4byte 참조 포인터)
- 원시 타입의 데이터가 값과 함께 할당된다.(int ...)
- 지역 변수들은 scope에 따른 visibility를 가진다.
- 각 Thread는 자신만의 Stack을 가진다.
 
 #### Heap
 - 주로 긴 생명주기를 가지는 데이터들이 저장된다 - Object(서로 다른 코드 블럭에서 공유되는 경우가 많다)
 - app의 모든 메모리 중 stack에 있는 데이터를 제외한 부분
 - 모든 Object 타입이 저장되는 곳
 - 몇 개의 쓰레드가 존재하든 상관없이 단 하나의 Heap 영역만 존재
 
 #### 자바에서 Wrapper class
 - Integer, Character, Byte, Boolean, Long, Double, Float, Short 클래스
 - 모두 Immutable - 값을 바꾸려고 시도한다는 것 = 새로운 객체를 할당하여 포인트만 바꾼다는 것
 - 즉, 기존의 값이 바뀌지 않는다.
