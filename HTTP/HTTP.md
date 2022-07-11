# HTTP 메시지 구조

```
start-line 시작 라인

header 헤더

empty line 공백 라인(CRLF)

message body
```

# HTTP 요청메시지

```
 GET /search?q=hello&hl=ko HTTP/1.1 ### start-line 시작 라인
 Host:www.google.com. ### header 헤더
 empty line 공백 라인
 요청 메시지도 body 본문을 가질 수 있다.
```

# HTTP 응답메시지

```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length:3423
empty line
message body(<html>....)
```

# 시작 라인 (요청 메시지)
- HTTP메서드(GET:조회) / 요청 대상(/search?q=hello&hl=ko) / HTTP Version
- 요청 대상은 절대경로, q=query
- 절대경로= '/'로 시작하는 경로

# 시작 라인 (응답 메시지)
- HTTP/1.1. ## HTTP 버전
- 200 ## HTTP 상태 코드 : 요청 성공, 실패를 나타냄
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
- OK ## 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

# HTTP 메서드
---
- 회원 조회/등록/삭제/변경,  여기서 리소스는 회원, 행위는 조회/등록/삭제/변경
- URI는 리소스만 식별. 리소스는 명사, 행위는 동사. 여기서 행위를 HTTP 메서드를 사용.
- HTTP 메서드 종류
  - GET : 리소스 조회
  - POST : 요청 데이터 처리, 주로 등록에 사용
  - PUT : 리소스를 대체, 해당 리소스를 대체, 해당 리소스가 없으면 생성
  - PATCH : 리소스 부분 변경
  - DELETE : 리소스 삭제

# GET
```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않음

# POST
- 클라이언트에서 서버로 요청을 보낼 때 데이터를 같이 보낼 테니까 서버 니가 이 데이터를 처리 해줘!
```
POST /members HTTP/1.1
Content-Type: application/json

{
 "username":"hello",
 "age":20
}
```
- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 서버는 요청 데이터를 처리
 - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
- 주로 전달된 데이터로 신규 리스소 등록, 프로세스 처리에 사용

# PUT
- 리소스를 대체
 - 리소스가 있으면 대체
 - 리소스가 없으면 생성
 - 쉽게 이야기해서 덮어버림
- 중요! 클라이언트가 리소스를 식별, 즉 클라이언트가 리소스를 알고 있다 /members/100 이렇게 POST는 /members까지만 알고 있다
 - 클라이언트가 리소스 위치를 알고 URI 지정
 - POST와 차이점 
 - 만약 DB에 /members/100 에 어떤 데이터가 있을 때, PUT으로 /members/100을 요청하면 DB에 있던 데이터를 새로 요청 한 데이터로 완전히 바꾼다.

# PATCH
- 리소스 부분 변경가능
- 혹시 PATCH를 지원하지 않는다면 POST를 사용하자

# DELETE
- 리소스 제거

# HTTP 메서드의 속성
- 안전(Safe Methods)
 - 호출해도 리소스를 변경하지 않는다.
 - Q : 그래도 계속 호출해서, 로그 같은게 쌓여서 장애가 발생하면요?
 - A : 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다. 
- 멱등(Idempotent Methods)
 - 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다
 - 멱등 메서드
  - GET : 한 번 조회하든, 두 번 조회하든 같은 결과가 조회된다.
  - PUT : 결과를 대체한다. 따라서 같은 요청을 여러번 해도 최종 결과는 같다.
  - DELETE : 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 똑같다.
  - POST : 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다. 
- 캐시가능(Cacheable Methods)
