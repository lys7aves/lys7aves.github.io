---
layout: post
title: '[Back-end] Django를 이용하여 서버 구축하기(1)'
date: 2022-03-13-10:32
author: 이유섭
cover: '/assets/img/2022-03-13-(Back-end) Django를 이용하여 서버 구축하기(1)/Django_server.png'
tags: back_end Django Server
---



_Last updated: 2022. 03. 13._



# 기본 설정



1. 가상환경 만들기

 가상환경을 만들 디렉토리로 이동한 후, 아래 명령어를 통해 가상환경을 만들 수 있다.

```shell
$ python -m venv [venv name]
```



2. 가상환경 활성화

```shell
$ [venv name]\Scripts\activate
```



3. 패키지 설치 (Django install)

```shell
$ pip install django
$ pip install [package name]
```

 Django를 포함하여 기타 필요한 패키지들을 설치해준다.



4. Django 프로젝트 생성

```shell
$ django-admin startproject [project name]
```



5. Pycharm으로 가상환경 활성화 하기

 생성한 프로젝트를 열어준다.

- File > Open.. 클릭
- 생성한 프로젝트 선택 (가상환경이 아닌 Django 프로젝트를 선택해야 한다.)

 프로젝트의 가상환경을 잡아준다.

- File > Settings..
- Project: [project name] > Python Interpreter
- 설정(톱니바퀴) > Add..
- Existing environment 선택
- Interpreter 경로를 "가상환경 폴더\\Scripts\\python.exe"로 설정

 Pycharm 환경 하단에 있는 "Terminal"을 클릭해 확인해보면 가상환경으로 접속되어 있는 것을 볼 수 있다. 만약 PowerShell(PS)로 되어 있다면, 터미널 창 상단에 "v" 를 클릭하여 "Command Prompt"를 클릭하면 가상환경에 접속한 터미널을 볼 수 있다.



# 시크릿 키(SECRET_KEY) 분리 설정

 Django 프로젝트를 생성하면, 기본적으로 메인 폴더에 settings.py가 생성된다. settings.py 안에는 다양한 설정 항목들이 있는데, 그 중 SECRET_KEY라는 것도 있다.

 SECRET_KEY

- SECRET_KEY란 특정 django 설치를 위한 비밀 키이다. 이는 암호화 서명을 제공하는데 사용되며 고유하고 예측할 수 엇는 값으로 설정해야 한다.
- SECRET_KEY는 공개하면 안된다.
- SECRET_KEY가 없으면 Django 프로젝트는 실행되지 않는다.
- 해당 키를 분리하는 방법으로는 환경 변수를 이용한 방법과 외부에 저장하는 방법 2가지가 있다.
  - 환경변수 패턴: SECRET_KEY의 값을 환경변수에 저장하여 참고한다.
  - 비밀파일 패턴: SECRET_KEY의 값을 별도 파일에 저장하여 참고한다.



## 외부에 저장하는 방법

1. secrets.json 생성

secrets.json 파일을 프로젝트 컨테이너 폴더에 생성해 준다. (manage.py와 같은 위치)



2. secrets.json 내용

```json
{
    "SECRET_KEY": "<Your Django SECRET KEY>"
}
```

secrets.json 파일은 이후 데이터 베이스 ID, PW 값 등 보안에 문제가 될 수 있는 정보들을 따로 분리하여 저장하는데 사용될 수 있다.



3. Settings.py

```python
SECRET_KEY = [SECRET_KEY]
```

 이 부분을 아래와 같이 바꿔준다.

```python
import json
import os
from django.core.exceptions import ImproperlyConfigured


secret_file = os.path.join(BASE_DIR, 'secrets.json')  # secrets.json 파일 위치 명시

with open(secret_file) as f:
    secrets = json.loads(f.read())


def get_secret(setting):
    """비밀 변수를 가져오거나 명시적 예외를 반환한다."""
    try:
        return secrets[setting]
    except KeyError:
        error_msg = "Set the {} environment variable".format(setting)
        raise ImproperlyConfigured(error_msg)


SECRET_KEY = get_secret("SECRET_KEY")
```



4. .gitignore 파일에 추가

```text
# .gitignore 파일

secrets.json
```

 .gitignore 파일에 setcrets.json 파일을 추가한다.



- .gitignore 파일이란?

 사용자가 원하지 않은 파일들을 자동적으로 git 커밋 대상에서 제외시켜주는 파일이다.

- 커밋 대상에서 제외시켜야 할 것들
  - IDE tool과 관련된 설정 파일
  - 언어의 빌드 결과물, 로그, 패키지 관련 파일
  - 그 외 프로젝트에서 사용자가 제외하기를 원하는 파일
  - etc.



# Django 한국 시간 설정

 Django에서의 기본 Time Zone(시간 설정)은 UTC이다. 따라서 우리는 시간을 한국 시간으로 설정해줄 필요가 있다.



 시간 설정은 settings.py 에서 해주면 된다.

```python
LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True
```

 이 부분을 아래와 같이 수정해주면 된다.

```python
LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'Asia/Seoul'    # 한국 시간 적용

USE_I18N = True

USE_L10N = True

USE_TZ = False  # False 로 설정해야 DB에 변경 된 TIME_ZONE 이 반영 됨
```



**Tip.**

 웹에서 CRUD 작업을 하다보면 보통 아래와 같이 생성 일자와 수정 일자 정보를 DB 스키마에 만들어서 저장하게 된다.

