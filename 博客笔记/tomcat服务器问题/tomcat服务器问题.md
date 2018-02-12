---
date: 2017-10-14 11:05
status: public
title: tomcat启动失败的几种解决方案
---

> Server Tomcat v9.0 Server at localhost failed to start.

运行tomcat没有显示以上错误信息，然后点击detail，没有什么具体的错误信息。这个原因是因为你的某一个工程中出现了问题，导致整个tomcat启动不了。

解决办法：在server处右键点击"open",然后左下角显示两个分类overview和Modules，点击Modules，把path下面的工程包一个一个remove。这种重新部署的方式可以让你的tomcat恢复成最初的状态。