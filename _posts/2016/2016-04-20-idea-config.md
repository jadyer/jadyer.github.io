---
layout: post
title: "idea配置小结"
categories: 工具
tags: idea intellij eclipse netbeans
author: 玄玉
excerpt: 一些idea的优化配置，诸如字体、乱码、显示、格式、主题、快捷键等等。
---

* content
{:toc}


> 本文所列配置项，已适配：ideaIC-2019.3.5<br/>
  idea历史版本下载：<http://www.jetbrains.com/idea/download/other.html>

## 快捷键

 * 自动补全：Alt + 回車
 * 返回上一个方法： Ctrl + Alt + 方向键左
 * 查询某方法被其它地方调用：Ctrl+Alt+H（另外：Alt + F7 也挺好用）
 * 快速输入main函数：键入 main 再按 Ctrl+J 键（或者键入 psvm 再按 Tab 键）
 * 快速输入System.out.println：键入 sout 再按 Tab 键（对应Eclipse中的syso）

## 橘黄色图标插件

从 idea.2016.3 开始，文件夹图标全部换成那种蓝色的，单独拿出来看着有点高科技，放一起实则暴丑

如果想回到之前版本的橘黄色图标，可以用这个 Idea 2016.2 Icon Pack 插件，目前最新版为 v3.2

插件地址：<https://plugins.jetbrains.com/idea/plugin/7285-idea-2016-2-icon-pack>

安装时选择 Install plugin from disk... 再重启 idea 就会看到经典的橘黄色图标啦

另外，ideaIC-2019.3.2中该插件无效，ideaIC-2018.3.6没问题

这时，可以用这个插件：<https://plugins.jetbrains.com/plugin/10777-legacy-icon-pack-for-2018-2->

## 首次运行前的配置

### 64.exe.vmoptions
```
-server
-Xms2048m
-Xmx2048m
-XX:MaxPermSize=1024m
-XX:ReservedCodeCacheSize=512m
-XX:+UseConcMarkSweepGC
-XX:+UseCodeCacheFlushing
-XX:SoftRefLRUPolicyMSPerMB=100
-XX:CICompilerCount=2
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-ea
-Dsun.io.useCanonCaches=false
-Dsun.io.useCanonPrefixCache=false
-Djdk.http.auth.tunneling.disabledSchemes=""
-Djdk.attach.allowAttachSelf=true
-Djdk.module.illegalAccess.silent=true
-Dkotlinx.coroutines.debug=off
-Dsun.awt.keepWorkingSetOnMinimize=true
-Djava.net.preferIPv4Stack=true
-Djsse.enablesSNIExtension=false

```

### idea.properties
```properties
idea.config.path=D:/Develop/JetBrains/ideaIC/JadyerData/config
idea.system.path=D:/Develop/JetBrains/ideaIC/JadyerData/system
idea.plugins.path=${idea.config.path}/plugins
idea.log.path=${idea.system.path}/log
# 编辑大文件时idea容易卡顿：可适当提高该属性值
idea.max.intellisense.filesize=2500
# 禁用控制台输出缓存：大项目开启很多输出时，控制台会很快刷满，导致不能自动输出后面的日志
# 这时可以禁用该值或增大 `idea.cycle.buffer.size=1024` 的配置
idea.cycle.buffer.size=disabled
```

## 全局配置

**在欢迎界面，点击右下方 Configure ，开始进行下列配置**

### 项目参数及JDK
```
# 关闭插件
Plugins---Installed---取消勾选后，重启idea

# 设置JDK
Structure for New Projects---Project Settings---Project---设置JDK
Structure for New Projects---Platform Settings---SDKs---删除自带的jdk11

# 应用控制台颜色输出
Run Configuration Templates for New Projects---Application---VM options: -Dspring.output.ansi.enabled=ALWAYS
对于 SpringBoot 那种 main() 方法直接启动的（Maven或Gradle与之类似，也是右上角配置JVM参数），控制台会彩色输出日志信息

# 应用启动参数短命令行
Run Configuration Templates for New Projects---Application---jre---1.8
Run Configuration Templates for New Projects---Application---Shorten command line---classpath file
```

