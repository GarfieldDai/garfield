---
title: Angular环境配置
date: 2017-11-24 22:00:06
categories: JavaScript
tags: Angular
thumbnail: "/images/JavaScript/angular/Angular5.png"
---
![](/images/JavaScript/angular/Angular5.png)

## 目的
如何配置Angular5环境，使用Angular CLI进行辅助开发。

<!--more-->

## 简介
Angular后期版本使用TypeScript进行开发，不同于1.x版本。

## 内容
1. 确保node 6.9.x ／ npm 3.x.x 以上版本。执行Angular CLI安装命令。
```bash
$ npm install -g @angular/cli
```

2. 创建应用。
```bash
$ ng new my-app
```

3. `ng serve`可以启动自带的服务器，方便在浏览器调试应用。
```bash
$ cd my-app
$ ng serve --open
```

4. `ng generate component component-name`自动生成组件。
`ng generate directive|pipe|service|class|guard|interface|enum|module`。

5. `ng build`构建项目，将生成的文件放置目录`dist/`，使用`-prod`构建生产线项目。

6. `ng test`使用[Karma](https://karma-runner.github.io)执行单元测试。

7. `ng e2e`使用[Protractor](http://www.protractortest.org/)执行端对端测试。

8. `ng help`查看更多帮助文档。


参考资料
[Angular Quick Start](https://angular.io/guide/quickstart)
