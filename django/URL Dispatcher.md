- HTTP 요청이 들어올 때마다, 등록된 urlpatterns 상의 매핑 리스트를 처음부터 순차적으로 훑으며 URL 매칭을 시도
- 매칭이 되는 URL Rule이 다수 존재하더라도, 처음 Rule만을 사용. 따라서 URL이 겹치지 않도록 잘 설계해야함.
- 매칭되는 URL Rule이 없을 경우, 404 Page Not Found 응답을 발생

# path, re_path (django 2.x 대에서 등장)
- django 1.x에서의 django.conf.urls.url() 사용이 2가지로 분리 -> path, re_path
- django.urls.re_path() = django.conf.urls.url()과 동일
- django.urls.path()
  - 기본 지원되는 path converters를 통해 정규표현식 기입이 간소화 -> 만능은 아니다
  - 자주 사용되는 패턴을 converter로 등록하면, 재활용면에서 편리 

```
# django 1.x에서의 다음 코드를
url(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive), ## 0~9사이의 숫자가 4번 반복된다. ex) 1(X) 124(X) 1234(O) 16436(X) 1324(O)

# 다음과 같이 간소화 가능
path('articles/<int:year>/', views.year_archive), ## 정수형이 반복된다. 1(O) 235(O) 235235(O)

# 물론 다음과 같이 동일하게 쓸 수 있다.
re_path(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive)
```
path(' ', views.item_list, name='item_list'),
```
- ' '에 어떠한 문자열이 들어왔을 경우, views.item_list 이러한 views 함수를 호출하겠다라는 의미.

# 기본 제공되는 Path Converters
- IntConverter : r'[0-9]+' ## 정수가 +는 1회 이상 반복된다는 뜻.
- StringConverter : r'[^/]+' ## /를 제외한(^) 어떤 문자열이 + 1회 이상 반복
- UUIDConverter : r'[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0--9a-f]{4}-[0-9a-f]{12}' ## 16진수 범위의 문자 8회 반복([0-9a-f]{8})...
- SlugConverter : (StringConverter 상속) : r'[-a-zA-Z0-9_]+'
- PathConverter (StringConverter 상속) : r'.+' ## .이 모든 문자열을 뜻함. 즉 모든 문자열에 대해 1회 이상 반복

# 정규 표현식(Regular Expression)
- 거의 모든 프로그래밍 언어에서 지원
- 문자열의 패턴, 규칙, Rule을 정의하는 방법
- 문자열 검색이나 치환작업을 간편하게 처리
- django URL Dispatchard에서는 정규표현식을 통한 URL 매칭
- 문법 
  - 1글자에 대한 패턴 + 연속된 출연 횟수 지정
  - 대괄호 내에 1글자에 대한 후보 글자들을 나열
- ex)
  - 3자리 숫자 : r'\d{3}'
  - [] 대괄호는 여러가지 를 나열할 때
  - 휴대폰 번호 : r'010[1-9]\d{7}' 1~9사이의 숫자가 연속해서 7번
  - 알파벳 소문자 1글자 : '[a-z]'
  
# 반복횟수 지정 문법
- r'\d' : 별도 횟수 지정 없음 -> 1회 반복
- r'\d{1}' : 1회 반복
- r'\d{2}' : 2회 반복
- r'\d{2,4} : 2~4회 반복
- r'\d?' : 0회 혹은 1회 반복
- r'\d*' : 0회 이상 반복
- r'\d+' : 1회 이상 반복
- 정규표현식은 띄워쓰기 하지 말자
