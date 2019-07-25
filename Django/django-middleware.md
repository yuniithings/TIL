# django-middleware.md


### middleward.py 생성
`python manage.py startapp [appname]`으로 생성했던 app directroy에 만들어준다.
(따로 패키지화를 해도 됨)

### settings.py에 등록하기
```python
MIDDLEWARE = [
    ...,
    'blog.middleware.login_check',
]
```
기본적으로 등록된 middleware들의 순서는 request <-> response 순서이다.<br/>
필요한 부분에 넣어 사용하면 된다.


### 코드 작성
```python
def login_check(request):

    def middleware(request):
    
        # request 코드 작성
    
        response = get_reponse(request)
        
        # response 코드 작성        
        
        return response
        
    return middleware(request)
```

기본적인 흐름도는 이러하며, take할 reponse, request부분에 코드를 작성하면 된다.<br/>

개인적으로 응용했던 부분은 다음과 같다. 
- 홈페이지 방문자 수 확인을 위한 쿠키생성
- 로그인 만료/ 미 로그인 시 로그인페이지로 이동


 