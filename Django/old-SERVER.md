
## 0. 설치 전 셋팅


### 0-1. yum repository 서버 변경

```
# sudo su
# yum install -y https://centos7.iuscommunity.org/ius-release.rpm
```


### 0-2. 컴파일할 yum 소스 설치

```
# yum install 'perl(Data::Dumper)' -y
# yum install perl perl-devel -y
# yum install -y cmake ncurses-devel openssl-devel libtool-ltdl expat-devel db4-devel
# yum install -y  gcc*
# yum install -y wget
# yum update -y
```


## 1. python3.6 설치


### 1-1. yum repository로 python 설치

```
# yum install -y python36u python36u-libs python36u-devel python36u-pip
```


### 1-2. 설치된 파이썬 버전확인 , 파이썬 설치경로 확인

```
# python3.6 -V
python 3.6.5
# which python3.6
/bin/python3.6
```


### 1-3. 파이썬 심볼릭링크 확인

```
# ls -l /bin/python*
```


### 1-4. 파이썬 심볼릭링크 3.6버전으로 이동

```
# ln -s /bin/python3.6 /bin/python3
# unlink /bin/python
# ln -s /bin/python3 /bin/python
# ln -s /bin/pip3.6 /bin/pip
```


### 1-!!.yum 명령어 사용시 python2.0으로 되돌려야함

```
# unlink /bin/python
# ln -s /bin/python2 /bin/python
```


## 2. apache-httpd 설치


### 2-1. 임의의 디렉토리 생성 후 이동

```
# mkdir /home/downloads
# cd /home/downloads
```


### 2-2. 존속성 패키지 - apr 설치


#### 2-2-1. apr 다운로드 후 압축풀기.

```
# wget http://archive.apache.org/dist/apr/apr-1.5.1.tar.gz
# sudo tar zxvf apr-1.5.1.tar.gz
# cd apr-1.5.1
```


#### 2-2-2. apr 컴파일

```
# ./configure
```


#### 2-2-3. 에러 발생 시 대처.

