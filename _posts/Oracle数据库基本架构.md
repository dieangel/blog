---
title: Oracle数据库基本架构
date: 2016-10-31 15:05:45
tags: Oracle
categories: Oracle
toc: true
---
ORACLE数据库服务器由物理存储的数据库及一个数据库实例组成(包括分配的内存区域、运行的进程等)。多数时候我们管理数据库并不再在意它的物理架构，而只在意它的逻辑架构。但是，对物理架构的了解会让你更容易进行管理好数据库。
<!--more-->
# 1、数据库的物理存储
## 数据文件(data file)
每个库有一个或多个数据文件(data file)，包括了数据库中的所有数据。
可以通过 `v$datafile dba_data_files` 进行查看
## 控制文件(control file)
每一个 Oracle 数据库都有控制文件（control file）。 控制文件包含元数据指定的数据库的物理结构，包括有数据库名称、数据库文件的名称和存储位置。
可以通过`v$controlfile`进行查看。
## 在线重做日志文件(online redo log file)
每一个 Oracle 数据库都有在线重做日志（online redo log），包含两个或多个在线重做日志文件（online redo log files）的集合。在线重做日志（redo log）由重做条目（或者称作重做记录（redo records）） 构 成 ， 其 中记录了所有数据的改变。 在数据恢复操作中，在线重做日志是最重要的。
相关视图：`v$log v$logfile`
## 存档重做日志文件(archived Redo Log)
对比Online，这是将一个或多个充满了的Online Log进行离线存储，数据库运行在ARCHIVELOG  mode下由archiving进程处理

# 2、数据库的逻辑存储结构
数据库的逻辑存储结构从大到小依次可为：表空间->段->区->数据块。  
每个数据库都会分配一个表空间。    
表空间至少包含一个数据文件(data file)。表空间是段逻辑上的容器。  
段则是区的集合，用来分配给用户的对象、撤销数据(undo data)、临时数据。  
数据库在表空间中使用数据段(data segment)来保存表中数据。一个段包含由数据块(data blocks)组成的扩展区(extents)。  
可以通过如下表或视图来查看信息。  
```
v$tablespace
v$datafile
v$tmpfile
dba_tablespaces, user_tablespaces
dba_free_space, user_free_space
dba_segments, user_segments
```
