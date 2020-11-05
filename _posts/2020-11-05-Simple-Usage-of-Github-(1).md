---
title: Simple Usage of Github (Overview&Profile)
author: Wu Han
date: 2020-11-05 22:50:00 +0800
categories: [Tutorial]
tags: [Github]
math: false
pin: false
image: /assets/img/posts/github.jpg
---

# Github 基本介绍小白向:从注册登录到完善信息
## BeforeStart
最近咕了好久才开始更，并且第一篇是Github相关的。主要是因为大二课程编排真的累，每天都有很多活和作业要写，最近这周还有比赛要打。这篇文章是在npy的再三要求之下(划掉)才开始抽空写的[^footnote1].全文小白向，不要觉得多就不读了，很多是没用的废话(x)，因为主要是让npy不问出奇奇怪怪的问题(大雾)(真实原因:特别奇技淫巧的我也不会:-)
## WhatIsGithub
>Github是什么东西呢？电脑网页相信大家都很熟悉，但是Github是什么东西呢？下面就让小编带大家一起了解吧。Github是什么东西，其实就是一个全球最大的同性交友网站，大家可能会很惊讶Github怎么会是全球最大的同性交友网站呢？但事实就是这样，小编也感到非常惊讶。这就是关于Github的事情了，大家有什么想法呢，欢迎在评论区告诉小编一起讨论哦！

好了不皮了，GitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub[^footnote2]。说人话就是Github是一个可以在上面分享并且查看保存自己或者其他人的代码的网站，开源的意思就是这些代码是开放的[^footnote3]。因为code早就刻进了coder的DNA里，所以交换代码无异于交换基因(怎么有点怪怪的[滑稽])总而言之，Github很重要，如果你想直接借鉴或者改造别人的成果，Github能很好的避免重复造轮子。那么，让我们开始吧！

## Signup&Signin
首先让我们打开[Github网站](https://github.com/),大家都是成熟的大学生了，该学会自己看英语了(划掉)。如果你没有用过这个网站的话需要先注册一个账号。在打开的主页分别填入注册用的Username(用户名),Email(邮箱),Password(密码)，点击下方signup按钮进入一个界面![注册界面](/assets/img/posts/github.jpg)，过一下验证码![验证码界面](/assets/img/posts/verify.jpg)，进入选择兴趣界面，按自己的实际情况填写即可(其实用处不大)，填完之后(想跳过可以直接)按最下方的按钮，到发验证码邮件阶段![验证码](/assets/img/posts/checkemail.jpg)，检查邮箱，点击验证链接就完成注册啦！登录的话就是回到[主页面](https://github.com/)，点击最上面signup，输入email和password就可以了.![登录界面](/assets/img/posts/login.jpg)

## Exploring
成功登录后，好好看看你的主页部分。![主页部分](/assets/img/posts/index.jpg),因为东西很多，所以我只是简略介绍功能，具体怎么玩就自己explore吧！首先看上图的红色部分，这里是你自己上传的/fork别人的代码库，具体什么意思我会在下一节详细介绍。黄色的部分是teamwork，不过我想大学里面应该用不上这个功能。这个功能是多个账号对同一个代码进行维护的时候用到的，github支持创建私密库但是只能有限的几人参与维护，加入team则无限制，相应的，这个功能并不免费。中间的蓝色部分就是动态啦，你关注的人最近star(类似于点赞)过那些库，fork(类似于转载)过哪些库，create(创建)过哪些库等等[^footnote4]。右边绿色部分是一些github的活动以及推荐的库，可以没事逛一逛，很容易逛到惊喜哟~上面粉粉的框框里首先最醒目的就是搜索框，搜索出来的结果支持按类区分，这点很赞，也可以指定搜索范围(本代码库/全体github)，后面的几个也很实用，不过和下一节要说的库有一定重复，pullrequest是你所有库里pull的总和，Issues是所有库里issue的总和(下节讲),market里面有很多有趣有用的小插件，当然国内访问github有点慢，这些插件配合fq工具使用效果更佳。explore和Twitter的结构差不多，这个就留给自己explore吧XD

接下来是右上角橙色的部分，从左到右第一个是通知信息，第二个是用来快捷建立新库或者gist[^footnote5]的，第三个是你的个人信息部分。

## HomePage
在主页点击右上角个人信息的头像下拉栏里的**your profile**，你会看到你的profile界面![profile](/assets/img/posts/profile.jpg).红色部分可以修改头像，地址，座右铭等等，橙色部分是你的库，项目和包的信息，其中项目和包基本上现在我们个人的能力涉及不到，包是封装好的项目，具体信息可以在package界面看官方文档。绿色是你这些年中哪些天活跃的可视化表示。接下来点击右上角下拉栏
**Settings**进行更多设置![Settings](/assets/img/posts/Settings.jpg)橙红色的区域是不同设置，绿色部分是对应的详细设置，这要是展开讲讲我人没了..说几个经常用到的吧

>profile
>>Name:昵称可改，账号名不可改<br>
Public email:公开的可被他人看到的email地址，在设置git时也有用。<br>

>Account
>>Change username:改昵称<br>
Export account data:导出profile和所有库，七天有效<br>
Successor settings:继承代码(离谱)<br>
Delete account:销号

>Account security
>>Change password:改密码<br>
Two-factor authentication:密码锁<br>

>Emails
>>Add email address:添加新的emailaddress(有的可以用来验证身份，有的不行，有的是公开的，有的是私密的)<br>

>Notifications
>>Email notification preferences:在什么情况下发邮件

>SSH and GPG keys
>>SSH keys:SSH连接的密钥，需要申请，申请之后可用于远程连接

>Developer settings
>>OAuth Apps:注册新的应用凭证(其实就是把Github的验证搬到你想要用的地方)

## AdvanceNotice
下一节要讲最重要的github的灵魂————托管库及操作，记得搬好小板凳来看喔，欢迎带点吃的投喂QAQ(不咕不咕)


## FootNote
[^footnote1]:之前其实录了一个特别完备的视频，结果估计有1G吧，发过去之后我就嫌太占地方删了，然后她没看就重装了QQ**超小声**
[^footnote2]:摘自百度百科
[^footnote3]:很多人认为开源就是随便用，其实是不对的，要看它遵循了什么协议，这里有一张图供参考。[阮一峰的网络日志](https://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html)
[^footnote4]:翔哥的github我就不打码了XD
[^footnote5]:gist是Github的一个宝藏功能，可惜知道的人不是很多，具体用法可见[What You Can Do With Gists on Github?](https://www.labnol.org/internet/github-gist-tutorial/28499/)
