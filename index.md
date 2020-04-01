## Section1 Centos配置Python3环境
```
## Yum初始化配置
-- sudo yum update
-- sudo yum upgrade
## 基本Yum依赖包
-- yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make
-- yum install libffi-devel -y
## 下载Python3.7
-- Windows下载再用SSH传到Linux中：
  打开python的官方网站：https://www.python.org/  -->Downloads-->Source code-->Latest Python 3 Release - Python 3.7.0-->拉到最下面，选择Gzipped source tarball，下载到本地，然后上传到服务器即可。
-- Linux直接安装：
wget https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tgz
## 解压安装Python3.7
-- tar -zxvf Python-3.7.0.tgz
-- cd Python-3.7.0
-- ./configure
-- make&&make install
## 配置环境变量
-- mv /usr/bin/python /usr/bin/python.bak
-- ln -s /usr/local/bin/python3 /usr/bin/python
-- mv /usr/bin/pip /usr/bin/pip.bak
-- ln -s /usr/local/bin/pip3 /usr/bin/pip
## 验证Python3及pip
-- 直接输入python以及pip -V 验证python版本是否正确
## 配置yum
yum是依赖python2.7,为此改为python默认python3后要将yum重指定为python2.7
-- vim /usr/libexec/urlgrabber-ext-down 修改第一行为/usr/bin/python2.7
-- vi /usr/bin/yum 修改第一行为/usr/bin/python2.7
```

## Section2 Centos配置基本Django环境
```
## 升级pip
-- pip install --upgrade pip
## 安装Django
-- pip install django
## 安装基本依赖包
-- pip install pymysql
-- pip install django-filter djangorestframework Pillow sqlparse 
## 安装mysqlclient
-- 先安装mysql环境，按照section3指示
-- yum install gcc mariadb-devel
-- yum install mysql-devel gcc gcc-devel python-devel
-- pip install mysqlclient

```

## Section3 Centos配置Mysql环境
```
## 配置命令如下
-- sudo yum localinstall https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm 
-- yum install mysql-community-server 
-- sudo systemctl enable mysqld 
-- sudo systemctl start mysqld 
-- sudo systemctl status mysqld 
-- sudo grep 'temporary password' /var/log/mysqld.log 
-- sudo mysql_secure_installation 
-- mysql -u root -p
```
## Section4 Centos配置Hadoop+Sqark+HIVE环境
```
### 配置yum
-- sudo yum -y update
-- sudo yum -y upgrade
-- sudo yum groupinstall -y development
-- sudo yum install -y java-1.8.0-openjdk net-tools rsync mlocate wget vim \
	gcc zlib-dev openssl-devel sqlite-devel bzip2-devel python-devel
### set Java
-- echo 'export JAVA_HOME=/usr/lib/jvm/jre' >> /etc/profile.d/java.sh
-- echo 'export PATH=/usr/lib/jvm/jre/bin:$PATH' >> /etc/profile.d/java.sh

### sshkey
-- sudo ssh-keygen -t rsa -f ~/.ssh/id_rsa

### hadoop 
-- tar xzf /vagrant/files/hadoop-2.7.7.tar.gz
-- mv hadoop-2.7.7 /usr/local/hadoop
-- cp /vagrant/conf/hadoop/hadoop.sh /etc/profile.d/
-- cp /vagrant/conf/hadoop/* /usr/local/hadoop/etc/hadoop

### Hive 
-- tar xzf /vagrant/files/apache-hive-2.1.1-bin.tar.gz
-- mv apache-hive-2.1.1-bin /usr/local/hive
-- cp /vagrant/conf/hive/hive.sh /etc/profile.d/
-- cp /vagrant/conf/hive/* /usr/local/hive/conf

### Spark
-- tar xzf /vagrant/files/spark-2.4.5-bin-hadoop2.7.tgz
-- mv spark-2.4.5-bin-hadoop2.7 /usr/local/spark
-- cp /vagrant/conf/spark/spark.sh /etc/profile.d/
-- cp /vagrant/conf/spark/* /usr/local/spark/conf

### 处理.sh文件格式
-- 设置完之后会出现bash错误，因为windows下的换行符是\r\n，而linux下的换行符是\n
-- yum install dos2unix
-- cd /etc/profile.d/
-- dos2unix hadoop.sh
-- dos2unix spark.sh
-- dos2unix hive.sh
ps. 若出现了bash错误导致大部分linux命令都无法使用时：
-- 加入临时变量(重启后消失
	export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
-- 修改profile文件：
	vi /etc/profile
	加入：export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin



# set hosts
-- echo '10.211.55.100 master' >> /etc/hosts
-- echo '10.211.55.101 node1' >> /etc/hosts
-- echo '10.211.55.102 node2' >> /etc/hosts

## 配置master节点
-- cd /bin/bash
-- wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
-- rpm -ivh mysql57-community-release-el7-9.noarch.rpm
-- yum install -y mysql-server mysql-connector-java 
-- systemctl enable mysqld 
-- ln -s /usr/share/java/mysql-connector-java.jar $HIVE_HOME/lib/mysql-connector-java.jar
-- curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
-- python get-pip.py
-- pip install numpy pandas ipython[all] jupyter virtualenv

```
