# PyCharm 的初始设置（知道）

## 目标

* 恢复 PyCharm 的初始设置
* 第一次启动 PyCharm
* 新建一个 Python 项目
* 设置 PyCharm 的字体显示
* PyCharm 的升级以及其他

PyCharm 的官方网站地址是：https://www.jetbrains.com/pycharm/

## 01. 恢复 PyCharm 的初始设置

`PyCharm` 的 **配置信息** 是保存在 **用户家目录下** 的 `.PyCharmxxxx.x` 目录下的，`xxxx.x` 表示当前使用的 `PyCharm` 的版本号

如果要恢复 `PyCharm` 的初始设置，可以按照以下步骤进行：

* 1. 关闭正在运行的 `PyCharm`
* 2. 在终端中执行以下终端命令，删除 `PyCharm` 的配置信息目录：

```bash
$ rm -r ~/.PyCharm2016.3
```

* 3. 重新启动 `PyCharm`

## 02. 第一次启动 PyCharm

1. 导入配置信息
2. 选择许可协议
3. 配置初始界面

### 2.1 导入配置信息

* 在第一次启动 `PyCharm` 时，会首先提示用户是否导入 **之前的配置信息**
* 如果是第一次使用，直接点击 **OK** 按钮

<img src="day01.assets/001_PyCharm%E5%AF%BC%E5%85%A5%E9%85%8D%E7%BD%AE%E4%BF%A1%E6%81%AF.png" alt="001_PyCharm导入配置信息-w603" style="zoom:50%;" />

### 2.2 选择许可协议

* PyCharm 是一个付费软件，购买费用为 **199$ / 年** 或者 **19.90$ ／ 月**
* 不过 PyCharm 提供了对 **学生和教师免费使用的版本**
    * 下载地址是：https://www.jetbrains.com/pycharm-edu/download/#section=linux
* 商业版本会提示输入注册信息，或者选择免费评估

<img src="day01.assets/002_%E6%BF%80%E6%B4%BB%E8%AE%B8%E5%8F%AF%E8%AF%81.png" alt="002_激活许可证-w495" style="zoom:50%;" />

### 2.3 PyCharm 的配置初始界面

* 在初始配置界面，可以通过 `Editor colors and fonts` 选择 **编辑器的配色方案**

<img src="day01.assets/003_PyCharm%E5%88%9D%E5%A7%8B%E9%85%8D%E7%BD%AE%E7%95%8C%E9%9D%A2.png" alt="003_PyCharm初始配置界面-w491" style="zoom:50%;" />

### 2.4 欢迎界面

* 所有基础配置工作结束之后，就可以看到 `PyCharm` 的 **欢迎界面**了，通过 **欢迎界面** 就可以开始开发 Python 项目了

<img src="day01.assets/004_PyCharm%E6%AC%A2%E8%BF%8E%E9%A1%B5%E9%9D%A2.png" alt="004_PyCharm欢迎页面-w664" style="zoom:50%;" />

## 03. 新建/打开一个 Python 项目

### 3.1 项目简介

* 开发 **项目** 就是开发一个 **专门解决一个复杂业务功能的软件**
* 通常每 **一个项目** 就具有一个 **独立专属的目录**，用于保存 **所有和项目相关的文件**
    * 一个项目通常会包含 **很多源文件**

### 3.2 打开 Python 项目

* 直接点击 **Open** 按钮，然后浏览到之前保存 **Python 文件的目录**，既可以打开项目
* 打开之后，会在目录下新建一个 `.idea` 的目录，用于保存 **项目相关的信息**，例如：**解释器版本**、**项目包含的文件**等等
* 第一次打开项目，需要耐心等待 `PyCharm` 对项目**进行初始设置**

<img src="day01.assets/005_%E6%89%93%E5%BC%80%E5%B7%B2%E6%9C%89Python%E9%A1%B9%E7%9B%AE.png" alt="005_打开已有Python项目-w423" style="zoom:50%;" />

#### 设置项目使用的解释器版本

* 打开的目录如果不是由 `PyCharm` 建立的项目目录，**有的时候** 使用的解释器版本是 `Python 2.x` 的，需要**单独设置解释器的版本**
* 通过 **File** / **Settings...** 可以打开设置窗口，如下图所示：

