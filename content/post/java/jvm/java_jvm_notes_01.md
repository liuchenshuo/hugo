+++
banner = ""
categories = ["java-jvm"]
date = "2021-05-05T09:03:51+02:00"
description = ""
images = []
tags = ["深入理解JVM"]
title = "深入理解Java虚拟机--第一章 走进java"

+++
# 深入理解Java虚拟机--第一章 走进java

1. 世界上没有完美的程序，但是我们并不因此而沮丧，因为写程序本来就是一个不断追求完美的过程。
2. JDK: Java Development Kit. 开发库
3. JRE: Java Runtime Environment. 运行库

4. JAVA当前版本维护：

   *每六个JDK大版本中才会被划出一个长期支持（Long Term Support，LTS）版，只有LTS版的JDK能够获得为期三年的支持和更新，普通版的JDK就只有短短六个月的生命周期。JDK 8和JDK 11会是LTS版，再下一个就到2021年发布的JDK 17了。*

### 虚拟机 HotSpot VM

* Classic VM 第一个JVM 一直到 JDK1.4
* Exact VM 没能够商用
* HostSpot VM 从JDK1.2开始使用 当前使用范围最广的虚拟机
* Mobile/Embedded VM 手机端使用
* BEA JRockit/IBM J9 VM 其他公司虚拟机
* ......

### 无语言倾向发展

2018年4月，Oracle Labs新公开了一项黑科技：Graal VM，它的口号“Run Programs Faster Anywhere” 不仅仅支持java还支持其他多种语言。

经过一系列的重构与开放，HotSpot虚拟机逐渐从时间的侵蚀中挣脱出来，虽然代码复杂度还在增长，体积仍在变大，但其架构并未老朽，而是拥有了越来越多的开放性和扩展性，使得HotSpot成为一个能够联动外部功能，能够应对各种场景，能够学会十八般武艺的身手灵活敏捷的“胖子”。

Page 51