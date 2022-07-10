# HttpRequest 객체
- 클라이언트로부터의 모든 요청 내용을 담고 있으며
- 함수 기반 뷰 : 매 요청 시마다 뷰 함수의 첫번째 인자 request로 전달
- 클래스 기반 뷰 : 매 요청 시마다 self.request를 통해 접근
- Form 처리 관련 속성들
- .method : 요청의 종류 "GET" 또는 "POST"로서 모두 대문자
- .GET : GET 인자 목록 (QueryDict 타입)
- .POST : POST 인자 목록 (QueryDict 타입)
- .FILES : POST 인자 중에서 파일 목록 (MultiValueDict 타입)

# HttpResponse
- view 함수에서의 반환값은 무조건 HttpResponse여야 한다.
- 다양한 응답을 HttpResponse라는 객체로 감싸서(Wrapping) 응답을 처리하게 된다. 감싸는 대상은 어떠한 대상도 될 수 있다.
- 웹에서는 HTML 문자열, 이미지, 엑셀, PDF, video 등등 다 가능 
