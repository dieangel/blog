---
title: Kindle越狱操作
date: 2016-11-12 08:29:55
tags: [Kindle, 越狱, 阅读]
toc: true
categories: Device
---
前不久女朋友送了个Kindle Voyage，不过用来看pdf文档实在是不好看，寻思良久，网络上果然有狱越之法，遂记录之，以备固件升级重装之用。
<!--more-->
# 可升级固件
当前固件版本已经升级到了5.8.5.0.2，这是不能升级的，需要手刷到低版本的固件，待越狱成功后，再手刷高版本的固件，这样越狱不会消失。  
[可升级固件下载地址](https://kindlefere.com/post/410.html)   
下载解压得到`.bin`文件放到kindle根目录下，断开USB连接，`菜单->设置->菜单->更新你的Kindle`更新重启即可。   
接下来你可以选择自动推送升级，或者自己手刷升级。  
[所有固件下载地址](https://kindlefere.com/update)
# 安装KUAL插件程序及插件包
安装了这个插件你就可以干很多活儿了    
[参考原文地址](http://www.mobileread.com/forums/showthread.php?t=203326)
文中有两个附件，都下载完毕。
1. 将`KUAL-v2.7.zip`解包，将其中的`KUAL-KDK-2.0.azw2`放到 kindle的`documents`目录下。   
2. 将`kual-helper-0.5.N.zip`解包，将`extensions\`放到根目录下，这样越狱就算完成了。你就可以在你的书籍界面看到一个`kindle launcher`了   
3. [下载mrinstaller](http://www.mobileread.com/forums/showthread.php?t=251143)，直接解压到根目录即可`包含extensions和mrpackages`   
4. [下载kpvbooklet](https://github.com/koreader/kpvbooklet/releases)，然后将`update_kpvbooklet_x.x.x_install.bin`放到`mrpackages`目录。打开`kindle launcher -> helper -> Install MR Packages`，重启。    
5. [下载Koreader](https://github.com/koreader/koreader/releases)。解压，`koreader`文件夹放到根目录,`extensions`目录也复制到根目录   

这样，你就可以打开epub 可以进行pdf重排了
# 展示
![](/res/20161112-kindle-01.png)
![](/res/20161112-kindle-02.png)
![](/res/20161112-kindle-03.png)
