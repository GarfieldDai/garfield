---
title: TypeScript 系列教程一
date: 2017-05-20 21:28:50
categories: JavaScript
tags: TypeScript
thumbnail: "/images/JavaScript/typescript/typescript.png"
---
![](/images/JavaScript/typescript/typescript.png)

## 目的
如何配置TypeScript环境，以及在Ubuntu系统下配置Atom编辑器。

<!--more-->

## 简介
TypeScript是由Microsoft开发维护的一门免费的开源语言。该语言是JavaScript的超集，有着严格的语法格式，同时也是一门基于类的面向对象的语言。TypeScript可以被编译为JavaScript，任何存在的JavaScript程序都是合法有效的TypeScript程序。目前很多流行的库都基于该语言开发，如AngularJS, Ionic, jQuery, MongoDB和D3.js。

## 内容
### 环境配置
TypeScript 可以通过Node.js进行安装。
```
$ sudo npm install -g typescript
```
将TypeScript编译为JavaScript。
```
tsc helloworld.ts
```
### 编辑器
+ [Visual Studio 2017](https://blogs.msdn.microsoft.com/typescript/2017/03/27/typescripts-new-release-cadence/)
+ [Visual Studio 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48593)
+ [Visual Studio Code](https://code.visualstudio.com/)
+ [Sublime Text](https://github.com/Microsoft/TypeScript-Sublime-Plugin)
+ [Atom](https://atom.io/packages/atom-typescript)
+ [Eclipse](https://github.com/palantir/eclipse-typescript)
+ [Emacs](https://github.com/ananthakumaran/tide)
+ [WebStorm](https://www.jetbrains.com/webstorm/)
+ [Vim](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Editor-Support#vim)

### Atom
1. 下载Atom,并用命令行进行安装,Debian Linux (Ubuntu) 仅支持64位操作系统。
```
$ sudo dpkg --install atom-amd64.deb
```
2. 安装 [Script](https://atom.io/packages/script)插件，可以在Atom编辑器通过快捷键`shift-ctrl-b`执行js代码。
```
$ sudo apm install script
```
3. 安装Atom TypeScript插件，前提是已经安装了Git。你也可以不安装，直接编辑`.ts`文件进行开发。
```
$ sudo apm install atom-typescript
```
4. 重新启动Atom,然后会提示你安装相应的依赖包，选择安装。如果没有提示，可以手动进行安装执行下面的命令。
```
$ sudo apm install linter
```
该插件提供了以下的功能。
+ 自动补全（Autocomplete）: `ctrl+space`，使用`tab`进行选择。
+ 语法校验（Live error analysis）
+ 信息提示（Type information on hover）
+ 定位声明位置（Goto Declaration）`F12`。
+ 查询引用（Find References）: `shift+F12`。
+ 代码格式化（Format Code）: `ctrl+alt+l`。
+ 重命名（Rename refactoring）
+ 保存后编译（Compile on save）: 能够帮助你保存TypeScript后，自动编译为js代码，需要在`tsconfig.json`配置`"compileOnSave": true`。你可以在项目根目录创建`tsconfig.json`,复制下面的代码。
```
{
   "compileOnSave": true,
   "compilerOptions": {
       "noImplicitAny" : true
   }
}
```

参考资料
[TypeScript official site](http://www.typescriptlang.org/)
[TypeScript wikipedia](https://en.wikipedia.org/wiki/TypeScript)
[atom-typescript](https://atom.io/packages/atom-typescript)
[tsconfig.json](http://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
[script](https://atom.io/packages/script)
