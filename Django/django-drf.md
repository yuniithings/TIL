# django-drf.md


## django-rest-framework
drf는 django로 첫 웹사이트를 제작하며 첫 멘붕을 안겨준 친구입니다.<br/>
첫 웹사이트의 계획은 back-end(django) + front-end(react)의 결합으로 멋진 웹사이트를 만들고 싶었지만, 
drf의 벽은 아직 django의 발걸음도 떼지 않은 저에게 큰 벽이었습니다.<br/>
drf를 꼭 사용할수 있도록..

## drf install
```linux
$ sudo python3 -m pip install djangorestframework
```

## settings.py에 drf 추가
```python
INSTALLED_APPS = [
    ...,
    'rest_framework',
]
```