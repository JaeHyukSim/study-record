>### 참조 : https://yeolco.tistory.com/94

### Vector
- 예전 자바에서 제공했던 레거시 클래스
- 레거시 클래스란? Collections 프레임워크가 포함되어 있지 않던 초기 자바에서 정의한 Interface
- 현재는 재구성 및 설계되어, Collections 프레임워크와 완벽하게 호환된다

- 필요에 따라 크기를 동적으로 조절할 수 있는 동적 배열을 구현
- 정수 인덱스로 액세스
- Thread Safe(동기화) 되어있어, 한번에 하나의 쓰레드만 벡터의 메서드를 호출할 수 있다.

### ArrayList
- Collections 프레임워크의 일부. java.util 패키지 내에 존재.
- 벡터와 마찬가지로 동적 배열을 사용하기 위해 사용

- 표준 배열보다 약간 느리다
- 배열에서 많은 조작이 필요할 때 유용하게 사용
- Integer, Object 등의 객체에 대해 참조해서 사용

### 차이점
- 동기화(Synchronize) : Vector는 동기화, ArrayList는 비동기화
- ArrayLisy에서 여러 스레드가 동시에 엑세스 한다면, 명시적으로 동기화하는 코드를 추가
- Thread Safe : 여러 스레드가 동시에 접근해도 문제가 없어야 한다.
- Vector는 Thread Safe하지만, ArrayList는 명시적으로 동기화 해야 한다.
- 성능 : ArrayList는 비동기화이기 때문에 벡터보다 빠르다
- Vector와 ArrayList에서 최대 인덱스를 초과할 때 추가되는 인덱스 수.
- Vector는 100%, ArrayList : 50%

### 결론
- 멀티 스레드 환경이 아닌 경우, ArrayList 사용이 바람직하다
- Vector를 사용하기 위한 명시적 요구사항이 없는 경우, ArrayList
