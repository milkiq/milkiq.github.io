---
title: SpringMVC的简单例子
date: 2018-03-28 10:18:45
tags: [Java, SpringMVC]
categories: 后端

---

《软件架构与设计模式》课程的老师在讲解 MVC 时留下作业，要求用 SpringMVC 实现一个简单的系统，只有登录注册就可以。

Java Web 项目我曾经做过一点，但是还没接触过使用比较专业的框架的开发的程序。所以在这次尝试的时候踩到了一些坑，包括 maven 的使用以及常见的目录结构。

<!-- more -->

话不多说，上效果图吧（成品及其简陋...）

{% asset_img main.jpg home %}

{% asset_img login.jpg login %}

{% asset_img success.jpg success %}

{% asset_img user.jpg username-wrong %}

{% asset_img password.jpg password-wrong %}

{% asset_img signup.jpg signup %}

是很丑啦...我是假的前端...不过简单例子嘛，撒撒水啦~

整个 demo 的目录结构是这样的：

{% asset_img filetree.jpg  directory-structure %}

开发环境为 JDK1.8 + Maven3.0.5 + IDEA 。

关于使用 Maven ，有一个很好的免费视频教程：[孔浩的 Maven 视频教程](http://www.icoolxue.com/album/show/45)，看一看概述就能很快的理解 Maven 的用途和便利。当然，不使用 Maven 也能开发 SpringMVC ，手动导入依赖的包就可以了。不过我不怎么推荐这种方式，因为经过我上手的配置了一下后发现，手动导入包后还需要自行创建相关结构。对于初学者来说，从网上千奇百怪的目录结构示例中挑选到一个合适的简单的例子进行模仿是并不容易的，而能自行创建项目结构的 Maven 就显得格外重要了。

Maven 配置好后，打开IDEA（如果你也是使用IDEA的话），选择创建 Maven 项目：

{% asset_img MavenProject.jpg Maven-project %}

创建好了之后，稍稍等待，Maven 就会把目录建立好，这个时候就可以编辑和添加自己的配置文件了。

我在项目中使用的配置文件有：

1. pom.xml
2. web.xml
3. spring-content.xml

pom.xml 中是用 Maven 配置项目的“设置”文件，为了使用 SpringMVC 一定要在这个文件中的 `<dependencies>` 标签中写明所有需要的包。Maven 的另一个好处也将显示出来，比如项目中我要使用 MySQL 数据库，原本必须下载JDBC驱动并导入，现在只需要在 pom.xml 中添加：

```xml
<dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.34</version>
        </dependency>
```

就可以通过 Maven 自动导入数据库连接所需要的包了，并且在随后的编写代码中并不需要 import 导入相关的包，是不是很省心~

web.xml 是SpringMVC中非常重要的配置，所有使用SpringMVC框架开发文件都必须使用它来说明对应用的设置，比如配置 SpringMVC 的配置文件的位置。如果这个文件编写的有错误，应用是不可能正常运转的。

spring-content.xml 就是 SpringMVC 的配置文件。在这里要写明对项目中类的扫描，以及配置视图解析器。可能听起来很术语，不好理解，那么我们就索性顺带着说一下SpringMVC的架构，以更好的理解SpringMVC。

{% asset_img SpringMVC.jpg SpringMVC %}

SpringMVC 和最基础的MVC架构略有不同，SpringMVC使用 Dispatcher Servlet 这个控制器来和用户进行交互，而不是一般 MVC 视图中那样用户直接和视图进行接触。

{% asset_img MVC.jpg MVC %}

# 架构流程

1. 用户发送请求至前端控制器 Dispatcher Servlet。
2. Dispatcher Servlet 收到请求调用 Handler Mapping 处理器映射器。
3. 处理器映射器根据请求 URL 找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给 Dispatcher Servlet 。
4. Dispatcher Servlet 通过 Handler Adapter 处理器适配器调用处理器。
5. 执行处理器( Controller，也叫后端控制器)。
6. Controller 执行完成返回 Model And View（图省事之后写成M&V）。
7. Handler Adapter 将 controller 执行结果 M&V 返回给 Dispatcher Servlet 。
8. Dispatcher Servlet 将 M&V 传给 View Reslover 视图解析器。
9.  View Reslover 解析后返回具体 View 。
10. Dispatcher Servlet 对 View 进行渲染视图（即将模型数据填充至视图中）。
11. Dispatcher Servlet 响应用户。

具体的 SpringMVC 流程我说不太全，而且我研究的也不是很深入，详细的内容我找到了一篇非常棒的博客：[SpringMVC学习(二)——SpringMVC架构及组件（及其运行原理）](http://www.cnblogs.com/leiqiannian/p/7807579.html) 作者讲的非常详细也非常棒。不过还要回答一个我觉得像我一样的小白可能想问的问题：以上流程的代码都要自己写么？写在哪里？

其实上面的大部分流程都是不可见的，各层级的调用也不用自己写函数调用，以我自己项目中的处理器为例：

```java
    @RequestMapping(value = "/signup", method = RequestMethod.GET)
    public String signup(Model model) {
        return "sign";
    }
```



Request Mapping 设置了响应的 URL 和响应方法，这一句简单的标注就设置完成了上述流程中的处理映射器（ Handler Mapping ），而下面的 hello 函数自然就是处理器啦，处理器函数最后 return 的值就是返回的 View，函数的参数 model 就是 Model，合并起来就是 M&V 。而后象征着 M&V 的字串返回给 Dispatcher Servlet ，再传给被 spring-content.xml 配置好的视图解析器解析，找到 JSP ——这个真正的视图，并回传给 Dispatcher Servlet ，把 Model 里的数据填充到 View 中，最后完美的响应给用户的浏览器~

这些流程中的处理映射器、Model 、前端控制器、视图解析器都是通过配置文件配置好的，不用开发者详细编写代码，也看不到调用流程，开发者只需要编写处理器（后端控制器 controller ）怎么处理用户发来的数据，Model里面应该填写哪些数据，显示给用户的页面应该是怎样的就够了。

罗里吧嗦的说了这么多概念性的东西可能也有点抽象，那就把我项目的源码地址贴上来吧：https://github.com/LittleIQ/Small-Example/tree/master/JAVA/mvcdemo

我的目录代码结构参考了[ dayu-teacher 的空白项目示例](https://github.com/dayu-teacher/dayu-java-ssm/tree/master/lesson1ssm) ，大家有兴趣也可以去看一看最最简单、比我的还简单的目录结构是什么样的。