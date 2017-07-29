---
title: Sass架构设计以及基于Gulp实现自动化构建
date: 2017-07-29 09:42:39
categories: CSS
tags: SASS
thumbnail: "/images/CSS/SASS/sass-gulp.jpg"
---
![](/images/CSS/SASS/sass-gulp.jpg)

## 目的
如何使用Sass进行前端样式架构设计，并且使用Gulp进行自动化构建项目。

<!--more-->

## 简介
+ 在阅读Bootstrap的基于Sass的源代码后，吸收了Bootstrap架构设计的经验，来谈谈如何在实际的项目开发中搭建Sass架构。
+ 在进行前端开发过程中，虽然可以使用Sass自带的编译命令类似`sass --watch style.scss:style.css --style compact`进行CSS的编译，但是自带的命令功能有限。结合Gulp的使用，可以让项目自动化构建变得更加的灵活，而并不局限于编译CSS。

## 内容
#### Preparation
+ Nodejs
+ Sass
+ Gulp

#### Sass Architecture
我们可以这样建立项目结构。
```
--project/
  --css/    
    --mySass/      
      --_dialog.scss
      --_home.scss
      --_mixins.scss
      --_variables.scss
    --mySass.scss
```

1. 在文件夹`mySass`里面，放置项目的Sass文件，所有的文件被引用到`mySass.scss`，然后使用`mySass.scss`进行CSS编译。
```css
/* mySass.scss */
/* Core variables and mixins */
@import "mySass/variables";
@import "mySass/mixins";

/* Module or others */
@import "mySass/home";
@import "mySass/dialog";
```

2. `_variables.scss`该文件放置项目的全局变量，`_mixins.scss`该文件放置项目可复用的代码块，这两个文件需要放置在最前面，因为Sass在引入文件的时候是有顺序的要求。

3. `_dialog.scss`和`_home.scss`这里只是样例，可以根据具体的项目进行设计，可以按照控件进行归类，也可以按照某个页面进行归类等等。

4. 最后使用下面命令检验项目是否配置成功。
```
$ sass --watch mySass.scss:mySass.min.css --style compressed
```

#### Gulp
Gulp是基于流的自动化构建工具，类似的工具有Grunt和webpack。

1. 安装Gulp。
```bash
$ sudo npm install --global gulp-cli
$ gulp --help
```

2. 初始化为node项目。
```bash
$ npm init
```

3. 将Gulp加入项目。
```bash
$ sudo npm install --save-dev gulp
```

4. 安装Sass编译插件。
```bash
$ sudo npm install --save-dev gulp-sass
```

5. 在根目录创建`gulpfile.js`。

6. 当前项目结构。
```
--project/
  --css/    
    --mySass/      
      --_dialog.scss
      --_home.scss
      --_mixins.scss
      --_variables.scss
    --mySass.scss
  --node_modules/
  --gulpfile.js
  --package.json
```

7. `package.json`内容。
```json
{
  "name": "project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://xxx.xxx.xxx.git"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "gulp": "^3.9.1",
    "gulp-sass": "^3.1.0"
  }
}
```

8. `gulpfile.js`内容。
```javascript
'use strict';

var gulp = require('gulp');
var sass = require('gulp-sass');

gulp.task('sass', function () {
  return gulp.src('./css/mySass.scss')
    .pipe(sass({outputStyle: 'compressed'}).on('error', sass.logError))
    .pipe(gulp.dest('./css/'));
});

gulp.task('run', ['sass']);

gulp.task('watch', function () {
  gulp.watch('./css/**/*.scss', ['sass']);
});

gulp.task('default', ['run','watch']);

```

9. 在根目录运行命令，gulp就会自动执行任务。
```bash
$ gulp
```
至此，所有的配置完成。

参考资料
[Bootstrap](http://getbootstrap.com/getting-started/#download)
[Gulp Document](https://github.com/gulpjs/gulp/blob/master/docs/API.md)
[Gulp Sass](https://www.npmjs.com/package/gulp-sass)
