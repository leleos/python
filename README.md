## Python 爬虫

### 基本安装
+ 本实例，1台CentOS服务器+1台本地win10
+ 安装PyCharm 开发工具

#### 安装Python 3.7
+ 本地安装Python3.7 环境。
```shell
https://www.python.org/ftp/python/3.7.1/python-3.7.1-amd64.exe  （win10）

https://www.python.org/ftp/python/3.7.1/python-3.7.1-macosx10.9.pkg （Mac）
```
+ PyCharm 会报R错误，可选安装R语言
```shell
https://mirrors.tuna.tsinghua.edu.cn/CRAN/bin/windows/base/R-3.5.1-win.exe
```
+ CentOS下安装
```shell
wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tar.xz
xz -d Python-3.7.1.tar.xz
tar xvf Python-3.7.1.tar.xz
解压到 python371
```
```shell
wget https://www.openssl.org/source/openssl-1.1.1.tar.gz
tar zxvf openssl-1.1.1.tar.gz
解压到 openss-1.1.1
```
+ 安装编译环境 gcc-c++等
```shell
yum install -y  libffi-devel  gcc-c++  zlib*  bzip2  sqlite*
```
+ 安装ssl
```shell
cd openssl-1.1.1/

./config --prefix=/usr/local/openssl

make
make install
```
```shell
cd /usr/local
ldd /usr/local/openssl/bin/openssl
会有not found
```
```shell
mv /usr/bin/openssl /usr/bin/openssl.old
ln -s /usr/local/openssl/bin/openssl /usr/bin/openssl
echo "/usr/local/openssl/lib/" >> /etc/ld.so.conf
ldconfig -v

reboot 
```
重启之后
```shell
ldd /usr/local/openssl/bin/openssl

openssl version -a
```
查看版本，显示
OpenSSL 1.1.1  11 Sep 2018

+ 安装Python3.7
```shell
目标安装在我的用户名下的目录python3
cd 
mkdir python3
我的路径:/home/seven/python3
./configure --prefix='/home/seven/python3' --with-openssl=/usr/local/openssl/
make
make install
```

+ 配置环境变量
```shell
vim .bashrc

最后添加两行
alias python3=/home/seven/python3/bin/python3.7
alias pip3=/home/seven/python3/bin/pip3
```


#### 安装Scrapy
+ 先安装 Twisted
```shell
https://files.pythonhosted.org/packages/5d/0e/a72d85a55761c2c3ff1cb968143a2fd5f360220779ed90e0fadf4106d4f2/Twisted-18.9.0.tar.bz2

```
再安装 Scrapy
```shell
pip3 install scrapy
```

```shell
vim .bashrc

alias scrapy=/root/python3/bin/scrapy
```

#### 安装mongodb
```shell
touch /etc/yum.repos.d/mongodb-org-4.0.repo 
```
文件内容
```shell
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
```
```shell
yum install -y mongodb-org
```
```shell
vim /etc/mongod.conf
修改 bindIP
0.0.0.1
```
```shell
firewall-cmd --zone=public --add-port=27017/tcp --permanent
firewall-cmd --reload
systemctl restart firewalld
```


#### 安装支持

```shell
pip3 install pymongo
```

### 开发

#### 创建项目

```shell
scrapy startproject toutiao

cd toutiao
cd toutiao
cd spiders
scrapy genspider toutiao_spider
scrapy genspider toutiao_spider www.xxx.com
```

#### 基于pycharm编写

pycharm 需要安装两个插件

scrapy
pypiwin32

#### 运行
```shell
scrapy crawl toutiao_spider
```

#### 导出
```shell
scrapy crawl toutiao_spider -o hot.csv
```

#### 编写Mongo数据

#### 

```shell
use toutiao
show collections
db.hotnews.find().pretty()
```






