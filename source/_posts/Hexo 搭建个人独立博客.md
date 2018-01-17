---
title: Hexo 搭建个人独立博客
tags: 随笔
categories:
- 随笔
---
以前经常在[简书](https://www.jianshu.com/)，[CSDN](https://www.csdn.net/)等博客平台闯荡，但感觉太零散了，所以一直想有个专属于自己的博客来写日志。刚好最近任务不是很重，利用工作之闲搭建了一个个人独立博客，下面介绍下搭建过程，有DIY情结的可以参考下。
#### 搭建步骤:
1. 安装hexo,初始化blog
2. 部署
3. 更换主题(可选)
4. 添加第三方插件(可选)
  <!-- more -->
***
#### 第一步:安装hexo
* 环境要求：ndoe,git 
* 参考地址:[安装nodejs](http://www.runoob.com/nodejs/nodejs-install-setup.html)  [安装GIT](https://git-scm.com/download/) 
* 注:以下说的站点配置指的是blog根目录下的_config.yml,主题配置指的是blog\themes目录下的_config.yml

环境准备好了，开工:
随便找个目录右键打开gitbash,一步步的输入如下命令:
```
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ hexo server 
```
ok,打开浏览器输入http://localhost:4000/
![效果](https://wx1.sinaimg.cn/mw1024/93e5a6afgy1fnhgnk76jtj215d0mojsn.jpg)
这是hexo的默认皮肤，默认有一篇日志(heloWorld.md)存放在source/_posts目录下，以后撰写的日志都存放于此
* 注:.md是markdown文件格式，利用mrakdown标记语言来写日志简直爽到爆，学习成本不高，掌握几个常用的就足够了。markdown编辑器推荐[Typora](https://www.typora.io/)

#### 第二步:部署blog
* 第一步只是在本机环境部署，要想他人也能访问你的blog，必须部署到公网上，正常流程是购买域名-购买云服务器-部署项目，但是考虑到这只是个静态博客，花钱就没必要了，所以推荐GitHub提供的静态个人主页。

1.登录github，新建repository，注意repository name必须yourgithubname.github.io，如：wonderful5.github.io，因为该路径就是你github的个人主页，每个账户只有一个。完了在你的reposities里就会多一个xxx.github.io项目，该项目就是你的主页源码了。
![github.io](https://wx1.sinaimg.cn/mw1024/93e5a6afgy1fnijoic95aj20s20jn0tu.jpg)
浏览器输入htts://xxx.hithub.io就可以看到你的github个人主页，空白，因为你还没有将blog源码推送到该资源库，继续往下。
2.打开站点配置文件，找到deploy节点，更改如下：
```
deploy:
  type: git
  repo: git@github.com:wonderful5/wonderful5.github.io.git
  branch: master
```
接下来就要开始推送代码部署项目了，回到你的blog根目录，右键打开gitbash，敲命令:
```
$ hexo clean
$ hexo generate
$ hexo deploy
```
大功告成，浏览器输入htts://yourgithubname.hithub.io访问看看效果吧，是不是跟你本机浏览的一样了。

#### 第三步:更换主题(可选)
* 至此，你的blog就面向大众了，是不是来个个性点的主题呢，hexo主题很多，这里我推荐next，后面的讲解也是针对next主题

在blog根目录下右键打开gitbash，下载next主题:
```
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
你会在themes目录下看到一个next目录，这就是next主题源码了，修改站点配置文件的theme节点,默认值:landscape
```
theme:next
```
按上面的部署命令重新发布一下，浏览器输入htts://yourgithubname.hithub.io看看效果吧,
![效果](https://wx3.sinaimg.cn/mw1024/93e5a6afgy1fnhhn7dug2j218g0jz76b.jpg)
* 说明:个性的配置都藏于站点配置文件和主题配置文件下，且都有注释

#### 第四步：添加第三方插件(可选)
* 想要知道你的日志有多少人访问怎么办？那就给日志来个阅读次数吧
* 访客想要跟博主互动怎么办？那就来个评论功能吧

###### 添加阅读次数
1.打开LeanCloud官网，进入[注册页面](http://www.jeyzhang.com/hexo-next-add-post-views.html)注册。完成邮箱激活后，点击头像，进入控制台页面，如下：
![lendCloud注册](https://wx2.sinaimg.cn/mw1024/93e5a6afgy1fniajhvw2fj218g0jzwf4.jpg)
2.创建新应用，应用名随意，blog.me就是我创建的新应用，如下:
![lendCloud注册](https://wx2.sinaimg.cn/mw1024/93e5a6afgy1fniajhvw2fj218g0jzwf4.jpg)
3.创建Class,命名为Counter,如下：
![创建Class](https://wx4.sinaimg.cn/mw1024/93e5a6afgy1fniav1gj4fj218g0jzwfp.jpg)
4.绑定blog域名，如下
![绑定域名](https://wxt.sinaimg.cn/mw1024/93e5a6afgy1fniaxyhrlvj218g0jzmyx.jpg?tags=%5B%5D)
5.配置leanCloud，打开next主题配置，找到leancloud_visitors节点，修改如下，其中app_id和app_key在你lennCloud所创建的应用的设置->应用Key中。
```
leancloud_visitors:
  enable: true
  app_id: GulnQhVRPj7fGO8jejvfvJcD-gzGzoHsz
  app_key: YyNk6gHXUVLBH6tuMac7u274
```

###### 添加评论
1.[注册](https://github.com/settings/applications/new) OAuth Application,其他内容可以随意填写，但要确保填入正确的 callback URL（一般是评论页面对应的域名，如https://wonderful5.github.io/）。
你会得到一个 client ID 和一个 client secret，这个将被用于之后的用户登录。
2.打开next主题配置，找到gitment节点，修改如下，其中github_user和github_repo分别是你的GitHub账号和blog仓库的repo名称
```
gitment:
  enable: true
  mint: true # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true # Show comments count in post meta area
  lazy: false # Comments lazy loading with a button
  cleanly: false # Hide 'Powered by ...' on footer, and more
  language: # Force language, or auto switch by theme
  github_user: wonderful5 # MUST HAVE, Your Github ID
  github_repo: wonderful5.github.io # MUST HAVE, The repo you use to store Gitment comments
  client_id: bc397d84441834a5cbef # MUST HAVE, Github client id for the Gitment
  client_secret: c5268ce514ba62ce1ec33c90c9f4c043c7ccd2df # EITHER this or proxy_gateway, Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```
重新部署看看效果吧







