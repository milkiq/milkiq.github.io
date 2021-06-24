---
title: 前端工程化
date: 2018-05-13 21:51:07
tags: [软件工程, 学习笔记]
categories: 前端
---

## 工程化

方法论，链路规范化、系统化、流程化

**前端工具、流程等**

## 前端发展历史

1. 早期：用户需求简单，开发前后端没有明显区分，开发者只关心页面是否正常输出，开发、维护困难
2. 近现代时期：前端出现，HTML 中插入后端代码，后端为主的 MVC，意识到多人协作问题
3. 现代：用户要求内容多元、交互复杂、体验优良，加载快内容丰富、流量省、更安全。多人合作、前端亦可独立开发。

<!--more-->

**代码特点：**

- 项目变大
- 结构、逻辑、内容复杂
- 代码校验
- 页面有相似性

**以往开发流程：**

- 复杂繁琐
- 自行优化

## 前端工程化包含内容

### 规范化

变量命名， 固定的 DOM 结构

Airbnb 代码规范等

文件结构规范

代码检测：Style Lint，JSLint 等

### 模块化开发

开发阶段使用分而治之对方法封装、设计

如：CSS

代码检查   =》 预处理  =》 后处理    =》 合并         =》 压缩

CSSHint          SASS     AutoPrefixer   CSS-combo    clean-css

...                      ...           ...                        ...                      ...

POSTCSS 平台，插件集合

CSS Modules，解决变量名全局污染问题

JS

代码检查      =》   编译     =》  合并   =》    优化

JSLint                  

### 组件化开发

WEBAPP = PAGE + PAGE + ...

### 开发流程

- MOCK API：约定好接口，在平台上检验，不必等待后端
- 实时编译：nodemon，webpack - - watch，gulp watch
- 实时更新：webpack-dev-server - -hot，browser-sync
- 本地调试
- ...

### 测试

- 单元测试
- 功能测试
- UI 测试
- 自动化测试

ARMA，mocha， QUnit，PhantomCSS（与设计稿像素级对比），Puppeteer（替代 PhantomCSS）

### 部署

- 静态资源管理、及其版本管理
- 发布上线
- 覆盖式、版本记录
- 多机房部署
- 自动化部署

### 性能优化

- 资源合并
- 代码压缩、混淆
- 安全漏洞自动修复
- ...

### 监控、统计...

- 性能监控，统计分析：
  - 个性化定制统计
  - Google、百度统计，友盟cnzz
- 业务监控，及时发现问题，定位问题：FunDebug...

## 其他语言构建

- 构建指的是建设的过程
- 大多数指动手创建的过程


- makefiles
- Apache Maven
- shell

## 前端构建工具

GRUNT、Gulp、Yann npm + webpack、F.I.S（百度）、燕尾服（360）

### npm script

- package.json
- package-lock.json
- 依赖 shell
- 难以注释

### gulp

- 有很多好用的插件
- 依赖插件开发者
- 需要关注文档多
- 难以调试

### webpack

- 模块化的打包工具，一切资源皆模块，以 JS 为入口

#### 配置

```javascript
module.exports = {
    entry: './entry.js',
    output: {
        path: __dirname,
        filename: 'bundle.js'
    },
    modules: {
        rules: [
            { test: /\.vue$/, loader: 'vue-loader' },
        ]
    }
}
```

#### 特点

- 对 JS、CSS、图片等资源文件都支持打包
- 对 CommonJS、AMD、ES6 的语法做了兼容
- 串联式模块加载器以及插件机制
- 支持按需加载，降低首屏加载时间

#### 功能

- 代码压缩
- 代码合并
- 内联图片转为 base64
- 编译转换，js、react、vue...
- 按需加载
- 简单的 HTML 处理

#### 短板

- 复杂模板处理
- 安全漏洞自动修复
- 在处理资源前，先更新代码
- 上线之前测试

#### 相关

1. loader
   - eslint
   - babel
   - vue
   - image->base64


1. plugin
   - MiniCssExtractPlugin
   - HtmlWebpack
2. ...

#### 可自定义插件

e.g. qcdn-webpack-plugin（360）

- webpack插件
- 生成资源
- 替换被引用文件中资源
- 上传引用文件和静态资源、生成目标模板

## 思考

- 结合业务特点落地
- 工具不是为了使用而使用

（ 360 前端星计划 2018.05.10 ）