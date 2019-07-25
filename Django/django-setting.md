**개인 리포지토리의 REAME.md에 등록된 내용입니다.**
[yuniithings.com](https://github.com/yuniithings/yuniithings.com)

# 서버셋팅
**ec2의 아마존리눅스 기반의 설정방법입니다.**

## 1. apache, mysql, python 설치
```linux
$ sudo yum install -y httpd24-* mysql57-* python36-*
```

### 1-1. python3 bash에 등록

`$ vi /home/ec2-user/.bashrcalias`에 alias 추가
```bash
# User specific aliases and functions
alias python="/usr/bin/python36"
```
ssh 재접속 후 `$ which python`으로 python36이 제대로 연결되었는지 확인한다.<br>
__alias를 확인하지 않으면 pip명령어 사용할때 python2 버전으로 실행되서 에러가 발생한다.__


## 2. Django 셋팅

### 2-1. pip로 장고 설치하기
```linux
$ sudo python3 -m pip install --upgrade pip
$ python3 -m pip install django~=2.0.0
```
`django~=2.0.0` 부분은 원하는 버전으로 치환하여 사용해도 된다.
```linux
$ mdkir [dir]
$ cd [dir]
$ django-admin startproject [projectname] .
```
`[dir]`과 `[projectname]`은 원하는 네이밍을 사용하면 된다. **대괄호는 빼고..**<br>
`[projectname]` 뒤의 `.`을 붙이지 않는다면 `[projectname]/[projectname]`에 해당 app의 cofig파일들이 생성된다.<br>
이 repository는 `[projectname]/[projectname]`으로 생성되어있다.

```linux
$ python3 manage.py startapp [appname]
```
manage.py가 있는 `/home/ec2-user/[dir]/[projectname]`경로에서 실행해주세요.

### 2-2. apache에 python 셋팅

apahce가 python을 읽어낼수 있도록 mod_wsgi 모듈을 설치한다.
```linux
$ sudo yum install -y mod24_wsgi-python36
```
**ami의 yum repository는 너무나 방대해서 설치가 간편하다.**<br>

`$ sudo vi /etc/httpd/conf.d/django.conf`로 host를 설정할 conf파일을 생성한다.

```bash
<VirtualHost *:80>
        WSGIScriptAlias / /home/ec2-user/[dir]/[projectname]/wsgi.py

        DocumentRoot /home/ec2-user/[projectname]
        ServerName [cname].[domain]
        
        # apache로그 경로 및 네이밍은 마음대로 작성해도 된다.
        # 해당 코드로 실행 시 로그가 작성되는 경로는 /etc/httpd/logs/ 이다.
        ErrorLog "logs/[cname]-error-log"
        CustomLog "logs/[cname]-access-log" common
        
        # wsgi.py가 있는 폴더의 경로를 넣어주세요.
        <Directory /home/ec2-user/[dir]/[projectname]>
                <Files wsgi.py>
                        Order deny,allow
                        Require all granted
                </Files>
        </Directory>

        <Directory /home/ec2-user/[dir]/[projectname]>
                Options FollowSymLinks
                AllowOverride FileInfo
                Order allow,deny
                Require all granted
        </Directory>

</VirtualHost>
```
추가적인 vhost 설정을 원한다면 같은 내용을 복붙해서 대괄호[] 안의 내용을 바꿔 사용하면된다.
yum으로 설치한 apache의 경우, 기본 conf 파일에 conf.d 폴더의 모든 .conf파일을 풀러오기 때문에 추가적인 설정은 하지 않아도 된다.

**한글 파일 경로 읽을수 있게 설정하기**
`$ sudo vi /etc/sysconfig/httpd`에 아래 내용 추가
```bash
export LANG=‘en_US.UTF-8’
export LC_ALL=‘en_US.UTF-8’
```

[wsgi.py](https://github.com/yuniithings/yuniithings.com/blob/master/adminApp/adminApp/wsgi.py)는 해당 repository의 파일처럼 설정해주세요. `adminApp.settings` 를 `[projectname].settings`로 바꿔주기만 하면 됩니다.


### 2-3. 기존 DB의 테이블 연결하기
**mysql5.7버전의 기초 셋팅이 되어있어야 합니다.**
mysqlclient를 설치한다.
```linux
$ sudo python3 -m pip install mysqlclient
```


settings.py에 DB 접속정보 등록하기
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'OPTIONS': {
            'read_default_file': '/etc/my.cnf'
        }
    }
}
```
`/etc/my.cnf`에 접속정보를 등록합니다.
```bash
[client]
default-character-set=utf8
database = [database schema]
host = [host]
user = [user]
password = [password]
```

데이터베이스 마이그레이션을 실행해줍니다.
```linux
$ python3 manage.py inspectdb > [appname]/models.py
$ python3 manage.py makemigrations
$ python3 manage.py migrate
```
manage.py가 있는 `/home/ec2-user/[dir]/[projectname]`경로에서 실행해주세요.