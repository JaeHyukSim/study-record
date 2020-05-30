# Rest API란??

> 참고 자료 :
    1. edwith - web programming boost course <https://www.edwith.org/boostcourse-web/lecture/16740/>

>### 들어가기 전에
클라이언트의 종류가 웹 브라우저, 안드로이드 앱, iOS 앱 등, 다양해지면서 이러한 클라이언트들에게 정보를 제공하는 방법을
하나로 일원화 시키기!!!! <br>
그것이 바로 **HTTP 프로토콜로 API를 제공하는 것** <br>
**HTTP 프로토콜로 제공하는 API를 REST API라고 합니다.**

### 목표 
1. REST API가 무엇인지 이해한다.
2. WEB API(HTTP API)와 REST API를 구분할 수 있다.

### 학습하기
1. API란????(Application Programming Interface)
`응용 프로그램에서 사용할 수 있도록 운영체제, 프로그래밍 언어가 제공하는 기능 인터페이스`
`System call을 모르더라도 API를 통해 일련의 System call을 호출가능`

2. REST API란?
 1. **REST**는 REpresentational State Transfer 용어의 약자 - 2000년도에 Roy Fielding의 박사학위 논문에 최초 소개
 2. REST API = REST 형식의 API
 3. REST API란, 핵심 컨텐츠 및 기능을 외부 사이트에서 활용할 수 있도록 제공되는 Interface!!
 4. ex) Naver에서 블로그에 글을 저장, 글 목록을 읽어갈 수 있도록 외부에 기능을 제공, 우체국에서 우편번호를
 조회할 수 있는 기능을 제거, 구글에서 구글 지도를 사용할 수 있도록 제공하는 것
 5. 웹 브라우저 뿐 아니라, 앱 등 다양한 클라이언트가 등장하면서 대응하기 위해 REST API가 널리 사용되기 시작.
 6. 서비스 업체들이 다양한 REST API를 제공함으로써, 클라이언트는 이러한 REST API들을 조합한 APP을 만들
 수 있게 되었다. - 이를 Mashup이라 한다
 
 ### REST 이것을 지켜라
 1. client-server
 2. stateless
 3. cache
 4. uniform interface
 5. layered system
 6. code-on-demand (optional)
 **HTTP protocol사용 시 -> 1, 2, 3, 5, 6에 대해서는 모두 쉽게 구현** <br>
 **문제는 uniform interface**
     - 리소스가 URI로 식별되야 한다
     - 리소스를 생성, 수정, 추가하고자 할 때 HTTP 메시지에 표현을 해서 전송해야 한다.
     - 메시지는 스스로 설명할 수 있어야 한다(Self-descriptive message)
     - 애플리케이션의 상태는 Hyperlink를 이용해 전이되야 한다(HATEOAS) <br>
 **어려운 점** <br>
 스스로 설명하기, HATEOAS를 지키는 것은 API로 쉽지 않다.
 - REST API는 쉽지 않다. 그래서, 보통은 Web API 혹은 HTTP API를 사용한다.
 - 따라서, REST의 몇가지 규칙을 안지킨다면 걍 WEB, OR HTTP API라 부르자 ^^