![006_选择项目的解释器版本-w975](day01.assets/006_%E9%80%89%E6%8B%A9%E9%A1%B9%E7%9B%AE%E7%9A%84%E8%A7%A3%E9%87%8A%E5%99%A8%E7%89%88%E6%9C%AC.png)

### 3.3 新建项目

#### 1) 命名规则

* 以后 **项目名** 前面都以 **数字编号**，**随着知识点递增，编号递增**
    * 例如：**01_Python 基础**、**02_分支**、**03_循环**...
* 每个项目下的 **文件名** 都以 `hm_xx_知识点` 方式来命名
    * 其中 **xx** 是演练文件的序号

* 注意
    * 1. 命名文件名时建议只使用 **小写字母**、**数字** 和 **下划线**
    * 2. **文件名不能以数字开始**

* 通过 **欢迎界面** 或者菜单 **File** / **New Project** 可以新建项目

#### 2) 演练步骤

* 新建 `01_Python基础` 项目，使用 **Python 3.x 解释器**
* 在项目下新建 `hm_01_hello.py` Python 文件
* 编写 `print("Hello Python")` 代码

## 04. 设置 PyCharm 的字体显示

![007_PyCharm设置编辑器字体-w500](day01.assets/007_PyCharm%E8%AE%BE%E7%BD%AE%E7%BC%96%E8%BE%91%E5%99%A8%E5%AD%97%E4%BD%93.png)

![008_PyCharm设置控制台字体-w500](day01.assets/008_PyCharm%E8%AE%BE%E7%BD%AE%E6%8E%A7%E5%88%B6%E5%8F%B0%E5%AD%97%E4%BD%93.png)

## 05. PyCharm 的升级以及其他

> PyCharm 提供了对 **学生和教师免费使用的版本**

* 教育版下载地址：https://www.jetbrains.com/pycharm-edu/download/#section=linux
* 专业版下载地址：https://www.jetbrains.com/pycharm/download/#section=linux

### 5.1 安装和启动步骤

* 1. 执行以下终端命令，解压缩下载后的安装包

```bash
$ tar -zxvf pycharm-professional-2017.1.3.tar.gz
```

* 2. 将解压缩后的目录移动到 `/opt` 目录下，可以方便其他用户使用

> `/opt` 目录用户存放给主机额外安装的软件

```bash
$ sudo mv pycharm-2017.1.3/ /opt/
```

* 3. 切换工作目录

```bash
$ cd /opt/pycharm-2017.1.3/bin
```

* 4. 启动 `PyCharm`

```bash
$ ./pycharm.sh
```

### 5.2 设置专业版启动图标

* 在**专业版**中，选择菜单 **Tools** / **Create Desktop Entry...** 可以设置任务栏启动图标
    * 注意：设置图标时，需要勾选 `Create the entry for all users`

<img src="day01.assets/009_%E5%88%9B%E5%BB%BA%E6%A1%8C%E9%9D%A2%E5%9B%BE%E6%A0%87.png" alt="009_创建桌面图标-w657" style="zoom:50%;" />

### 5.3 卸载之前版本的 PyCharm 

#### 1) 程序安装

* 1. **程序文件目录** 
    * 将安装包解压缩，并且移动到 `/opt` 目录下
    * **所有的相关文件都保存在解压缩的目录中**
* 2. **配置文件目录**
    * 启动 `PyCharm` 后，会在用户家目录下建立一个 `.PyCharmxxx` 的隐藏目录
    * **保存 `PyCharm` 相关的配置信息**
* 3. **快捷方式文件**
    * `/usr/share/applications/jetbrains-pycharm.desktop` 

> 在 `ubuntu` 中，应用程序启动的快捷方式通常都保存在 `/usr/share/applications` 目录下

#### 2) 程序卸载

* 要卸载 `PyCharm` 只需要做以下两步工作：

* 1. 删除解压缩目录

```bash
$ sudo rm -r /opt/pycharm-2016.3.1/
```

* 2. 删除家目录下用于保存配置信息的隐藏目录

```bash
$ rm -r ~/.PyCharm2016.3/
```

