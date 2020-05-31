# 오버로딩과 오버라이딩 차이와 예제

># 참조 : <https://private.tistory.com/25>
># 참조 : <https://itpangpang.xyz/105?category=556738>

### 개요
- Java에서는 다형성을 지원하는 방식으로 Overloading, Overriding이 있다.
- Overloading : 같은 이름의 메서드 여러개 중복해서 만들 수 있게 한다.
- Overriding : 상위 클래스가 가지고 있는 메서드를 하위 클래스가 재정의해서 사용

### Overloading
- 메서드 오버로딩과 생성자 오버로딩이 있다.
- 매개변수 유형, 개수를 다르게 해서 여러개의 메서드를 정의할 수 있다.
- **같은 기능을 다른 이름으로 구현한다면 가독성이 떨어진다**

### Overriding
- 상위 클래스의 메서드를 하위 클래스에서 재정의해서 사용
- 결합도를 낮출 수 있다 : Interface, Abstract
