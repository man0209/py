# Basid 인증
- Basic 인증은 유저 이름과 패스워드로 인증을 한다. 유저 이름과 패스워드는 Authorization 헤더에 넣어 요청마다 전송.
- Authorization 헤더의 내용은 유저이름:패스워드 로 구성하고 Base64인코딩한 문자열이 된다. 문자열은 암호처럼 보이지만 실상은 간단히 디코딩이 가능
- 따라서 네트워크 상에서 암호가 흘러다닌다고 생각할 수 있다. 보다 높은 정도의 보안 강도를 위해서는 SSL 과 TLS를 사용해 HTTPS 통신을 사용해야 한다.


# JWT 토큰을 header의 Authorization로 보낼 때 type 을 basic 으로 해야 할까 아니면 bearer 아니면 type 없이??
- https://jwt.io/introduction/
- Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema.
- 공식문서에서 Bearer을 사용한 Authorization header을 권장한다.
```
GET /resource HTTP/1.1
Host: server.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIXVCJ9TJV...r7E20RMHrHDcEfxjoYZgeFONFh7HgQ
```