> 如果不再使用 PyCharm 还需要将 `/usr/share/applications/` 下的 `jetbrains-pycharm.desktop` 删掉

### 5.4 教育版安装演练

```bash
# 1. 解压缩下载后的安装包
$ tar -zxvf pycharm-edu-3.5.1.tar.gz

# 2. 将解压缩后的目录移动到 `/opt` 目录下，可以方便其他用户使用
$ sudo mv pycharm-edu-3.5.1/ /opt/

# 3. 启动 `PyCharm`
/opt/pycharm-edu-3.5.1/bin/pycharm.sh
```

> 后续课程**都使用专业版本演练**

#### 设置启动图标

* 1. 编辑快捷方式文件

```bash
$ sudo gedit /usr/share/applications/jetbrains-pycharm.desktop
```

* 3. 按照以下内容修改文件内容，需要注意**指定正确的 `pycharm` 目录**

```
[Desktop Entry]
Version=1.0
Type=Application
Name=PyCharm
Icon=/opt/pycharm-edu-3.5.1/bin/pycharm.png
Exec="/opt/pycharm-edu-3.5.1/bin/pycharm.sh" %f
Comment=The Drive to Develop
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-pycharm
```

# 认识 Python

> 人生苦短，我用 Python —— Life is short, you need Python

![001_人生苦短我用python](day01.assets/001_%E4%BA%BA%E7%94%9F%E8%8B%A6%E7%9F%AD%E6%88%91%E7%94%A8python.jpg)

## 目标

* Python 的起源
* 为什么要用 Python？
* Python 的特点
* Python 的优缺点

## 01. Python 的起源

> Python 的创始人为吉多·范罗苏姆（Guido van Rossum）

<img src="day01.assets/002_%E5%90%89%E5%A4%9A.jpg" alt="002_吉多-w256" style="zoom: 25%;" />

1. 1989 年的圣诞节期间，吉多·范罗苏姆为了在阿姆斯特丹打发时间，决心开发一个新的**解释程序**，作为 ABC 语言的一种继承（**感觉下什么叫牛人**）
2. ABC 是由吉多参加设计的一种教学语言，就吉多本人看来，ABC 这种语言非常优美和强大，是**专门为非专业程序员设计的**。但是 ABC 语言并没有成功，究其原因，吉多认为是**非开放**造成的。吉多决心在 Python 中避免这一错误，并获取了非常好的效果
3. 之所以选中 Python（蟒蛇） 作为程序的名字，是因为他是 BBC 电视剧——蒙提·派森的飞行马戏团（Monty Python's Flying Circus）的爱好者
4. 1991 年，第一个 Python **解释器** 诞生，它是用 C 语言实现的，并能够调用 C 语言的库文件

### 1.1 解释器（科普）

**计算机不能直接理解任何除机器语言以外的语言**，所以必须要把程序员所写的程序语言翻译成机器语言，计算机才能执行程序。**将其他语言翻译成机器语言的工具，被称为编译器**

编译器翻译的方式有两种：一个是**编译**，另外一个是**解释**。两种方式之间的区别在于**翻译时间点的不同**。当编译器**以解释方式运行的时候**，也称之为**解释器**

![001_编译型和解释型语言工作对比-w360](day01.assets/001_%E7%BC%96%E8%AF%91%E5%9E%8B%E5%92%8C%E8%A7%A3%E9%87%8A%E5%9E%8B%E8%AF%AD%E8%A8%80%E5%B7%A5%E4%BD%9C%E5%AF%B9%E6%AF%94.png)

* **编译型语言**：程序在执行之前需要一个专门的编译过程，把程序编译成为机器语言的文件，运行时不需要重新翻译，直接使用编译的结果就行了。程序执行效率高，依赖编译器，跨平台性差些。如 C、C++
* **解释型语言**：解释型语言编写的程序不进行预先编译，以文本方式存储程序代码，会将代码一句一句直接运行。在发布程序时，看起来省了道编译工序，但是在运行程序的时候，必须先解释再运行

#### 编译型语言和解释型语言对比

* **速度** —— 编译型语言比解释型语言执行速度快
* **跨平台性** —— 解释型语言比编译型语言跨平台性好