### 外观及行为配置
```
# 黑色主题及避免中文乱码（此处若选 Yahei Consolas Hybrid，会使得配置窗口很难看，非常难看）
settings---Appearance & Behavior---Appearance---Theme---Darcula，Use custom font，Microsoft YaHei UI，Size=12

# 打开内存使用状态
settings---Appearance & Behavior---Appearance---Show memory indicator

# 隐藏工具栏快捷键下划线
settings---Appearance & Behavior---Appearance---Disable mnemonics in menu

# 打开工程时询问打开窗口（这样在idea选择某个工程打开时，会询问在 This Window 还是 New Window 打开）
settings---Appearance & Behavior---System Settings---Project Opening---Confirm window to open project in

# 应用空闲时自动保存文件
settings---Appearance & Behavior---System Settings---Save files if the IDE is idle for 15 seconds

# 不发送统计文件给JetBrains
settings---Appearance & Behavior---System Settings---Data Sharing---Send usage statistics

# 取消自动更新
settings---Appearance & Behavior---System Settings---Updates---Automatically check updates
```

### 编辑器之通用配置
```
# 设置Ctrl+E弹层的文件个数
settings---Editor---General---Limits---Recent files limit---16

# 自动移除UnuseImport
settings---Editor---General---Auto Import---Add unambiguous...fly 以及 Optimize imports...fly

# 显示行号
settings---Editor---General---Appearance---Show line numbers

# 取消面包屑导航（即打开 HTML／XML 文件时隐藏 html／header／script 等标签）
settings---Editor---General---Breadcrumbs---Show breadcrumbs

# 代码提示区分大小写
settings---Editor---General---Code Completion---不勾选Match case

# 设定折叠或展开的代码类型（勾选则表示该类型代码在文件被打开时默认是被折叠显示的）
settings---Editor---General---Code Folding---勾选Inner classes、Anonymous classes

# 移除文件编辑Tab上的文件icon和后缀
settings---Editor---General---Editor Tabs---Show file extension

# 星号标识编辑过的文件
settings---Editor---General---Editor Tabs---勾选Mark modified (*)

# 移除文件编辑Tab上的茬叉
settings---Editor---General---Editor Tabs---Close button position---None

# 设置文件编辑Tab的最多数
settings---Editor---General---Editor Tabs--Closing Policy---Tab limit---8
```

### 编辑器之代码字体

用的是网上推荐的 Yahei Consolas Hybrid 字体，下载地址如下（三个地址都是同一个文件）

<http://download.csdn.net/detail/jadyer/9719438>

<https://gitee.com/a42/YaHei-Consolas-Hybrid-1.12>

<https://github.com/GitHubNull/YaHei-Consolas-Hybrid-1.12>

之前的两种安装方法：双击 ttf 文件再点击安装按钮，或把 ttf 文件拷贝到 C:\Windows\Fonts\ 目录

但新版 Win10 有一个特性是：默认安装字体只是给当前用户安装的，而 2018.3 无法良好的适配该特性，导致获取不到新安装字体

解决办法就是：右键 ttf 文件，选择为所有用户安装即可

再回到 idea 配置：settings---Editor---Font---Yahei Consolas Hybrid，Size=14

### 编辑器之代码风格
```
# 控制台字号（先拷贝一份 Scheme 的 Darcula 配置，新命名为 Darcula_Jadyer）
settings---Editor---Color Scheme---Console Font---Use console font instead of the default---Size=12

# 文件换行符使用Unix格式（先拷贝一份 Scheme 的 Default 配置，新命名为 Default_Jadyer）
settings---Editor---Colors Style---Line separator---Unix and OS X (\n)

# 函数花括号显示为对称结构（这里我没有改，还是默认的End of line）
settings---Editor---Colors Style---Java---Wrapping and Braces---Braces placement---Next line

# import每个类而非整个包（当import某个包下的类超过这里设置的个数时，就会换成星号来代替，比如import java.util.*）
settings---Editor---Colors Style---Java---Imports---Class count to use import with---64

# 注释时双斜杠位置为代码头部
settings---Editor---Colors Style---Java---Code Generation---不勾选Line comment at first column

# 注释的双斜线与注释内容之间有且仅有一个空格
settings---Editor---Colors Style---Java---Code Generation---勾选Add a space at comment start
```

### 编辑器之关闭检查

先拷贝一份 Profile 的 Default 配置，新命名为 Default_Jadyer

