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

#> Roy T Fielding
#### "How do I improve HTTP without breaking the web?"
-----------

#### REST : Architectured Styles and the Design of Network - based Software

### Uniform Interface의 제약조건
    - identification of resources -> uri로 resource 식별
    - manipulation of resources through representations -> resources update 표현
    - **self-descriptive messages**
    - hypermedia as the engine of application state(HATEOAS)
    
### Self-descriptive message
    - GET / Http / 1.1
    - 위와 같은 식 : 목적지가 빠져있다. (Host : www.example.org)
    - 따라서 self-descriptive 하지 못하다
### 
    - ContentType : application / json
    - 위와 같은 식 : json을 쓴다고 명시되어 있지만, json을 쓸 경우, 좀 더 구체적인 문서가 필요하다
    
###
    - Self-descriptive한 식
    - HTTP / 1.1 / OK
    - ContentType : application / json-patch + json
    - [{ "op" : "aaaa" , "path" : "/a/b/c" }]
    
###
    - json-patch + json 이라는 media 타입 명세를  찾아가서, 이해한 다음 메시지를 보라! - 설명이 가능
    
### HATEOAS
- 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야 한다.

### 왜 Uniform Interface????
- Server와 Client가 독립적으로 발전할 수 있다.
- **Server 기능이 변경되어도, Client를 Update할 필요가 없다.**

### REST 만든 계기
- **"How do I improve HTTP without breaking the web"**
- 따라서, web은 REST를 매우매우 잘 만족하고 있다.
- HTML, HTTP 명세가 바뀌어도 WEB은 잘 동작

### 따라서
- Some update에 의해 Client가 영향을 받는다:??????
- **"RESTFUL하지 않다"**
- **"REST로 통신하지 않다"**

### WEB이 REST로 잘 동작하는 이유
- W3C Working groups : HTML
- IETF Working groups : HTTP
- 웹 브라우저 개발자들
- 웹 서버 개발자들
- 이들이 매우 열심히 개발
- HTML5 첫 초안에서 권고안 나오는 데까지 **6년**
- HTTP/1.1 명세 개정판 **7년**

### 상호운용성(interoperability)에 대한 집착
- Referer 오타 안고침
- charset 잘못 지은 이름 안고침
- HTTP 상태코드 416 포기(I'm a teapot : 만우절때 만든, 심지어 HTTP도 아닌, 서버들이 사용하는 상태코드)
- HTTP 0.9 아직도 지원함(크롬, 파이어폭스)
- **"이미 구현체가 존재한다면 상호운용성을 위해 지켜준다"**

### REST가 웹의 독립적 진화에 도움을 주었다
- YES
- Host 헤더 추가
- 길이 제한을 다루는 방법이 명시 (414 URI Too Long 등)
- URI에서 resource 정의가 추상적으로 변경됨 "식별하고자 하는 무언가"
- 옛날에는 "문서의 위치" 정도로 정의
- HTTP / 1.1 명세 최신판에서 REST에 대한 언급이 들어감
- Reminder : Roy T Fielding이 HTTP, URI 명세의 저자 중 한명! ㅋㅋ

### Roy T Fielding
- **"If you think you have control over the system or, aren't interested in evolability, don't waste your time arguing about REST"**
- 클라이언트, 서버 둘 다 통제 가능하면 굳이 REST?
- 이용자의 적당한 불만... 괜찮아!! - (엄청 소수니깐...! ^^)
- **BUT!** 오랜 시간에 걸쳐 진화하는 시스템을 설계하고 싶다???? -> **"REST에 관심을 가져라!"**
- **"Please try to adhere to them or choose some other buzzword for your API"**