### 1.2 Python 的设计目标

1999 年，吉多·范罗苏姆向 DARPA 提交了一条名为 “Computer Programming for Everybody” 的资金申请，并在后来说明了他对 Python 的目标：

* 一门**简单直观的语言**并与主要竞争者一样强大
* **开源**，以便任何人都可以为它做贡献
* 代码**像纯英语那样容易理解**
* 适用于**短期**开发的日常任务

这些想法中的基本都已经成为现实，Python 已经成为一门流行的编程语言

### 1.3 Python 的设计哲学

1. 优雅
2. 明确
3. 简单

<!-- > 在 Python 解释器内运行 `import this` 可以获得完整的列表 -->

* Python 开发者的哲学是：**用一种方法，最好是只有一种方法来做一件事**
* 如果面临多种选择，Python 开发者一般会拒绝花俏的语法，而选择**明确没有或者很少有歧义的语法**

> 在 Python 社区，吉多被称为“仁慈的独裁者”

## 02. 为什么选择 Python？

* 代码量少
* ……

> 同一样问题，用不同的语言解决，代码量差距还是很多的，一般情况下 `Python` 是 `Java` 的 **1/5**，所以说 **人生苦短，我用 Python**

## 03. Python 特点

* Python 是**完全面向对象的语言**
    * **函数**、**模块**、**数字**、**字符串**都是对象，**在 Python 中一切皆对象**
    * 完全支持继承、重载、多重继承
    * 支持重载运算符，也支持泛型设计
* Python **拥有一个强大的标准库**，Python 语言的核心只包含 **数字**、**字符串**、**列表**、**字典**、**文件** 等常见类型和函数，而由 Python 标准库提供了 **系统管理**、**网络通信**、**文本处理**、**数据库接口**、**图形系统**、**XML 处理** 等额外的功能
* Python 社区提供了**大量的第三方模块**，使用方式与标准库类似。它们的功能覆盖 **科学计算**、**人工智能**、**机器学习**、**Web 开发**、**数据库接口**、**图形系统** 多个领域

### 面向对象的思维方式

* **面向对象** 是一种 **思维方式**，也是一门 **程序设计技术**
* 要解决一个问题前，首先考虑 **由谁** 来做，怎么做事情是 **谁** 的职责，最后把事情做好就行！
    * **对象** 就是 **谁**
* 要解决复杂的问题，就可以找**多个不同的对象**，**各司其职**，共同实现，最终完成需求

## 04. Python 的优缺点

### 4.1 优点

* 简单、易学
* 免费、开源
* **面向对象**
* 丰富的库
* 可扩展性
    * 如果需要一段关键代码运行得更快或者希望某些算法不公开，可以把这部分程序用 `C` 或 `C++` 编写，然后在 `Python` 程序中使用它们
* ……

### 4.2 缺点

* 运行速度
* 国内市场较小
* 中文资料匮乏


# 第一个 Python 程序

## 目标

* 第一个 `HelloPython` 程序
* `Python 2.x` 与 `3​​.x` 版本简介
* 执行 `Python` 程序的三种方式
    * 解释器 —— `python` / `python3`
    * 交互式 —— `ipython`
    * 集成开发环境 —— `PyCharm`

## 01. 第一个 `HelloPython` 程序

### 1.1 Python 源程序的基本概念

1. Python 源程序就是**一个特殊格式的文本文件**，可以**使用任意文本编辑软件**做 `Python` 的开发
2. Python 程序的 **文件扩展名** 通常都是 `.py`

### 1.2 演练步骤

* 在桌面下，新建 `认识Python` 目录
* 在 `认识Python` 目录下新建 `01-HelloPython.py` 文件
* 使用 **gedit** 编辑 `01-HelloPython.py` 并且输入以下内容：

```python
print("hello python")
print("hello world")
```

* 在终端中输入以下命令执行 `01-HelloPython.py`

```bash
$ python 01-HelloPython.py
```

> `print` 是 `python` 中我们学习的第一个 **函数**
> 
> `print` 函数的作用，可以把 **""** 内部的内容，输出到屏幕上

### 1.3 演练扩展 —— 认识错误（BUG）