```
# DefaultFileTemplate
settings---Editor---Inspections---General---不勾选Default File Template Usage

# 方法参数是相同值
settings---Editor---Inspections---Java---Declaration redundancy---不勾选Actual method parameter is the same constant

# Return value of the method is never used
settings---Editor---Inspections---Java---Declaration redundancy---不勾选Method can be void

# neverused
settings---Editor---Inspections---Java---Declaration redundancy---不勾选Unused declaration

# lamba转化
settings---Editor---Inspections---Java---Java language level migration aids---Java 8---不勾选Anonymous type can be replaced with lambda

# @create@author@see（前者针对@create@author，后者针对@see）
settings---Editor---Inspections---Java---Javadoc---不勾选Declaration has Javadoc problems和Declaration has problems in Javadoc references

# 方法和类同名
settings---Editor---Inspections---Java---Naming conventions---不勾选Method name same as class name

# 未处理方法返回值（比如java.io.File.delete()）
settings---Editor---Inspections---Java---Probable bugs---不勾选Result of method call ignored

# serialVersionUID（然后回到类文件中，光标放到类名上，Alt+Enter就会提示生成serialVersionUID）
settings---Editor---Inspections---Java---Serialization issues---勾选Serializable class without serialVersionUID
settings---Editor---Inspections---Java---Serialization issues---勾选Non-serializable class with serialVersionUID

# properties的属性未使用
settings---Editor---Inspections---Properties Files---不勾选Unused Property

# 取消拼写检查
settings---Editor---Inspections---Spelling---不勾选
```

### 编辑器之注释模板

这是设置文件头注释（创建新文件时的）

settings---Editor---File and Code Templates---Includes---File Header---编辑为如下

```
/**
 * Created by 玄玉<https://jadyer.cn/> on ${DATE} ${TIME}.
 */
```

接下来是自定义方法上的注释

settings---Editor---Live Templates---右上角 `+` 选择 Template Group---输入模板组名：JadyerGroup

再点击 JadyerGroup---右上角 `+` 加号选择 Live Template---设置自定义的触发注释输出的字母

然后在最下方的 No applicable contexts. Define 处选择模板适用范围（截图中我勾选的是 **Java** 范围）

接下来填写自定义的注释内容，如截图所示（我设置的就是输入 `c` ，然后按 `Tab` 键，就会生成方法注释）

其中时间位置可以用 `$date$` 或者 `$time$` 占位，并点击 Edit variables 按钮，然后在下拉框选择 `date()` 和 `time()`

```
/**
 *
 * Comment by 玄玉<https://jadyer.cn/> on $date$ $time$.
 */
```