```python
from django.db import models

class TestModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)	# 생성 시간
    updated_at = models.DateTimeField(auto_now=True)	# 수정 시간
```

 여기서 auto_now_add 와 auto_now 의 차이점은 아래와 같다.

- 수정일자: auto_now=True 사용
  - auto_now=True는 django model의 데이터 값이 save 될 때마다 현재 날짜와 시간으로 갱신된다.
  - 주로 최종 수정 일자 field option으로 사용된다.

- 생성일자: auto_now_add=True 사용
  - auto_now_add=True는 django model의 데이터 값이 최초 저장(insert) 시에만 현재 날짜와 시간으로 적용된다.





# Migrate

 app을 설치하거나 변경사항이 있을 시, 이를 Django framework에 적용시켜주어야 한다. 이는 다음 명령어를 통해 적용시킬 수 있다.

```shell
$ python manage.py migrate
```





# 서버 실행하기

1. command 명령어 사용

```shell
$ python manage.py runserver
```



2. Run을 통해 서버 실행하기

- Run > Edit Configurations.. 클릭
- \+ > Python 클릭
- Name을 Runserver 등으로 작성
- Script path에서 mange.py 경로를 선택
- parameters에 runserver 입력





# 접속 호스트 변경

1. ALLOWED_HOSTS 부분 수정

 settings.py 파일에서 ALLOWED_HOSTS 부분을 아래와 같이 수정해준다.

```python
ALLOWED_HOSTS = ['*']
# or
# ALLOWED_HOSTS = ['ip', 'url']
```

 ALLOWED_HOSTS를 '*'로 설정하면 누구든 서버에 접속할 수 있게 하는 것이고, 특정 ip 혹은 url로 설정하면 해당 ip 혹은 url에서 접속하는 사람들만 서버에 접속할 수 있게 하는 것이다.



2. 서버 실행

 외부에서 서버에 접속할 수 있게 하려면 서버를 실행하는 명령어에 옵션을 추가해줘야 한다.

```shell
$ python manage.py runserver 0.0.0.0:8000
```

 Run을 통해 서버를 실행하였다면, Run Configrations에서 parameters를 "runserver"에서 "runserver 0.0.0.0:8000"으로 바꾸어 주어야 한다.





# REST framework 설치 및 실행

```shell
$ pip install djangorestframework
$ pip install markdown
$ pip install django-filter
```

 터미널에서 위 패키지들을 설치해준다.



 settings.py 파일에서 INSTALLED_APPS 부분을 찾아 아래와 같이 rest_framework를 추가시켜주고, 코드 마지막에 REST_FRAMEWORK를 정의해 준다.

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]

...

REST_FRAMEWORK = {
    # Use Django's standard `django.contrib.auth` permissions,
    # or allow read-only access for unauthenticated users.
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly'
    ]
}
```



 urls.py 파일에서 다음과 같이 경로를 url 경로를 추가해준다.

```python
from django.urls import inclue

urlpatterns = [
    ...
    path('api-auth/', include('rest_framework.urls')),
]
```





# App(앱) 추가

## App 생성

 앱 설치는 터미널에서 아래 명령어를 입력하여 할 수 있다.

```shell
$ python manage.py startapp [app_name]
```



 app을 설치하고 나서 settings.py의 INSTALLED_APP에 [app_name]을 등록해주어야 한다.

```python
INSTALLED_APPS = [
    ...
    '[app_name]',
]
```



## 모델 생성

 새로 만든 app의 models.py 파일에서 아래와 같이 사용할 class를 정의해 준다.

```python
class ModelName(models.Model):
    char_field = models.CharField(max_length=50)
    integer_field = models.IntegerField()
    created = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['created']
```

 모델을 만든 후, 가장 먼저 migration을 해주는 것이 좋다. migration 명령어는 다음과 같다.

```shell
$ python manage.py makemigrations
```





## Serializer 생성

 serializer는 Django에서 기본적으로 생성되는 파일이 아니다. 따라서 serializer.py 파일을 직접 만들어주어야 한다. serializer 는 다음과 같이 class Meta 에 사용할 모델이랑 사용할 필드를 적어주면 된다. serializer는 객체 데이터를 넣으면 설정한 필드만 JSON으로 바꿔주는 역할을 하게 된다.

```python
from rest_framework import serializers
from [App_name].models import ModelName

class ModelNameSerializer(serializers.ModelSerializer):
    class Meta:
        model = ModelName
        fields = ['field1', 'field2', ...]
```





## View 생성

 view.py에 위와 같이 수행해야 할 작업을 작성해준다.

```python
from django.shortcuts import render
from django.http import HttpResponse, JsonResponse
from django.views.decorators.csrf import csrf_exempt
from rest_framework.parsers import JSONParser
from addresses.models import Addresses
from addresses.serializers import AddressesSerializer

@csrf_exempt
def FunctionName(request):
    if request.method == 'GET':
        query_set = Addresses.objects.all()
        serializer = AddressesSerializer(query_set, many=True)
        return JsonResponse(serializer.data, safe=False)

    elif request.method == 'POST':
        data = JSONParser().parse(request)
        serializer = AddressesSerializer(data=data)
        if serializer.is_valid():
            serializer.save()
            return JsonResponse(serializer.data, status=201)
        return JsonResponse(serializer.errors, status=400)
```





## URL 생성

 urls.py 파일의 urlpatterns 부분에 사용할 url와 해당 url로 접속 시 실행될 작업을 작성해준다.

```python
from [app_name] import views as [app_name]_views

urlpatterns = [
    ...
    path('[url]', [app_name]_views.[FunctionName]),
]
```