#### 关于错误

* 编写的程序**不能正常执行**，或者**执行的结果不是我们期望的**
* 俗称 `BUG`，是程序员在开发时非常常见的，初学者常见错误的原因包括：
    1. 手误
    2. 对已经学习过的知识理解还存在不足
    3. 对语言还有需要学习和提升的内容
* 在学习语言时，不仅要**学会语言的语法**，而且还要**学会如何认识错误和解决错误的方法**

> 每一个程序员都是在不断地修改错误中成长的

#### 第一个演练中的常见错误

* 1> **手误**，例如使用 `pirnt("Hello world")` 

```
NameError: name 'pirnt' is not defined

名称错误：'pirnt' 名字没有定义
```

* 2> 将多条 `print` 写在一行

```
SyntaxError: invalid syntax

语法错误：语法无效
```

> 每行代码负责完成一个动作

* 3> 缩进错误

```
IndentationError: unexpected indent

缩进错误：不期望出现的缩进
```

> * Python 是一个格式非常严格的程序设计语言
> * 目前而言，大家记住每行代码前面都不要增加空格

* 4> **python 2.x 默认不支持中文** 

目前市场上有两个 Python 的版本并存着，分别是 `Python 2.x` 和 `Python 3.x`

* **Python 2.x 默认不支持中文**，具体原因，等到介绍 **字符编码** 时给大家讲解
* Python 2.x 的解释器名称是 **python**
* Python 3.x 的解释器名称是 **python3**

```
SyntaxError: Non-ASCII character '\xe4' in file 01-HelloPython.py on line 3, 
but no encoding declared; 
see http://python.org/dev/peps/pep-0263/ for details

语法错误： 在 01-HelloPython.py 中第 3 行出现了非 ASCII 字符 '\xe4'，但是没有声明文件编码
请访问 http://python.org/dev/peps/pep-0263/ 了解详细信息
```

> * `ASCII` 字符只包含 `256` 个字符，不支持中文
> * 有关字符编码的问题，后续会讲

#### 单词列表

```
* error 错误
* name 名字
* defined 已经定义
* syntax 语法
* invalid 无效
* Indentation 索引
* unexpected 意外的，不期望的
* character 字符
* line 行
* encoding 编码
* declared 声明
* details 细节，详细信息
* ASCII 一种字符编码
```

## 02. `Python 2.x` 与 `3​​.x` 版本简介

目前市场上有两个 Python 的版本并存着，分别是 `Python 2.x` 和 `Python 3.x`

> 新的 Python 程序建议使用 `Python 3.0` 版本的语法

* Python 2.x 是 **过去的版本**
    * 解释器名称是 **python**
* Python 3.x 是 **现在和未来 主流的版本**
    * 解释器名称是 **python3**
    * 相对于 `Python` 的早期版本，这是一个 **较大的升级**
    * 为了不带入过多的累赘，`Python 3.0` 在设计的时候 **没有考虑向下兼容**
        * 许多早期 `Python` 版本设计的程序都无法在 `Python 3.0` 上正常执行
    * Python 3.0 发布于 **2008 年**
    * 到目前为止，Python 3.0 的稳定版本已经有很多年了
        * Python 3.3 发布于 2012
        * Python 3.4 发布于 2014
        * Python 3.5 发布于 2015
        * Python 3.6 发布于 2016
* 为了照顾现有的程序，官方提供了一个过渡版本 —— **Python 2.6**
    * 基本使用了 `Python 2.x` 的语法和库
    * 同时考虑了向 `Python 3.0` 的迁移，**允许使用部分** `Python 3.0` 的语法与函数
    * 2010 年中推出的 `Python 2.7` 被确定为 **最后一个Python 2.x 版本**

> 提示：如果开发时，无法立即使用 Python 3.0（还有极少的第三方库不支持 3.0 的语法），建议
> 
> * 先使用 `Python 3.0` 版本进行开发
> * 然后使用 `Python 2.6`、`Python 2.7` 来执行，并且做一些兼容性的处理

## 03. 执行 Python 程序的三种方式

### 3.1. 解释器 `python` / `python3`

#### Python 的解释器

