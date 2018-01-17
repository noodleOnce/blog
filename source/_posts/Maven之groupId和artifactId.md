---
title: Maven之groupId和artifactId
date: 2018-01-11
tags: maven
categories:
- maven
---
> 我们在利用eclipse或者idea新建一个maven项目的时候，会让你输入GroupId和ArtifactId，那这两个ID是什么东东呢？有什么用呢?

groupid和artifactId被统称为“坐标”是为了保证项目唯一性而提出的，如果你要把你项目弄到maven本地仓库去，你想要找到你的项目就必须根据这两个id去查找。groupId一般分为多个段，这里我只说两段，第一段为域，第二段为公司名称。<!--more-->域又分为org、com、cn等等许多，其中org为非营利组织，com为商业组织。举个apache公司的tomcat项目例子：这个项目的groupId是org.apache，它的域是org（因为tomcat是非营利项目），公司名称是apache，artigactId是tomcat。比如我创建一个项目，我一般会将groupId设置为cn.wonderful，cn表示域为中国，wonderful是我个人姓名缩写，artifactId设置为springDemo，表示你这个项目的名称是springDemo，依照这个设置，你的包结构最好是cn.wonderful.springDemo打头的，如果有个StudentDao，它的全路径就是cn.wonderful.springDemo.dao.StudentDao,我们依赖的第三方jar包都是遵循这个规则，如下：

``` java
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.16.14</version>
</dependency>
```


