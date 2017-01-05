---
title: Oracle中的union和join
toc: true
date: 2017-01-03 22:39:53
tags: [Oracle, 数据库, SQL]
categories: 
- Oracle
---
有时候，我们需要把很多表的查询结果给合并在一起显示或者导出，有时候呢我们又需要几张表联合一些条件进行查询，所以我们常会用到**join**和**union**语句。
<!--more-->
# left join
举个例子
有一个属地代码表md_area(areano, name)。
有一个用户表users(mdn,areano,....)。
我现在要统计users表中各属地的用户数，还要根据代码显示出属地名称，以便更加直观的进行统计。
```sql
	select area, areaname, ct from
		(select areano as area, count(*) as ct from users group by areano) t1
		left join 
		(select areano, name as areaname from md_area t2) on t2.areano = t1.area;
```