```bash
# 使用 python 2.x 解释器
$ python xxx.py

# 使用 python 3.x 解释器
$ python3 xxx.py
```

##### 其他解释器（知道）

**Python 的解释器** 如今有多个语言的实现，包括：

* `CPython` —— 官方版本的 C 语言实现
* `Jython` —— 可以运行在 Java 平台
* `IronPython` —— 可以运行在 .NET 和 Mono 平台
* `PyPy` —— Python 实现的，支持 JIT 即时编译

### 3.2. 交互式运行 Python 程序

* 直接在终端中运行解释器，而不输入要执行的文件名
* 在 Python 的 `Shell` 中直接输入 **Python 的代码**，会立即看到程序执行结果

#### 1) 交互式运行 Python 的优缺点

##### 优点
* 适合于学习/验证 Python 语法或者局部代码

##### 缺点
* 代码不能保存
* 不适合运行太大的程序

#### 2) 退出 官方的解释器

##### 1> 直接输入 `exit()`

```python
>>> exit()
```

##### 2> 使用热键退出

在 python 解释器中，按热键 `ctrl + d` 可以退出解释器

<img src="day01.assets/001_%E7%A7%AF%E8%B7%AC%E6%AD%A5%E4%BB%A5%E8%87%B3%E5%8D%83%E9%87%8C.jpg" alt="001_积跬步以至千里" style="zoom:67%;" />

#### 3) IPython

* IPython 中 的 “I” 代表 **交互 interactive**

##### 特点

* IPython 是一个 python 的 **交互式 shell**，比默认的 `python shell` 好用得多
    * 支持自动补全
    * 自动缩进
    * 支持 `bash shell` 命令
    * 内置了许多很有用的功能和函数
* IPython 是基于 BSD 开源的

##### 版本

* Python 2.x 使用的解释器是 **ipython**
* Python 3.x 使用的解释器是 **ipython3**

* 要退出解释器可以有以下两种方式：

##### 1> 直接输入 `exit`

```python
In [1]: exit
```

##### 2> 使用热键退出

在 IPython 解释器中，按热键 `ctrl + d`，`IPython` 会询问是否退出解释器

#### IPython 的安装

```bash
$ sudo apt install ipython
```

## 3.3. Python 的 IDE —— `PyCharm`

### 1） 集成开发环境（IDE）

集成开发环境（`IDE`，Integrated Development Environment）—— **集成了开发软件需要的所有工具**，一般包括以下工具：

* 图形用户界面
* 代码编辑器（支持 **代码补全**／**自动缩进**）
* 编译器／解释器
* 调试器（**断点**／**单步执行**）
* ……

### 2）PyCharm 介绍

* `PyCharm` 是 Python 的一款非常优秀的集成开发环境
* `PyCharm` 除了具有一般 IDE 所必备功能外，还可以在 `Windows`、`Linux`、`macOS` 下使用
* `PyCharm` 适合开发大型项目
    * 一个项目通常会包含 **很多源文件**
    * 每个 **源文件** 的代码行数是有限的，通常在几百行之内
    * 每个 **源文件** 各司其职，共同完成复杂的业务功能

### 3）PyCharm 快速体验

![001_PyCharm的界面结构](day01.assets/001_PyCharm%E7%9A%84%E7%95%8C%E9%9D%A2%E7%BB%93%E6%9E%84.png)

* **文件导航区域** 能够 **浏览**／**定位**／**打开** 项目文件
* **文件编辑区域** 能够 **编辑** 当前打开的文件
* **控制台区域** 能够：
    * 输出程序执行内容
    * 跟踪调试代码的执行
* 右上角的 **工具栏** 能够 **执行(SHIFT + F10)** / **调试(SHIFT + F9)** 代码

<img src="day01.assets/002_PyCharm%E8%BF%90%E8%A1%8C%E5%B7%A5%E5%85%B7%E6%A0%8F.png" alt="002_PyCharm运行工具栏" style="zoom:50%;" />

* 通过控制台上方的**单步执行按钮(F8)**，可以单步执行代码

<img src="day01.assets/003_PyCharm%E8%B0%83%E8%AF%95%E5%99%A8.png" alt="003_PyCharm调试器" style="zoom:50%;" />









