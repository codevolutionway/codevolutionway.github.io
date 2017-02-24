---
title: Centos6.5+CDH5
date: 2017-02-24 16:58:29
tags:
---


# 坑位
## python依赖
cdh依赖东西很多，一步一坑，一坑一晚。。。

> http://blog.druggo.org/post/2015/01/18/%E8%A3%85CDH5%E7%9A%84%E5%87%A0%E4%B8%AA%E5%9D%91
> https://my.oschina.net/lgscofield/blog/408164

* centos6.x cdh5依赖python2.7，需要多版本python支持

Processing Dependency: libpython2.7.so.1.0()(64bit)
> http://stackoverflow.com/questions/26597527/how-to-install-libpython2-7-so

How to install libpython2.7.so 但是没解决这个坑！！！
this problem is 【How to install libpython2.7.so】

> https://ruiaylin.github.io/2014/12/12/python%20update/

## Processing Dependency: /lib/lsb/init-functions for package:
cloudera-manager-agent-5.5.2-1.cm552.p0.16.el7.x86_64

先删除目录，再安装redhat-lsb-core
```
rmdir /lib/lsb/init-functions
yum install redhat-lsb-core
```

## 主机名称
```
vi /etc/sysconfig/network
vi /etc/hosts
```

# 命令
```
#cm服务
service cloudera-scm-server status
service cloudera-scm-agent restart
```
# MARK
可参考博客

# 下载
> http://mirror.bit.edu.cn/apache/hadoop/common/
> http://mirrors.cnnic.cn/apache/hadoop/common/

Hadoop安装完后，启动时报Error: JAVA_HOME is not set and could not be found.
解决办法：
        修改/etc/hadoop/hadoop-env.sh中设JAVA_HOME。
        应当使用绝对路径。
        export JAVA_HOME=$JAVA_HOME                  //错误，不能这么改
        export JAVA_HOME=/usr/java/jdk1.6.0_45        //正确，应该这么改

引用
> http://www.powerxing.com/install-hadoop-simplify/