![](https://ae01.alicdn.com/kf/H7ad4863359204e2a857bf832bc20b055M.png)

### 编辑器之其它

```
# 资源文件的中文显示
settings---Editor---File Encodings---Global Encoding---UTF-8
settings---Editor---File Encodings---Project Encoding---UTF-8
settings---Editor---File Encodings---Default encoding for properties files---UTF-8
settings---Editor---File Encodings---Transparent native-to-ascii conversion

# 隐藏文件和文件夹
settings---Editor---File Types---Ignore files and folders---target;.gradle;*.iml;*.idea;

# 版本控制下文件变化的显示（调整文件夹显示颜色，配置在Version Control---File Status Color）
settings---Version Control---Show directories with changed descendants

# Markdown文件默认以编辑模式打开
settings---Languages & Frameworks---Default layout---Editor only
```

### 快捷键

先拷贝一份 keymap 的 Windows 配置，新命名为 Windows_Jadyer

```
# 修改代码提示快捷键
settings---keymap---搜索框输入basic（idea默认的是Ctrl+空格，和我们输入法冲突）---Ctrl+B

# 设置全屏模式快捷键（即工具类 View 菜单下面的 Enter Full Screen）
settings---keymap---搜索框输入full screen（搜索到的是Toggle Full Screen mode）---F11

# 修改文件关闭快捷键
settings---keymap---快捷键搜索Ctrl+F4（搜索到的是Window--Editor Tabs--Close）---Ctrl+W

# 修改类方法列表快捷键
settings---keymap---快捷键搜索Ctrl+F12（搜索到的是Main menu--Navigate--File Structure）---Ctrl+O
```

### Maven及构建配置

```
# Maven配置
settings---Build,Execution,Deployment---Build Tools---Maven---勾选Print exception stack traces，并选择本机Maven及本地仓库
settings---Build,Execution,Deployment---Build Tools---Maven---Importing---Import Maven projects automatically
settings---Build,Execution,Deployment---Build Tools---Maven---Importing---Automatically download---勾选Sources
settings---Build,Execution,Deployment---Build Tools---Maven---Importing---JDK for importer---选择本机安装的1.8
settings---Build,Execution,Deployment---Build Tools---Maven---Runner---JRE---选择本机安装的1.8

# 自动编译
settings---Build,Execution,Deployment---Compiler---Build project automatically

# 编译报告OutOfMemoryError
settings---Build,Execution,Deployment---Compiler---Shared build process heap size(Mbytes)---1024
```

### 编译报错

* 报告：找不到符号、未结束的字符串文字
  > 1、UTF-8文件分有BOM和无BOM，idea默认使用的编译器是javac，而其只能编译无BOM的文件（settings---settings---Editor---File Encodings---右侧BOM设置）<br/>
  　　很多eclipse用户在使用idea开发eclipse项目时会遇到此问题<br/>
  　　主要是因为eclipse的编译器是eclipse，其支持有BOM的文件编译。故需对文件进行BOM去除<br/>
  2、批量去除BOM，可以Google：批量去除BOM、批量转换无BOM等关键字，网上已有各种方案<br/>
  3、除了通过去除BOM，还有设置idea的编译器为eclipse，但是一般不建议这样做<br/>
  4、若仍无法解决，而且也确认了idea各配置编码都是UTF-8，报错文件编码也是UTF-8无BOM的<br/>
  　　那还有一种可能也会出现这种情况：项目配置文件有问题<br/>
  　　项目编码的配置文件在：/项目目录/.idea/encodings.xml。你要是能修改明白就修改<br/>
  　　要是不会修改，那就删掉.idea整个目录，重启idea重新配置这个项目即可

### 清除缓存和索引

idea的缓存和索引主要用来加快文件查询、代码提示等操作的速度，但其缓存和索引文件偶尔会莫名损坏

此时打开idea，很有可能idea会报告各种奇妙的错误，甚至打不开项目，idea主题还原为默认状态等等

此时便需清除缓存和索引，清除之后下次启动时就会重建

File-->Invalidate Caches / Restart（此时会弹出一个提示框，内容如下）

```
The caches will be invalidated and rebuilt on the next startup.
WARNING: Local History will be also cleared.
Would you like to continue?
```

一般建议点击 Invalidate and Restart，这样会清除的比较干净

**注意**：若项目未加入版本控制，而又需要文件的历史记录，则提前备份下 ${idea.system.path}\LocalHistory\ 目录

## datagrip的几个配置

### 64.exe.vmoptions
```
-server
-Xms1024m
-Xmx1024m
-XX:MaxPermSize=512m
-XX:ReservedCodeCacheSize=512m
-XX:+UseConcMarkSweepGC
-XX:+UseCodeCacheFlushing
-XX:SoftRefLRUPolicyMSPerMB=100
-XX:CICompilerCount=2
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-ea
-Dsun.io.useCanonCaches=false
-Dsun.io.useCanonPrefixCache=false
-Djdk.http.auth.tunneling.disabledSchemes=""
-Djdk.attach.allowAttachSelf=true
-Djdk.module.illegalAccess.silent=true
-Dkotlinx.coroutines.debug=off
-Dsun.awt.keepWorkingSetOnMinimize=true
-Djava.net.preferIPv4Stack=true
-Djsse.enablesSNIExtension=false

```

### idea.properties
```properties
idea.config.path=D:/Develop/JetBrains/DataGrip/JadyerData/config
idea.system.path=D:/Develop/JetBrains/DataGrip/JadyerData/system
idea.plugins.path=${idea.config.path}/plugins
idea.log.path=${idea.system.path}/log
```

### 配置工作空间

其实 datagrip 也有工作空间和项目的概念的（在欢迎屏幕上才能看见）

默认的，是直接进默认工作空间（不像 idea 那样会让你来选择打开哪个项目）

datagrip 默认的工作空间是在 idea.config.path/projects/ 目录里面的，项目名叫 default

我们也可以自定义工作空间，并显示欢迎屏幕

欢迎界面Customize---All settings...---Appearancd & Behavior---System Settings---Default directory

欢迎界面Customize---All settings...---Appearancd & Behavior---System Settings---Show Welcome screen

**注：初次启动时，配置向导有一步 Attaching a directory... 不用理它，它不是配置工作空间**

### 快捷键

| 快捷键 | 用途 |
|:-----------------|:--------|
| Ctrl + /         | 注释SQL |
| Ctrl + Shift + / | 注释SQL |
| Ctrl + Enter     | 执行SQL（未选中SQL的情况下，会弹框询问你执行哪条SQL） |
| Ctrl + N         | 快速导航到指定的表、视图、函数等（跟 idea 一样） |
| Shift + Shift    | 可以搜索任何想搜索的内容（跟 idea 一样） |

### 常用配置
```
# 连接数据库失败（serverTimezone改成上海，还能避免SQL查询出的时间比真实落库时间早 8 个小时的问题）
File---Data Sources...---Drivers---MySQL---设置连接时使用本地 jar 以及 serverTimezone 等参数

# 消除绿框（默认在手写SQL时，会有一个绿框跟随着）
settings---Editor---Code Scheme---Database---Console---Statement to execucte---取消勾选Effects

# 关键词大写
settings---Editor---Code Style---SQL---General---Case选项卡---Word Case---Keywords---To Upper

### 执行光标所在的语句（此时SQL须以分号结尾，除非手动选中整个SQL，那时就会直接执行选中的SQL）
settings----Database---General---Execute---When inside statement execute---Smallest statement
```

### 常见用法
```
# 结果集中设置字段值为NULL
在查询出来的结果集中，字段上右键，Set NULL，即可

# 多窗口查看结果
若希望查询在新的 tab 中展示，而保留当前查询出来的结果集，那么点击现有结果集上方的 Pin Tab（像针的图标）即可

# 以列的方式查看单条数据信息
在表的数据列表的某个字段值上，或，查询出来的结果集的某个字段上，按 Ctrl + Q 键，就能以列的方式查看这一条数据

# 查看本地历史SQL
查询控制台上，右键，Local History，Show History、

# 结果集中搜索
在查询出来的结果集上，按 Ctrl + F 搜索内容（支持正则）

# 关键字导航
查询控制台上，鼠标放到表名上（也可以是字段名或函数名），按下 Ctrl，再点击鼠标左键，就会立即定位到具体表上
```

### 字符集混用或无效

当数据库服务端设置为 UTF8MB4 后，datagrip 在操作数据库时，可能会提示下面信息

`llegal mix of collations (utf8mb4_general_ci,IMPLICIT) and (utf8mb4_0900_ai_ci,IMPLICIT) for operation '='`

这时，可以在查询控制台确认一下

```
SHOW VARIABLES LIKE 'COLLATION_%';

Variable_name           Value
collation_connection	utf8mb4_general_ci
collation_database	utf8mb4_unicode_ci
collation_server	utf8mb4_unicode_ci
```

解决办法就是在数据库连接URL上增加：connectionCollation=utf8mb4_general_ci

### 导入和导出表数据

导出数据就通过命令行来做吧（Windows---运行---CMD）

```sql
C:\Users\Jadyer>mysqldump -h127.0.0.1 -uroot -pxuanyu -d ifs --single-transaction --default-character-set=UTF8 > C:\Users\Jadyer\Desktop\ifs.sql

-- ifs 代表数据库名
--  -d 表示只导出表结构，不导出数据，若需导出数据，去掉该参数即可

-- 如果出现下面的提示，那就加上 --single-transaction 参数（否则不用）
mysqldump: Got error: 1044: Access denied for user 'report'@'%' to database 'bi' when using LOCK TABLES

-- 另外，导出时，可能会出现下面的提示，可以不理它（不会影响导出的表结构和数据量）
mysqldump: Error: 'Access denied; you need (at least one of) the PROCESS privilege(s) for this operation' when trying to dump tablespaces
```

导入就简单了：先创建数据库，然后在 datagrip 里的新数据库上右键，选择 Run SQL Script... 即可

```sql
CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARSET utf8mb4 COLLATE utf8mb4_unicode_ci;
```