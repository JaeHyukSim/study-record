#String, StringBuilder, StringBuffer의 차이점과 장단점

>## 참조 : <https://12bme.tistory.com/42>

### String, StringBuilder, StringBuffer 모두 문자열을 저장하고 관리하는 클래스

### String
- String = Immutable, StringBuffer= Mutable
- 문자열을 조작하는 경우 유용하게 사용할 수 있다.
- concat을 사용하기 위해, 단순한 경우 String의 +연산자를 활용할 수 있다
- String 객체는 한번 생성되면, 할당된 메모리 공간이 변하지 않는다. 따라서 문자열 조작시, 새로운 메모리 할당이 이루어진다.
- Heap영역에 생성되고, 참조 변수가 없다면 GC가 회수
- 이러한 이유로, 문자열 연산이 많을 경우, 성능이 좋지 않다.
- Immutable한 객체는 간단하게 사용 가능하고, 동기화에 대해 신경쓰지 않아도 되기 때문에(Thread Safe) 내부 데이터를 자유롭게 공유할 수 있다.

### StringBuffer와 StringBuilder
- 문자열 연산 등으로 기존 객체의 공간이 부족하다면 버퍼의 크기를 유연하게 늘린다.
- StringBuffer와 StringBuilder 클래스가 제공하는 메서드는 서로 동일하다.
- 두 클래스의 차이점 : 동기화 여부
- StringBuffer : 각 메서드별로 Synchronized Keyword가 존재. 멀티 스레드 환경에서도 동기화 지원
- StringBuilder : 동기화를 보장하지 않음.
- 멀티 스레드 환경 : StringBuffer 사용
- 단일 스레드 환경 : StringBuilder 사용. (StringBuffer를 쓰면 동기화 관련 처리로 성능이 떨어질 수 있다)

### 강조
- String은 짧은 문자열을 더할 경우 사용
- StringBuffer는 스레드에 안전한 프로그램이 필요할 때, 개발중인 시스템의 부분이 스레드에 안전한지 모를 경우
- StringBuilder는 스레드에 안전한지 여부가 전혀 관계 없는 프로그램 개발 시 사용
- JDK 1.5 이후 : String 클래스를 활용해도 : StringBuilder로 컴파일된다.
- 하지만 루프를 사용해서 문자열을 더할 때는 객체를 계속 추가한다는 사실에는 변함이 없다
- **스레드와 관련이 있으면 StringBuffer, 그렇지 않으면 StringBuilder를 사용하는 것을 권장**
- 단순히 성능만 놓고 본다면 연산이 많은 경우 : StringBuilder > StringBuffer >>> String
