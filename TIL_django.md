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







## 2. 구현 순서

| 단계 |                          실행 순서                           |
| ---- | :----------------------------------------------------------: |
| 기초 | edit `settings.py`->`migrate`->`runserver`->`createsuperuser`->`startapp`->add app in `settings.py` |
| 모델 | `models.py`->`makemigrations`+`migrate`->`admin.py`=>글 포스트하기 |
|      |                                                              |





## 3. ERROR

> 정말 무서워잉



1) `makemigrations`하고 나서 text상자 없는 오류발견

: `migration 001 파일` 삭제->여전히 오류->DB까지 삭제->`makemigrations` 성공

2) admin page 로그인이 안되는 오류 발생

:DB삭제해서 superuser 정보까지 날아감->재생성

3) 여전히 글등록이 안되는 문제 발생

:`makemigrations` 하고나서 `migrate` 빼먹은게 문제.

->`migrate` 실행 후 글 등록까지 완료

