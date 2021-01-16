# Django Project 공부

> 미래의 나를 위한 작업!



## 1. 모르니까 일단 적는다

> 참고자료: 장고걸스 튜토리얼(https://tutorial.djangogirls.org/ko/)

1) 객체지향 프로그래밍

- 역할과 동작을 지시하여 알아서 신경쓰이지 않게 수행할 수 있도록 하는 프로그래밍
- `속성 = 명사`, `매서드 = 동사`라고 일단 생각하기

2)  `models.py` 

- class Post(models.Model):
  - class: 객체를 정의하겠다(특히 속성!). class의 첫글자는 무조건 **대문자**
  - Post: 모델의 이름.
  - DB안의 Model = 뼈대
  - *models.Model에서 앞에 models는 뭐지?*

  

- def publish(self):
  - def: 함수 또는 메서드임을 나타냄
  - 매서드는 공백X 대문자X. **소문자+'_'조합**으로 사용하고 이름 변경도 가능
  - string: 텍스트
  - *self가 따라붙는 이유?*

- `makemigrations`
  - 데이터를 저장하는 DB에 뼈대인 모델을 집어넣어주는 역할!
  - DB안에서 수많은 데이터들이 마구잡이로 떠다니지 않고 이쁘게 라벨링되어서 정리되어있도록 `models.py`에서 정의한 뼈대를 DB에 넣어주는 것
  - 장고의 기본 데이터베이스는 SQLite

3) `urlconf`

- url=좌표. 모든 페이지는 고유한 url을 부여받음. 
- `urlconf`: <u>url의 패턴을 설정</u>하여 일치하는 view를 찾기 위한 패턴들의 집합(`http:@@@.co.kr로 끝나는 url 찾아주세요)
- path('admin/', admin.site.urls),
  - admin/으로 시작하는 모든 URL을 view와 대조해 찾아내라
  - 무수히 많은 url이 존재하여 일일히 나열할 수 없기 때문에 정규표현식을 사용
- from django.urls import path, include
  - `from %% import @@` =>%%에 있는 @@ 불러오기
  - `app.urls`을 가져오기 위해서 `django.url` 모듈에 있는 `include`함수 사용. 
  - `include()`: 다른 urlconf들을 참고하도록 도와줌. url중 일치하는 부분은 잘라내고, 남은 문자열 부분을 `include`된 URLconf로 전달

- path('', views.post_list, name='post_list')
  - `name='post_list'` => url의 별명. Jan이라고 불러요~ 같은거
  - `''`: 연관된 주소 뭘 넣어도 바로 `views.post_list`를 보여줘
  - `views.post_list => `views.`파일 안에 `post_list` 부분을 뿌려줘

4) `views.py`

- ```python
  def post_list(request): 
  	return render(request, 'blog/post_list.html')
  ```

  - -> 요청을 넘겨받아 render 메서드 호출->호출받은 템플릿을 보여줌

- view는 templates과 forms에 연결되어있음



5) `post_list.html`

- templates



6) QuerySet

- 사이트에 작성한 글을 DB로 저장하기 위한 단계





## 2. 구현 순서

| 단계     |                          실행 순서                           |
| -------- | :----------------------------------------------------------: |
| 기초     | edit `settings.py`->`migrate`->`runserver`->`createsuperuser`->`startapp`->add app in `settings.py` |
| 모델     | `models.py`->`makemigrations`+`migrate`->`admin.py`=>글 포스트하기 |
| URL      | 최상위 `url.py`에  `include('app.url')` 경로 추가->`app/url.py`파일 생성->url패턴 추가 |
| views    | `post_list` 정의해주기->`templates/app/ post_list.html` 생성 |
| QuerySet |                          `DB 정리`                           |
|          |                                                              |
|          |                                                              |
|          |                                                              |
|          |                                                              |





## 3. ERROR

> 정말 무서워잉



1) `makemigrations`하고 나서 text상자 없는 오류발견

: `migration 001 파일` 삭제->여전히 오류->DB까지 삭제->`makemigrations` 성공

2) admin page 로그인이 안되는 오류 발생

:DB삭제해서 superuser 정보까지 날아감->재생성

3) 여전히 글등록이 안되는 문제 발생

:`makemigrations` 하고나서 `migrate` 빼먹은게 문제.

->`migrate` 실행 후 글 등록까지 완료

3) `urls.py`실행 에러

- ModuleNotFoundError: No module named 'django.<u>url</u>'
  - url->urls
- TypeError: view must be a callable or a list/tuple ins the case of include().
  - post_list.html 저장 안해서 뜬 오류
  - HttpResponse 날렸는데도 안뜸
    - HttpResponse 호출 들어간 객체(?) 정의가 post_list_test로 바뀌어서 그랬음!
- django.template.exceptions.TemplateDoesNotExist: blog/post_list.html
  - post_list.html없어서 뜬 오류