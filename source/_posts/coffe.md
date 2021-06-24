---
title: '老哥, 请我喝杯咖啡吧~'
date: 2018-01-24 21:58:42
tags: [转载, 表单]
categories: 前端
---

纯属财迷的我搭了这个博客之后就想在网站中添加个_请我喝茶_的按钮，点击之后就能跳转页面给我的支付宝账号转点money.
用支付宝的api来实现八百年都不一定有人用的这个功能实在太麻烦了，只要能简单跳转转给我就行，搞那个真没必要.

<!--more-->

于是我就找到了一个简单的办法，使用**隐藏表单**：

代码出处：[网站中添加请我喝杯茶，点击后跳转到支付宝转账界面](http://www.thinkphp.cn/code/1353.html)

首先在网页中构建一个隐藏form 

```html
<form name="alipay_form" style="padding-bottom: 0;border:none;" method="post" action="https://shenghuo.alipay.com/send/payment/fill.htm" target="_blank" accept-charset="GBK" onsubmit="document.charset='gbk';">
    <input type="hidden" value="你的高逼格支付宝账号" name="optEmail" />
    <input type="hidden" value="10" name="payAmount" /> //value值为数字，你想客户默认打赏你的钱
    <input type="hidden" name="title" placeholder="付款说明" value="打赏你的" />
    <input type="hidden" name="memo" placeholder="付款说明" value="老夫打赏你杯咖啡钱,拿去不谢！" />
</form>
```
然后添加个按钮用来提交这个表单：
```html
<button href="javascript:;" class="btn btn-default btn-sm" onclick="javascript:document.alipay_form.submit();">赞助杯咖啡，好好努力哈</button>
```

嘿嘿，贼吉儿简单吧，码一下吧，万一以后用得到呢~
