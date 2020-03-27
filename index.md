## Section1 Centos配置Python3环境

```
# 安装Yum依赖
## Yum初始化配置
1. sudo yum update
2. sudo yum upgrade
## 基本Yum依赖包
1. yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make
2. yum install libffi-devel -y
## 下载Python3.7
-- Windows下载再用SSH传到Linux中：
  打开python的官方网站：https://www.python.org/  -->Downloads-->Source code-->Latest Python 3 Release - Python 3.7.0-->拉到最下面，选择Gzipped source tarball，下载到本地，然后上传到服务器即可。
-- Linux直接安装：
wget https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tgz
## 解压安装Python3.7
1. tar -zxvf Python-3.7.0.tgz
2. cd Python-3.7.0
3. ./configure
4. make&&make install
## 配置环境变量
1. mv /usr/bin/python /usr/bin/python.bak
2. ln -s /usr/local/bin/python3 /usr/bin/python
3. mv /usr/bin/pip /usr/bin/pip.bak
4. ln -s /usr/local/bin/pip3 /usr/bin/pip
## 验证Python3及pip
-- 直接输入python以及pip -V 验证python版本是否正确
## 配置yum
yum是依赖python2.7,为此改为python默认python3后要将yum重指定为python2.7
-- vim /usr/libexec/urlgrabber-ext-down 修改第一行为/usr/bin/python2.7
-- vi /usr/bin/yum 修改第一行为/usr/bin/python2.7
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Liamleeee/Liamleeee.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
