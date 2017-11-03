---
title: TypeScript 系列教程三
date: 2017-05-23 21:28:50
categories: JavaScript
tags: TypeScript
thumbnail: "/images/JavaScript/typescript/typescript.png"
---
![](/images/JavaScript/typescript/typescript.png)

## 目的
学习TypeScript的基础数据类型（Basic Types）。

<!--more-->

## 简介
本章节主要学习TypeScript的基础数据类型。

## 内容
### Boolean 布尔类型
```
let isDone: boolean = false;
```
### Number 数值
```
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```
### String 字符串
TypeScript可以使用双引号`"`或者单引号`'`表示字符串。
```
let color: string = "blue";
color = 'red';
```
你也可以使用字符串模板（template strings），可以在字符串里面嵌套表达式`${ expr }`，字符串模板需要用单引号`'`来表示。
```
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${ fullName }.

I'll be ${ age + 1 } years old next month.`;
```
上面的表达式就跟下面的一样。
```
let sentence: string = "Hello, my name is " + fullName + ".\n\n" +
    "I'll be " + (age + 1) + " years old next month.";
```
### Array 数组
```
let list: number[] = [1, 2, 3];
```
你也可以使用`Array<elementType>`来声明数组。
```
let list: Array<number> = [1, 2, 3];
```
### Tuple 元组
```
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```

```
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```

```
x[3] = "world"; // OK, 'string' can be assigned to 'string | number'
console.log(x[5].toString()); // OK, 'string' and 'number' both have 'toString'
x[6] = true; // Error, 'boolean' isn't 'string | number'
```

### Enum 枚举
```
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```
枚举类型默认从0开始，你也可以手动修改初始值。
```
// 修改初始值为1
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
```
你也可以手动设置所有的初始值
```
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```

参考资料

[TypeScript-basic-types](http://www.typescriptlang.org/docs/handbook/basic-types.html)
