[TOC]

# Ubuntu安装

## 前置 - 压缩卷

为了给Ubuntu充足的磁盘空间我们需要腾出一部分未分配空间给它，但有时候，明明我们的磁盘剩余空间很大，但能够压缩的空间却很少，这说明磁盘内的“碎片”太多，需要我们去整理。

这篇[文章](https://blog.csdn.net/qq_32103873/article/details/132516221)几乎将所有能搜到的方法给总结了，而我则是使用了里面提到的MyDefrag工具才解决，关于这个工具的使用还有一篇[文章](https://blog.csdn.net/ZXY_aaaaa/article/details/128538818)详述它的用法。

## 下载镜像

1. [Iso镜像](https://cn.ubuntu.com/download)下载

2. 制作U盘启动盘，参考Debian安装

## 安装系统

> “坑”
>
> 1. 在进入`Install Ubuntu`界面时，需要按下`e`键，进入配置界面，找到`quiet splash ---`这个字符串，把后面的`---`改为`nomodeset`，意思是禁用掉自带的显卡设置，然后`F10`启动安装。
>
> 2. 系统语言选择`English`，否则后面会有的字符错乱的情况。
>
> 3. 进入设置完后，会要求重启，但重启后会“黑屏”（就一道下划线在那里闪动），这是因为没有显卡驱动（我的是这样）。解决方案：`ctrl+alt+t`或`ctrl+alt+f2\3\4\5`随便一个进入终端，输入以下命令。
>
>    ```shell
>    ubuntu-drivers devices  # 显示硬件及推荐驱动
>    sudo apt-get update  # 更新软件源
>    sudo ubuntu-drivers autoinstall  # 安装推荐的驱动
>    ```
>
> 4. 磁盘分配，选中我们留出的空白磁盘空间，设置挂载点`\`，之后会更新，然后我们在下面选择，刚才我们选的空白区的`Device`进行安装

## 美化

### Mac Big Sur 

详见文章[Blog。](https://blog.nineya.com/archives/106.html)

## Github配置ssh key的步骤

参考[文章](https://blog.csdn.net/weixin_42310154/article/details/118340458)。文章里的`ssh-keygen -t rsa -C "xxx@xxx.com" //执行后一直回车即可`里的`xxx@xxx.com`可随便命名。

设置成功后，即可不需要账号密码clone和push代码。

**注意之后在clone仓库的时候要使用ssh的url，而不是https！**

## 图床配置

PicGo[下载地址](https://github.com/Molunerfinn/PicGo/releases)

注意：在Linux系统选择Applmage后缀的版本。

[Ubuntu PicGo安装和腾讯云图床配置，超详细！！！](https://blog.csdn.net/qq_42584874/article/details/116534328)

在Typora里上传图像（右键 -- Upload）可以开梯子，直接用PicGo在没有配置代理时不能开梯子，否则会上传失败。

[什么是AppImage，以及如何在Ubuntu中安装它们？](https://ubunlog.com/zh-CN/%E4%BB%80%E4%B9%88%E6%98%AFappimage%E4%BB%A5%E5%8F%8A%E5%A6%82%E4%BD%95%E5%9C%A8ubuntu%E4%B8%AD%E5%AE%89%E8%A3%85%E5%AE%83%E4%BB%AC/)

该[文章](https://linux.cn/article-14619-1.html)解释了为什么运行AppImage文件时没反应，用终端运行时报错：

```shell
dlopen(): error loading libfuse.so.2
AppImages require FUSE to run. 
```

总结起来一句话：

```shell
sudo apt install libfuse2
```

## Git快速入门

Link：[https://nju-projectn.github.io/ics-pa-gitbook/ics2024/git.html](https://nju-projectn.github.io/ics-pa-gitbook/ics2024/git.html)

### 光玉

想象一下你正在玩Flappy Bird, 你今晚的目标是拿到100分, 不然就不睡觉. 经过千辛万苦, 你拿到了99分, 就要看到成功的曙光的时候, 你竟然失手了! 你悲痛欲绝, 滴血的心在呼喊着, "为什么上天要这样折磨我? 为什么不让我存档?"

想象一下你正在写代码, 你今晚的目标是实现某一个新功能, 不然就不睡觉. 经过千辛万苦, 你终于把代码写好了, 保存并编译运行, 你看到调试信息一行一行地在终端上输出. 就要看到成功的曙光的时候, 竟然发生了段错误! 你仔细思考, 发现你之前的构思有着致命的错误, 但之前正确运行的代码已经永远离你而去了. 你悲痛欲绝, 滴血的心在呼喊着, "为什么上天要这样折磨我?" 你绝望地倒在屏幕前... 这时, 你发现身边渐渐出现无数的光玉, 把你包围起来, 耀眼的光芒令你无法睁开眼睛... 等到你回过神来, 你发现屏幕上正是那份之前正确运行的代码! 但在你的记忆中, 你确实经历过那悲痛欲绝的时刻... 这一切真是不可思议啊...

### 人生如戏, 戏如人生

人生就像不能重玩的Flappy Bird, 但软件工程领域却并非如此, 而那不可思议的光玉就是"版本控制系统". 版本控制系统给你的开发流程提供了比朋也收集的更强大的光玉, 能够让你在过去和未来中随意穿梭, 避免上文中的悲剧降临你的身上.

没听说过版本控制系统就完成实验, 艰辛地排除万难, 就像游戏通关之后才知道原来游戏可以存档一样, 其实玩游戏的时候进行存档并不是什么丢人的事情.

在实验中, 我们使用 `git` 进行版本控制. 下面简单介绍如何使用 `git` .

#### 游戏设置

首先你得安装 `git` :

```
apt-get install git
```

安装好之后, 你需要先进行一些配置工作. 在终端里输入以下命令

```
git config --global user.name "Zhang San"        # your name
git config --global user.email "zhangsan@foo.com"    # your email
git config --global core.editor vim            # your favourite editor
git config --global color.ui true
```

经过这些配置, 你就可以开始使用 `git` 了.

在实验中, 你会通过 `git clone` 命令下载我们提供的框架代码, 里面已经包含一些 `git` 记录, 因此不需要额外进行初始化. 如果你想在别的实验/项目中使用 `git` , 你首先需要切换到实验/项目的目录中, 然后输入

```
git init
```

进行初始化.

#### 查看存档信息

使用

```
git log
```

查看目前为止所有的存档.

使用

```
git status
```

可以得知, 与当前存档相比, 哪些文件发生了变化.

#### 存档

你可以像以前一样编写代码. 等到你的开发取得了一些阶段性成果, 你应该马上进行"存档".

首先你需要使用 `git status` 查看是否有新的文件或已修改的文件未被跟踪, 若有, 则使用 `git add` 将文件加入跟踪列表, 例如

```
git add file.c
```

会将 `file.c` 加入跟踪列表. 如果需要一次添加所有未被跟踪的文件, 你可以使用

```
git add -A
```

如果想要添加所有文件，你可以使用

```
git add .
```

但这样可能会跟踪了一些不必要的文件, 例如编译产生的 `.o` 文件, 和最后产生的可执行文件. 事实上, 我们只需要跟踪代码源文件即可. 为了让 `git` 在添加跟踪文件之前作筛选, 你可以编辑 `.gitignore` 文件(你可以使用 `ls -a` 命令看到它), 在里面给出需要被 `git` 忽略的文件和文件类型.

把新文件加入跟踪列表后, 使用 `git status` 再次确认. 确认无误后就可以存档了, 使用

```
git commit [-m '#######']
```

提交工程当前的状态. 执行这条命令后, 将会弹出文本编辑器, 你需要在第一行中添加本次存档的注释, 例如"fix bug for xxx". 你应该尽可能添加详细的注释, 将来你需要根据这些注释来区别不同的存档. 编写好注释之后, 保存并退出文本编辑器, 存档成功. 你可以使用 `git log` 查看存档记录, 你应该能看到刚才编辑的注释.

如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下：

```
git commit -a
```

注意：如果你添加了新文件（夹）还是需要进行add！！！

再执行以下命令：

```
$ git commit -am '修改 hello.php 文件'
[master 71ee2cb] 修改 hello.php 文件
 1 file changed, 1 insertion(+)
```

#### 读档

如果你遇到了上文提到的让你悲痛欲绝的情况, 现在你可以使用光玉来救你一命了. 首先使用 `git log` 来查看已有的存档, 并决定你需要回到哪个过去. 每一份存档都有一个hash code, 例如 `b87c512d10348fd8f1e32ddea8ec95f87215aaa5` , 你需要通过hash code来告诉 `git` 你希望读哪一个档. 使用以下命令进行读档:

```
git reset --hard b87c
```

其中 `b87c` 是上文hash code的前缀: 你不需要输入整个hash code. 这时你再看看你的代码, 你已经成功地回到了过去!

但事实上, 在使用 `git reset` 的hard模式之前, 你需要再三确认选择的存档是不是你的真正目标. 如果你读入了一个较早的存档, 那么比这个存档新的所有记录都将被删除! 这意为着你不能随便回到"将来"了.

#### 第三视点

当然还是有办法来避免上文提到的副作用的, 这就是 `git` 的分支功能. 使用命令

```
git branch
```

查看所有分支. 其中 `master` 是主分支, 使用 `git init` 初始化之后会自动建立主分支.

读档的时候使用以下命令

```
git checkout b87c
```

而不是 `git reset` . 这时你将处于一个虚构的分支中, 你可以

- 查看 `b87c` 存档的内容

- 使用以下命令切换到其它分支

  ```
  git checkout 分支名
  ```

- 对代码的内容进行修改, 但你不能使用

  ```
  git commit
  ```
  
  进行存档, 你需要使用

  ```
  git checkout -B 分支名
  ```

  把修改结果保存到一个新的分支中, 如果分支已存在, 其内容将会被覆盖

不同的分支之间不会相互干扰, 这也给项目的分布式开发带来了便利. 有了分支功能, 你就可以像第三视点那样在一个世界的不同时间(一个分支的多个存档), 或者是多个平行世界(多个分支)之间来回穿梭了.

```
git push
```

将代码等推送到远程仓库。

#### 更多功能

以上介绍的是 `git` 的一些基本功能, `git` 还提供很多强大的功能, 例如使用 `git diff` 比较同一个文件在不同版本中的区别, 使用 `git bisect` 进行二分搜索来寻找一个bug在哪次提交中被引入...

其它功能的使用请参考 `git help` , `man git` , 或者在网上搜索相关资料.

补充：

如果仓库中代码进行了更新，想要在本地也更新怎么办？

这时就可以使用

```
git pull
```

一键拉取代码到本地，但有时候我们在本地仓库也进行了更改（还没有提交到远程仓库中），这时会提示

```shell
(base) leeson@leeson-ASUS-TUF:~/Documents/Md/OS/OS$ git pull
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 1.43 KiB | 1.43 MiB/s, done.
From github.com:jacket-mouse/OS
   57c39b3..2a19040  main       -> origin/main
Updating 57c39b3..2a19040
error: Your local changes to the following files would be overwritten by merge:
	200 - Algorithm/算法导论.md
Please commit your changes or stash them before you merge.
Aborting
```

此时，我们本地仓库的内容还并未改变，只有在进行合并操作之后才会改变，而此时我们无法进行合并，直接合并会将我们在本地仓库进行的修改覆盖掉，这可怎么办呢？其实我们可以用一个新的命令来解决这一问题，这个命令就是

```
git stash save "xxxx your description"
```

该命令可以暂存我们的本地修改到一个暂存区，使用完该命令之后，你可以发现，我们在本地的修改“不见了”，恢复到了我们上次提交时的状态。这是我们就可以放心大胆的合并了

```
git merge
```

合并完之后，我们还需要将我们存到暂存区的修改恢复，运行下面的命令

```
git stash pop
```

此时，产生冲突

```shell
(base) leeson@leeson-ASUS-TUF:~/Documents/Md/OS/OS$ git stash pop
Auto-merging 200 - Algorithm/算法导论.md
CONFLICT (content): Merge conflict in 200 - Algorithm/算法导论.md
On branch main
Your branch is up to date with 'origin/main'.

Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
	both modified:   "200 - Algorithm/\347\256\227\346\263\225\345\257\274\350\256\272.md"

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.
```

这就需要我们去产生冲突的文件里，手动解决冲突了，这样，就完美的解决了问题。

当然，我们也可以自己建一个分支，这样只有在分支合并时需要上述操作，平时两个分支互不影响。

- 特殊情况

> 当忘记远程仓库有提交，而自己在本地没有提前stash，而是已经commit并且push之后，这种情况如何解决？

```shell
To github.com:jacket-mouse/OS.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'github.com:jacket-mouse/OS.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

此时，我们想stash发现已经无效了。

```shell
(base) leeson@leeson-ASUS-TUF:~/Documents/Md/OS/OS$ git stash save "OS"
No local changes to save
```

根据提示，我们先进行pull操作，处理完冲突后，再进行push操作。

```shell
(base) leeson@leeson-ASUS-TUF:~/Documents/Md/OS/OS$ git pull origin main
From github.com:jacket-mouse/OS
 * branch            main       -> FETCH_HEAD
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

发现又有问题，询问AI之后，发现我们没有设置Git解决分歧的策略。于是，我们采用默认策略：在拉取时使用合并（merge）策略，将远程分支的更改合并到本地分支。

```shell
(base) leeson@leeson-ASUS-TUF:~/Documents/Md/OS/OS$ git config pull.rebase false
```

之后，成功进行拉取操作，可能需要处理冲突，最后，我们将自己在本地的修改重新提交。

#### 问题总结

> github不显示提交记录
>
> github上提交完代码之后，绿色小方块没有亮，也没有提交记录。查资料之后，原因是github绑定的邮箱与本地的邮箱不同的问题。

首先，查看本地邮箱：在git bash中输入

```shell
git config --global user.email
```

查看信息是否与GitHub中的一样，我的邮箱不同，所以这里我修改本地的邮箱：

```shell
git config --global user.email "2653xxxxx@qq.com"
```

为了确认已经修改成功，检查一下：

```shell
git config --global user.email即可
```

## [CUDA](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=runfile_local)安装

自己安装完CUDA后重启，出现了文章内的描述安装完NVIDIA驱动的界面，当时直接点了`continue boot`导致又出现了安装系统“坑”中第三个情况，所以又重新安装驱动，重启。开机后还是出现文章内的描述安装完NVIDIA驱动的界面，所以按照步骤选了`Enroll MDK` -> 输了一个密码 -> `reboot`就恢复了，但CUDA还是没安装上。

所以，参考该篇[文章](https://blog.csdn.net/m0_73860872/article/details/127276979)打算再安装一次。

注意：

- 版本号记得根据自己的情况进行更改。
- CUDA安装选项有一个[kernel objects nvidia-fs](https://geekice.com/index.php/archives/28/)不同。

## Tools

### fishshell

[fish安装](https://linux.cn/article-10622-1.html)

[oh-my-fish](https://github.com/oh-my-fish/oh-my-fish)

快捷键：补全fish供的命令，除了右键→，还可以是Ctrl+F

### 中文输入法

[Ubuntu16.04系统安装搜狗输入法详细教程](https://blog.csdn.net/areigninhell/article/details/79696751#commentBox)

### 截图

- 系统截图：`Shift + PrintScreen` 

###  一键截图美化工具

- [Xnapper](https://xnapper.com/) 只支持苹果全家桶
- [Pika](https://pika.style/templates/screenshot-editor)在线版，太贵了$120一年

### 编译器

- GCC编译器

gcc 能够支持多种 C 语言的变体，例如 K＆R C 和 ANSI C；GCC 也是一个交叉平台编译器，能够开发不同 CPU 体系结构的软件；同时，GCC 也能够进行代码优化，提高执行程序的运行速度。gcc 编译过程分为 4 个阶段：

- 预处理
- 编译
- 汇编
- 连接

最简单的 C 语言编译的例子：
用 vim 建立一个 hello.c 文件

```shell
$vi hello.c
```

```c
#include <stdio.h>
int main(void)
{
printf(“Hello World!\n”);
return 0;
}
```

最后输入字符`<Esc>:wq`,返回命令行，键入以下编译命令：
```shell
$gcc hello.c
```
如果没有错误 gcc 将生成默认的可执行文件 a.out,执行 a.out:

```shell
$./a.out
Hello World!
$
```

gcc 带有多达数页的编译选项，我们仅列出最常用的几项：

- -o 可执行文件名  指定输出的可执行文件名，而不是默认的 a.out
- -c  只编译生成.o 的目标文件,不连接生成可执行文件
- -s  只编译生成.s 的汇编文件,不连接生成可执行文件
- -g  在可执行文件中加入标准调试信息
- -Wall  允许 GCC 发出警告型错误信息

选项使用的例子:对以上 hello.c 使用-o,-g 常用选项重新编译、执行:

```shell
$gcc -g hello.c -o hello
$./hello
Hello World!
$`
```

GCC 默认的扩展文件名：

- .c  C 语言源代码
- .C .cc  C++语言源代码
- .i  预处理后的 C 语言源代码
- .ii  预处理后的 C++语言源代码
- .S .s 汇编语言源代码
- .o 编译后的目标代码
- .a .so  编译后的库代码




- G++编译器

g++是构建于 gcc 基础上的 C++语言编译器。

## FTP

主要用来提交学校的实验报告，上网搜了一下，找了一个Filezilla工具，直接可以在Ubuntu应用商店安装，但这个工具对中文的支持不是很好，如果有乱码可以看这篇文章[FileZilla中文乱码解决方法](https://blog.csdn.net/java_huashan/article/details/49421525)。

## Slidev

[Slidev](https://cn.sli.dev/)(slide + dev, **/slʌɪdɪv/**) 是基于 Web 的幻灯片制作和演示工具。它旨在让开发者专注在 Markdown 中编写内容，同时拥有支持 HTML 和 Vue 组件的能力，并且能够呈现像素级完美的布局，还在你的演讲稿中内置了互动的演示样例。

它使用了功能丰富的 markdown 文件来生成精美的幻灯片，具有即时重载的体验。它还拥有很多内置的集成功能，如实时编码、导出 PDF、演讲录制等。由于 Slidev 是由 web 驱动的，因此你可以使用它进行任何操作 —— 具有无限的可能性。

## Apple Music

> Description:
>
> My Ubuntu is 20.04, and when I open apple music, only an error window pop up. And when I press the OK button, the App will end up and exit. I want to know how could I fix it.

[Error: Failed to install Widevine components](https://ttys3.dev/blog/apple-music-electron)

## VSCode

### Ubuntu20.04中VScode不能输入中文解决

项目场景：
ubuntu20.04版本中安装vscode

问题描述：
在ubuntu中安装造成vscode中不能输入中文，例如添加注释时，总是出现补齐关键词，无法用拼音输入汉字。

原因分析：
vscode有好几种安装方法，有通过应用商店直接安装的，也有通过命令安装的，其中有些安装方法比如应用商店安装的是vscode的阉割版，造成无法输入汉字

解决方案：

1. 在应用商店里找到已安装目录下的vscode
2. 点击移除VScode
3. 使用apt安装visual studio code
4. vscode在官方的微软apt源库中可用，在终端中依次运行以下
   更新软件包索引并安装依赖软件

```shell
sudo apt update 
sudo apt install software-properties-common apt-transport-https wget
```
使用命令插入Microsoft GPG key
```shell
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
```
启动vscode源仓库，输入
```shell
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```
apt软件源被启动，安装vscode软件包，需要一会儿时间
```shell
sudo apt install code
```
当新版本发布时更新升级安装包
```shell
sudo apt update
sudo apt upgrade
```
安装成功，启动VScode

```shell
code
```


原文链接：https://blog.csdn.net/m0_44999129/article/details/123125650

### 保存输入密码问题

问题描述：

> 有时我们发现，文件夹是处在一个上锁的状态，这很形象，可以在Ubuntu系统文件夹里，看到文件夹被“锁住”了，在这样的情况下，每当我们对文件夹内的文件进行修改后，保存就需要管理员权限，直观地表现就是输入密码。

解决方案：

根据问题描述我们可以知道，原因是权限，所以我们直接用`chmod`命令，赋予当前用户对文件夹的完全访问权限就可以。
