---
title: Python3文件读写
categories: Python
date: 2017-06-22 21:31:01
thumbnail: "/images/Python/python.png"
---
![](/images/Python/python.png)

## 目的
使用Python3进行文件读写。
<!--more-->

## 内容
```python
f = open('workfile', 'w')
```
`open(filename, mode)`使用该函数进行文件的读写操作。`filename`：该参数为文件路径。`mode`：可省略，表示读取文件的模式，有以下四种模式。文件中的换行符`\n`或者`\r\n`将统一转为`\n`。
+ `'r'`：该模式表示文件只读，如果`mode`没填写，则默认为该模式。
+ `'w'`：该模式表示文件只写，写入的内容将会覆盖原有的内容。
+ `'a'`：该模式表示文件只写，从文件原有的内容结尾写入。
+ `'r+'`：该模式表示文件可读可写，从文件原有的内容结尾写入。

```python
>>> with open('workfile') as f:
...     read_data = f.read()
>>> f.closed
True
```
推荐使用`with`关键字使用file对象，好处是完成文本读取后自动关闭文件流，即便是读取期间出现异常也会安全关闭。比起使用`try-finally`，`with`的语法更加简洁。如果不使用`with`关键字，你需要使用`f.close()`手动关闭文件流，及时的释放系统资源。如果你不主动关闭文件流，Python的垃圾回收器最终也会帮你释放资源，只不过释放的时间不能够预知。

```python
>>> f.read()
'This is the entire file.\n'
>>> f.read()
''
```
`f.read(size)`你可以设置`size`来读取一定长度的文本。如果缺省或为负数，将会返回文本的全部内容。如果已经读完文本，将会返回空字符串`''`。

```python
>>> f.readline()
'This is the first line of the file.\n'
>>> f.readline()
'Second line of the file\n'
>>> f.readline()
''
```
`f.readline()`只读取一行文本,并且以`\n`结尾。如果已经读完文本，将会返回空字符串`''`。

```python
>>> for line in f:
...     print(line, end='')
...
This is the first line of the file.
Second line of the file
```
可以使用上面这个方法进行文本读取，节约内存并且高效。你也可以使用`list(f)`或者`f.readlines()`将文本一次性放到列表里面。

```python
>>> f.write('This is a test\n')
15
```
`f.write(string)`将文本写入文件中，返回的值是写入文本的长度。


参考资料
[Reading and Writing Files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files)
