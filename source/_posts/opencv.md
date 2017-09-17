---
title: OpenCV macOS 环境配置
date: 2017-09-13 20:26:57
categories: Computer Vision
tags: OpenCV
thumbnail: "/images/ComputerVision/opencv.jpg"
---
![](/images/ComputerVision/opencv.jpg)

## 目的
如何在macOS环境下进行OpenCV的配置，使用Python进行计算机视觉(Computer Vision)开发。

<!--more-->

## 简介
OpenCV是开源的计算机视觉类库，支持C，C++，Java，Python编程语言，可以进行跨平台开发，该类库集成了图像和视频的输入输出，图像处理，物体识别，机器学习和深度神经网络等实用工具类。

## 内容
本博文基于Python3.6和OpenCV3进行讲解，当前系统版本为macOS 10.12+，在macOS系统上面安装OpenCV是一件非常操蛋的事情。

1. 安装Xcode，如果是第一次安装使用，需要获得苹果开发者授权，安装完后，执行命令，按照提示输入`accept`。
```bash
$ sudo xcodebuild -license
```

2. 安装苹果命令行工具，该工具包含了make，GCC，clang。该步骤是必须要执行的。
```bash
$ sudo xcode-select --install
```

3. 安装苹果系统包管理器`Homebrew`，类似Debian系统系列的`apt-get`。
```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

4. macOS系统虽然自带了Python，但是为了避免与系统冲突，我们自己安装专门进行开发的Python。
```bash
$ brew install python3
```

5. 检查Python版本是否正确安装配置环境变量。
```
$ which python3
/usr/local/bin/python3
```
  如果Python没有配置好环境变量，需要手动更新环境变量`~/.bash_profile`。
  ```
  # Python3
  export PATH=/usr/local/bin/python3:$PATH
  ```
  更新环境变量配置。
  ```bash
  $ source ~/.bash_profile
  ```

6. 安装Python虚拟环境`virtualenv`和`virtualenvwrapper`。
```bash
$ pip install virtualenv virtualenvwrapper
```
  如果出现`OSError: [Errno 1] Operation not permitted by six`，可使用下面命令行解决问题。
  ```bash
  $ sudo pip install virtualenvwrapper --ignore-installed six
  ```

7. 配置环境变量`~/.bash_profile`。
```
# Virtualenv/VirtualenvWrapper
source /usr/local/bin/virtualenvwrapper.sh
```
  更新环境变量。
  ```bash
  $ source ~/.bash_profile
  ```

8. 创建Python3虚拟环境，使用`mkvirtualenv`。使用该命令创建名为`cv`的虚拟环境，该环境独立于系统其他环境，有自己独立的包目录，避免包冲突。
```bash
$ mkvirtualenv cv -p python3
```
  进入创建好的`cv`环境。
  ```bash
  $ workon cv
  ```

9. 安装`Numpy`。
```bash
$ pip install numpy
```

10. 正式编译之前，需要安装编译，图像I/O和优化相关的工具包的。
```bash
$ brew install cmake pkg-config
$ brew install jpeg libpng libtiff openexr
$ brew install eigen tbb
```

11. 从Gitub下载OpenCV源代码。
```bash
$ cd ~
$ git clone https://github.com/opencv/opencv
$ git clone https://github.com/opencv/opencv_contrib
```

12. 接下来正式开始编译配置，首先创建并进入编译目录。
```bash
$ cd ~/opencv
$ mkdir build
$ cd build
```

13. 构建自己环境的CMake命令，这里给出的是该命令的模版。
```bash
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D PYTHON3_LIBRARY=YYY \
    -D PYTHON3_INCLUDE_DIR=ZZZ \
    -D PYTHON3_EXECUTABLE=$VIRTUAL_ENV/bin/python \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=ON ..
```

14. 替换上面命令的`YYY`和`ZZZ`，可参考我本地的配置，不要复制粘贴，每个人的机器配置会有不同。
`PYTHON3_LIBRARY=YYY`：libpython3.6.dylib的路径。
`PYTHON3_INCLUDE_DIR=ZZZ`：python3.6m的路径。
```bash
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D PYTHON3_LIBRARY=/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/lib/python3.6/config-3.6m-darwin/libpython3.6.dylib \
    -D PYTHON3_INCLUDE_DIR=/usr/local/Cellar/python3/3.6.2/Frameworks/Python.framework/Versions/3.6/include/python3.6m \
    -D PYTHON3_EXECUTABLE=$VIRTUAL_ENV/bin/python \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=ON ..
```
  配置好后，执行该命令。

15. 开始编译，编译时间在30-90分钟左右，取决于你的机器配置。
```bash
$ make -j4
```

16. 编译完后，如果没有出现错误，执行安装命令。
```bash
$ sudo make install
```

17. 安装成功后，检查python包安装目录是否有类似`cv2.cpython-35m-darwin.so`的文件。
```bash
$ cd /usr/local/lib/python3.6/site-packages/
$ ls -l *.so
-rwxr-xr-x  1 root  admin  3694564 Nov 15 11:28 cv2.cpython-35m-darwin.so
```
18. 将`cv2.cpython-35m-darwin.so`重新命名为`cv2.so`。
```bash
$ cd /usr/local/lib/python3.6/site-packages/
$ mv cv2.cpython-35m-darwin.so cv2.so
$ cd ~

$ cd ~/.virtualenvs/cv/lib/python3.6/site-packages/
$ ln -s /usr/local/lib/python3.6/site-packages/cv2.so cv2.so
$ cd ~
```

19. 校验OpenCV是否已经正确安装并引入。
```bash
$ workon cv
$ python
Python 3.6.2 (default, Jul 17 2017, 16:44:45)
[GCC 4.2.1 Compatible Apple LLVM 8.1.0 (clang-802.0.42)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2
>>> cv2.__version__
'3.3.0-dev'
>>>
```

参考资料
[OpenCV Documentation](http://docs.opencv.org/master/d9/df8/tutorial_root.html)
[OpenCV Tutorials](http://www.pyimagesearch.com/2016/12/05/macos-install-opencv-3-and-python-3-5/)
[Homebrew](https://brew.sh)
