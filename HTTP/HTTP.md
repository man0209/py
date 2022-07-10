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

