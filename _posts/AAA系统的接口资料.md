---
title: AAA系统的接口资料
toc: true
date: 2016-12-23 10:06:19
tags: [AAA]
categories: Work
---
用来进行快速的接口操作。
<!--more-->
# Socket接口
## 电信
**host:interface2
path:/data/lcims/gzdx_lcbmi80/test
cmd:
**
```java
LANG=zh_CN.gb18030;export LANG

JAVA_HOME="/opt/java1.5"

${JAVA_HOME}/bin/java  -classpath .:../classes SocketClient 10.25.79.98 5902 ./20161223.txt
```
20161223.txt 为记录列表，每行一条操作记录，字段构造方式参考接口协议。

## 广电
**测试环境**
- 主机: 10.4.1.21:8008
- 目录:/data/lcims/gzgd_lcbmi80
- 连接类型：短连接

```
	##des3
	#openUserNum
	expirenum=65ec74e934aa87c1
	#yyyymmdd
	expiretime=37bf59c1ddbdeef7
```
修改为:
```
	10000  expirenum=29d21ca07eb0c66c
	20161211  expiretime=f282e0d777b3095c
```
# 常用报文

**开客户**

	1|||1|||P01=zgxtest0003|||P04=000|||M07=000205|||M32=boss
**lan开户**

	4|||1|||P01=zgxtest0003|||M02=492922|||M04=000205|||M05=3|||M06=10|||M10=8|||U12=1|||M15=0|||U38=0|||U23=bozs|||U24=5120|||U29=1024
**lan销户，status=2**

	4|||3|||P01=zgxtest0001|||U23=boss
**lan复机**

	4|||4|||P01=zgxtest0001|||U23=boss
**lan修改**

	4|||5|||P01=zgxtest0001|||U11=34324324|||U23=web
**lan查询**

	4|||21|||P01=zgxtest0001|||U97=M04,U12,M10,U11,M15,U24,U29
**lan欠费停机**

	4|||20|||P01=zgxtest0001|||U23=boss
**lan验证用户密码**

	4|||31|||P01=zgxtest0001|||M02=247104
**认证失败查询**

	41|||21|||M01=zgxtest0001|||U08=20161205##20161205|||U97=M01,U08,U10**

**认证成功查询**

	42|||21|||M01=zgxtest0001|||U08=20161205##20161205|||U97=M01,U03,U07,U08**

**在线查询**

	91|||21|||M01=zgxtest0001|||U97=U06,U05,U14,U08
**在线删除**

	91|||7|||M01=zgxtest0001|||M03=201|||U20=boss
**用户删除**

	4|||7|||P01=zgxtest0001|||U23=test
