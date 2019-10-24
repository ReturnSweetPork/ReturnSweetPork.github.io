# Django rest framework(DRF)를 통한 CRUD



- django REST framework 는 RESTFUL한 API를 쉽게 만들수 있도록 해줌.

- 환경셋팅

```python
pip install django 
pip install djangorestframework
```

- project생성

```
django admin startproject pjt
```

- app 생성

```
django damin startapp boards
```

- setting.py설정

```python
# settings.py 
ALLOWED_HOSTS = ['*'] 


INSTALLED_APPS = [ ... 'rest_framework', 
'boards', ]

```

- modeling

```python
# 공지사항 게시판
class Notice(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    name = models.CharField(max_length=50, default='관리자')
    contents = models.TextField()
    created_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```



- 모델링 완료후 마이그레션 및 마이그레이트 진행

```
python manage.py makemigrations 
python manage.py migrate
```



- serializer 생성

````python
from rest_framework import serializers
from .models import Notice

class NoticeSerializer(serializers.ModelSerializer):
    class Meta:
        model = Notice
        fields = '__all__'
````



- views.py 작성법 (viewset)

```python
from .models import Notice
from .serializers import NoticeSerializer
from rest_framework import viewsets


class NoticeViewset(viewsets.ModelViewSet): 
	queryset = Notice.objects.all() 
	serializer_class = NoticeSerializer


```



- urls.py 작성

```python
from django.urls import path
from django.conf.urls import url
from . import views

urlpatterns = [
    path('notice', views.notice_list.as_view()),
    path('notice/<int:pk>', views.notice_detail.as_view()),
]
```



- 실행

```
python manage.py runserver 
```



- 완성 및 확인작업



만들어진 CRUD를 사용해서 요청을 실시한다.



GET/notice/

공지사항 리스트 조회

POST/notice/

공지사항 리스트 생성

GET/notice/{pk}

공지사항 리스트 조회(1개의 특정 공지사항)

PUT/notice/{pk} 

공지사항 객체 수정

DELETE/notice/{pk}

공지사항 객체 삭제



