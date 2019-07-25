# django-custom_tags.md


### custom_tags
우리가 template단에서 사용할 tag나 filter를 등록하는 부분이다.<br/>
template별로 공통적으로 사용할 데이터들을 호출하거나 , 별도의 연산이 필요한 부분을 tag나 filter로 만들어두는 부분이다.<br/>
일종의 custom library로 생각하면된다.

### custom_tags.py 생성
`python manage.py startapp [appname]`으로 생성했던 app directroy에 만들어준다.<br/>
`[appname]/templatetags`패키지를 생성한다.<br/>
패키지이기 때문에 templatetags directory내에 `__init__.py`파일이 필요하다.<br/>
패키지 내에 `custom_tags.py` 파일을 생성한다.

#### 파일 작성하기

```python
# custom_tags.py
from django import template

register = template.Library()
```
템플릿 라이브러리에 등록한다고 상단에 코드를 작성한다.

### tag 만들기
```python
@register.inclusion_tag('common/paging.html', takes_context=True)
def custom_paging(context):
    paging_context = context
    
    return paging_context
```
html을 포함한 paging custom_tags의 예제이다.<br/>
template으로 전달되는 context를 take하지 않으려면 take_context 옵션을 기재하지 않으면 된다.<br/>
full code가 궁금하다면 [이곳](https://github.com/yuniithings/yuniithings.com/blob/master/adminApp/admin/templatetags/custom_tags.py)으로..
**django.core의 pagination을 사용하면 더 편리하다.**<br/>


### tag 사용하기
```html
{% load custom_tags %}

{% custom_paging %}
``` 
load 명령어로 costom_tags를 불러오고, 해당 함수를 사용하면 된다.<br/>
custom_tags를 파일별로 세분화하고 싶으면, templatetags 패키지 내에서 세분화시켜놓으면 된다.


### filter 작성하기
```python
@register.filter
def custom_lower(value):
    value = value.lower()
    return value
```
filter는 decoration이 다르다.<br/>
lower는 django-default-tag로 제공되지만, 사용의 이해를 위해 작성하였다.


### filter 사용하기
```html
{% load custom_tags %}

{{ context | custom_lower }}
```
load 명령어로 costom_tags를 불러오고, 해당 함수를 사용하면 된다.<br/>
`{{ 변수명 | custom_filter }}`의 형식이다. 예제로 설명하면 `{{ value | custom_lower }}` 인 셈이다.