```
rm: cannot remove `libtoolT': No such file or directory
// 해당 에러문구 출력시 아래의 명령어로 해결 후 다시 ./configure를 진행한다.
# cp -arp libtool libtoolT
# ./configure
```


#### 2-2-3. apr 컴파일 재시도

```
# make
# make install
# cd ..
```


### 2-3. 존속성 패키지 - apr-util 설치


#### 2-3-1. apr-util 다운로드 후 압축풀기.

```
# wget http://archive.apache.org/dist/apr/apr-util-1.5.4.tar.gz
# sudo tar zxvf apr-util-1.5.4.tar.gz
# cd apr-util-1.5.4
```


#### 2-3-2. apr-util 컴파일

```
# ./configure --with-apr=/usr/local/apr
# make
# make install
# cd ..
```


### 2-4. 존속성 패키지 - pcre 설치


#### 2-4-1. pcre 다운로드 후 압축풀기

```
# wget https://sourceforge.net/projects/pcre/files/pcre/8.36/pcre-8.36.tar.gz
# sudo tar zxvf pcre-8.36.tar.gz
# cd pcre-8.36
```


#### 2-4-2. pcre 컴파일

```
# ./configure --prefix=/usr/local/pcre
# make
# make install
# cd ..
```


### 2-5. apahce 2.4.1 설치


#### 2-5-1. httpd-2.4.1 다운로드 후 압축풀기

```
# wget http://archive.apache.org/dist/httpd/httpd-2.4.10.tar.gz
# sudo tar zxvf httpd-2.4.10.tar.gz
# cd httpd-2.4.10
```


#### 2-5-2. httpd 컴파일

```
# sudo ./configure \
--prefix=/usr/local/apache \
--enable-http  \
--enable-info \
--enable-cgi \
--enable-so \
--with-pcre=/usr/local/pcre
# sudo make
# sudo make install
# cd ..
```


### 2-6. python 모듈 - mod_wsgi 설치


#### 2-6-1. mod_wsgi 다운로드 후 압축풀기

```
# wget https://pypi.python.org/packages/15/d4/83c842c725cb2409e48e2999e80358bc1dee644dabd1f3950a8dd9c5a657/mod_wsgi-4.5.24.tar.gz
# sudo tar zxvf  mod_wsgi-4.5.24.tar.gz
# cd mod_wsgi-4.5.24
```


#### 2-6-2. 셸 리눅스 임시 off

```
# setenforce 0
```


#### 2-6-3. apx관련 파일 수정

```
# vi /usr/local/apache/bin/apxs
- - - - - -
#!/replace/with/path/to/perl/interpreter -w
- >
#!/usr/bin/perl -w
```


#### 2-6-4. mod_wsgi 컴파일

```
# ./configure --with-python=/bin/python
# make
# make install
# cd ..
```


#### 2-6-5. 셀리눅스  on

```
# setenforce 1
```


### 2-7. 아파치 서비스 등록


#### 2-7-1. 심볼릭 링크 생성

```
# ln -s /usr/local/apache/bin/apachectl /etc/init.d/httpd
```


#### 2-7-2. service 파일 수정

```
# vi /etc/init.d/httpd
- -  - - - - -
#!/bin/sh
#
# Apache This starts and stops Apache.
#
# chkconfig: 35 20 80
# description: Apache Web Service
#
# Licensed to the Apache Software Foundation ...
```

실행시 시작

#### 2-7-3. 아파치 실행

```
# service httpd start
```


## 3. mysql 5.7.10


### 3-1. 계정추가

```
# groupadd -g 400 mysql
# useradd -u400 -g400 -d /usr/local/mysql -s /bin/false mysql
```


### 3-2. 소스 다운로드 및 압축풀기

```
# wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.14.tar.gz
# sudo tar zxvf mysql-5.7.14.tar.gz
# cd mysql-5.7.14
```


### 3-!! 메모리 1G 서버일 경우 메모리 스왑

```
# dd if=/dev/zero of=/var/swapfile bs=1k count=3072000
# mkswap /var/swapfile
# swapon /var/swapfile
# swapon -s
```


### 3-3. mysql 5.7.14 컴파일 설치

```
# cmake \
-DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
-DWITH_EXTRA_CHARSETS=all \
-DMYSQL_DATADIR=/usr/local/mysql/data \
-DENABLED_LOCAL_INFILE=1 \
-DDOWNLOAD_BOOST=1 \
-DWITH_BOOST=/usr/include/boost \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_PARTITION_STORAGE_ENGINE=1 \
-DWITH_FEDERATED_STORAGE_ENGINE=1 \
-DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
-DWITH_MYISAM_STORAGE_ENGINE=1 \
-DENABLED_LOCAL_INFILE=1 \
-DMYSQL_UNIX_ADDR=/tmp/mysql.sock \
-DSYSCONFDIR=/etc \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DWITH_EXTRA_CHARSETS=all
# make
# make install
```


### 3-4. 환경설정

```
# cd /usr/local/mysql
# sudo chown -R mysql:mysql /usr/local/mysql
# sudo chmod 700 /usr/local/mysql/support-files/mysql.server 
# cp -s /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld
```


### 3-5. my.cnf 파일 수정

```
# mv /etc/my.cnf /etc/my.cnf.bak
# vi /etc/my.cnf
- - - - - - - -
[client]
default-character-set = utf8
port = 3306
socket = /tmp/mysql.sock
default-character-set = utf8
[mysqld]
socket=/tmp/mysql.sock
datadir=/usr/local/mysql/data
basedir = /usr/local/mysql
#user = mysql
#bind-address = 0.0.0.0
#
skip-external-locking
key_buffer_size = 384M
max_allowed_packet = 1M
table_open_cache = 512
sort_buffer_size = 2M
read_buffer_size = 2M
read_rnd_buffer_size = 8M
myisam_sort_buffer_size = 64M
thread_cache_size = 8
query_cache_size = 32M
#dns query
skip-name-resolve
#connection
max_connections = 1000
max_connect_errors = 1000
wait_timeout= 60
#slow-queries
#slow_query_log = /usr/local/mysql/data/slow-queries.log
#long_query_time = 3
#log-slow-queries = /free/mysql_data/mysql-slow-queries.log
##timestamp
explicit_defaults_for_timestamp
symbolic-links=0
### log
log-error=/usr/local/mysql/data/mysqld.log
pid-file=/tmp/mysqld.pid
###chracter
character-set-client-handshake=FALSE
init_connect = SET collation_connection = utf8_general_ci
init_connect = SET NAMES utf8
character-set-server = utf8
collation-server = utf8_general_ci
symbolic-links=0
##Password Policy
#validate_password_policy=LOW
#validate_password_policy=MEDIUM
### MyISAM Spectific options
default-storage-engine = myisam
key_buffer_size = 32M
bulk_insert_buffer_size = 64M
myisam_sort_buffer_size = 128M
myisam_max_sort_file_size = 10G
myisam_repair_threads = 1
### INNODB Spectific options
#default-storage-engine = InnoDB
#skip-innodb
#innodb_additional_mem_pool_size = 16M
#innodb_buffer_pool_size = 1024MB
#innodb_data_file_path = ibdata1:10M:autoextend
#innodb_write_io_threads = 8
#innodb_read_io_threads = 8
#innodb_thread_concurrency = 16
#innodb_flush_log_at_trx_commit = 1
#innodb_log_buffer_size = 8M
#innodb_log_file_size = 128M
#innodb_log_files_in_group = 3
#innodb_max_dirty_pages_pct = 90
#innodb_lock_wait_timeout = 120
[mysqldump]
default-character-set = utf8
max_allowed_packet = 16M
[mysql]
no-auto-rehash
default-character-set = utf8
[myisamchk]
key_buffer_size = 256M
sort_buffer_size = 256M
read_buffer = 2M
write_buffer = 2M
```


### 3-6. 데이터베이스 생성

```
# /usr/local/mysql/bin/mysql_install_db --user=mysql --datadir=/usr/local/mysql/data
```


### 3-7. 초기 root 비밀번호 확인

```
# cat /root/.mysql_secret
# service mysqld start
```


### 3-*. 비밀번호 복잡성 해제 * 패키지 설치일 경우

```
# cd /usr/lib64/mysql/plugin/
# mv validate_password.so validate_password.so.bak
```


### 3-8. 데이터베이스 접속 후 비밀번호 변경

```
# /usr/local/mysql/bin/mysql -u root -p
mysql> alert user ‘root’@‘localhost’ identified by ‘변경할비밀번호’;
mysql> flush privileges;
mysql> \q;

# /usr/local/mysql/bin/mysql -u root -p
mysql> \s
--------------
/usr/local/mysql/bin/mysql  Ver 14.14 Distrib 5.7.14, for Linux (x86_64) using  EditLine wrapper

Connection id:		3
Current database:	
Current user:		root@localhost
SSL:			Not in use
Current pager:		stdout
Using outfile:		''
Using delimiter:	;
Server version:		5.7.14 Source distribution
Protocol version:	10
Connection:		Localhost via UNIX socket
Server characterset:	utf8
Db     characterset:	utf8
Client characterset:	utf8
Conn.  characterset:	utf8
UNIX socket:		/tmp/mysql.sock
Uptime:			7 min 15 sec

Threads: 1  Questions: 9  Slow queries: 0  Opens: 114  Flush tables: 1  Open tables: 39  Queries per second avg: 0.020
--------------
mysql> \q;
```


## 4. django 설치


### 4-1. pip로 django 설치

```
# pip install --upgrade pip
# pip install django==1.8
```


### 4-2. django 프로젝트 생성

```
# cd /home/centos
// . 까지 넣어주어야함.
# django-admin startproject mysite .
```
