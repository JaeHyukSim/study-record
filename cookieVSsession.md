# Cookie VS session 
>## 참조 : <https://interconnection.tistory.com/74>

### HTTP의 특징과 쿠키, 세션을 사용하는 이유
- HTTP 프로토콜의 약점을 보완하기 위해.
- connectless, stateless

### Cookie
- Client local에 저장되는 key-value 데이터 파일 (최대 4KB)
- 유효 시간이 정해지면, 브라우저가 종료되어도 인증이 유지
- 300개까지 쿠키 저장 가능, 하나의 도메인당 20개, 4KB
- Response Header에 Set-Cookie 속성을 사용하면 클라이언트에 쿠키 만들 수 있다.
- 자동으로 브라우저가 Request Header에 넣어서 서버에 전송
- 방문 사이트 자동 로그인("아이디, 비번을 저장하시겠습니까?")
- 쇼핑몰의 장바구니
- 팝업("오늘은 더 이상 이 창을 보지 않음")

### Session
- 쿠키를 기반으로 서버측에서 관리
- 세션 ID 부여, Client의 서버 접속 ~ 브라우저 종료까지 인증상태 유지
- 접속 시간 제한 설정 가능
- 사용자가 많아질수록 서버 메모리 많이 차지
- 쿠키보다 보안에 좋음
- 동접자 = 성능저하
- 로그인 같이 보안상 중요한 작업을 수행할 때 사용

### Cookie VS Session
- 세션도 쿠키를 사용
- 저장 위치가 다름
