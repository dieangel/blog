---
title: AAA系统的报表生成脚本
toc: true
date: 2016-12-07 11:29:32
tags: [Oracle, Work]
categories: Work
---
系统是利用定时任务部署脚本，调用__sqlplus__命令执行一系列的操作后生成报表的。分为日任务、周任务、月任务。
<!--more-->
# 定时任务的安排
任务部署在__lcimsdb2__主机上，先看一下统计的任务列表

    10 1 * * * sh /data1/lcims/tj/stat_sh/day_run.sh >> /data1/lcims/tj/log/stat.log.`date +\%Y\%m\%d`
    30 0 2 * * sh /data1/lcims/tj/stat_sh/month_run.sh >> /data1/lcims/tj/log/month.log.`date +\%Y\%m\%d`
    0 4 8 * * sh /data1/lcims/tj/stat_sh/month_downreason_run.sh >> /data1/lcims/tj/log/tmp.log.`date +\%Y\%m\%d`
    0 4 15 * * sh /data1/lcims/tj/stat_sh/month_downreason_run.sh >> /data1/lcims/tj/log/tmp.log.`date +\%Y\%m\%d`
    0 4 22 * * sh /data1/lcims/tj/stat_sh/month_downreason_run.sh >> /data1/lcims/tj/log/tmp.log.`date +\%Y\%m\%d`
    0 4 1 * * sh /data1/lcims/tj/stat_sh/month_downreason_run.sh >> /data1/lcims/tj/log/tmp.log.`date +\%Y\%m\%d`
    10 0 * * * sh /data1/lcims/tj/stat_sh/loginusernum.sh >> /data1/lcims/tj/log/loginusernum.log.`date +\%Y\%m\%d`
    20 0 1 * * sh /data1/lcims/tj/stat_sh/loginusernum_month.sh >> /data1/lcims/tj/log/loginusernum_month.log.`date +\%Y\%m\%d`
    0 6 * * * sh /data1/lcims/tj/stat_sh/tj_active_user.sh >> /data1/lcims/tj/log/tj_active_user.log 2>&1

## day_run.sh 脚本
__工作流程：__  
**当前日期：20161207**  
1. 获取昨天日期`yesterday`(20161206,yyyymmdd格式)。  
2. **客户统计** 执行`./customer_number.sh yesterday user pwd dblink`   
3. **用户统计** 执行`./user_number.sh yesterday user pwd dblink`  
4. **用户到达** 执行`./total_number.sh yesterday user pwd dblink`  
5. **前天/昨天数据准备** 执行`./detail_tmp.sh yy mm dd user pwd dblink`  
6. **按组别、属地统计周期内使用用户数、总次数、时长、费用、出入流量** 执行`./login user pwd dblink`  
7. **分小时统计** 执行`./day_login.sh user pwd dblink`  
8. **分段统计登录次数** 执行`./day_login_times.sh user pwd dblink`   
9. **分段统计登录时长** 执行`./day_login_timelen.sh user pwd dblink`   
10. **分小时统计在线数** 执行`./day_online.sh user pwd dblink`  
11. **异常掉线统计** 执行`./downreason.sh user pwd dblink`  
12. **周报表** 执行`./week_login.sh user pwd dblink`  
13. **WLAN统计** 执行`./day_run_wlan_tj_detail.sh user pwd dblink`  

其中数据比较大的就是 __detail\_tmp__脚本，其工作流程是：  
1. __TJ\_DETAIL\_TMP\_B[efore]__ 表中删除 `detdate`小于__yesterday - 2(20161206 - 2 = 20161204) __的记录（每次50000行）  
2. 将__TJ\_DETAIL\_TMP\_Y[esterday]__表中数据插入到 **TJ\_DETAIL\_TMP\_B** （当前存放的是5号的数据）。  
3. `truncate` 表 **TJ\_DETAIL\_TMP\_Y**。  
4. 将昨天（20161206）表 **B\_BROADBAND\_DET`12`\_`06``** 中的数据插入 **TJ\_DETAIL\_TMP_Y** 。

之后的几个统计脚本数据都基于表 **TJ\_DETAIL\_TMP\_B**。 
 
