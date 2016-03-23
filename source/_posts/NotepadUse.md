---
title: Notepad++启动时提示load langs xml failed错误解决
tags: tech
categories: tech
notshow: true
date: 2016-03-16 15:53:48
---
问题描述：

我的Notepad++在一次崩溃后每一次启动的时候就提示load langs xml failed，然后不能自动加载语法高亮文件。
到Notepad++的安装目录查看langs.xml文件，发现该文件是空的(0kb)/或者文件内容相对langs.model.xml文件较少

解决方案：
<!-- more -->

很简单，就是将同目录下的langs.model.xml复制一份后放到langs.xml文件里面即可.再启动Notepad++.
希望这个方案对其他也碰到这个问题的人能有帮助
