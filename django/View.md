# View
- 1개 HTTP 요청애 대해 1개의 뷰가 호출
- urls.py/urlpatterns 리스트에 매핑된 호출 가능한 객체(함수도 호출 가능한 객체 중의 하나)
- 웹 클라이언트로부터의 HTTP 요청을 처리
- 크게 함수 기반 뷰(Function Based View), 클래스 기반 뷰(Class Based View)
- 클래스 기반 뷰는 클래스.as_view()를 통해 호출가능한 객체를 생성/리턴


# URL Captured Values
```
# instagram/1/
# instagram/2/
# ...
urlpatterns= [
  path('', views.post_list),
  path('<int:pk>', views.post_detail), # instagram/뒤 int 즉 숫자가 오면 views.post_detail에 pk로 인자를 넘긴다는 의미.
  # 그럼 views.py에 있는 post_detail함수 or 클래스에서 def post_detail(request, pk) 이렇게 인자로 받을 수 있다.
  # 이렇게 url에서 인자로 받는 값을 URL Captured Values 라 부른다.
  # django 1.0때 url. 2.0때 re_path로 변경됨.
  # <int:pk> 이 부분을 Converter 라고 부른다.
```

#  
