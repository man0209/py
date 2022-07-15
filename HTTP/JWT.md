# JWT란?
- JWT는 Json Web Token의 약자로 모바일이나 웹의 사용자 인증을 위해 사용하는 암호화된 토큰을 의미
- JWT 정보(사용자 id, 토큰 생성시간, 만료시간)를 request에 담아 사용자의 정보 열람, 수정 등 개인적인 작업들을 수행할 수 있다.

# JWT를 사용해 인증 시스템을 구축하는 이유
- 유저의 로그인 상태를 브라우저에서 간단하게 저장할 수 있어 서버의 부담이 적다
- 보안 문제 예방
- 대표적인 문제 XSS, CSRF 공격
- XSS
  - Cross Site Scription의 약자로 Code Injection Attack이라고도 한다. 이는 공격자가 의도하는 악의적인 js 코드를 목표 웹 브라우저에서 실행시키는 것
- CSRF
  - Cross Site Request Forger.
  - 정상적인 request를 가로채 백엔드 서버에 변조된 request를 보내 악의적인 동작을 수행하는 공격
  - 클라이언트의 정보 수정, 삭제, 조회. 
- 위와 같은 문제를 예방하기 위해 JWT 토큰의 만료 시간을 5분으로 설정하고, refresh 토큰을 추가적으로 생성하는 방법이 있다.
- Refresh 토큰을 httpOnly 쿠키로 설정하고, url이 새로고침 될 때마다 기존의 refresh 토큰을 가지고 새로운 JWT토큰을 요청한다.
- 그리고 발급받은 JWT토큰을 js내의 private변수에 저장한다.
- 이러한 방식은 refresh 토큰이 CSRF에 의해 사용된다 하더라도, 공격자는 실제로 인증에 사용되는 access_token을 알 수 없기 때문에 안전.
- 그리고 refresh 토큰이 httpOnly=True인 쿠키에 저장되기 때문에 XSS공격으로부터 안전하게 된다.
