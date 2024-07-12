# Debian安装

## 制作一个 Debian 的可启动 USB

大多数设备都有一个预装的操作系统；但是，你可以根据自己的喜好或要求改变操作系统。如今，计算机甚至没有内置的 DVD/CD 驱动器；因此，用户除了改用新方法外别无选择。通常情况下，笔式驱动器被用来获得新的操作系统；你可以通过使用操作系统的 iso 图像使 USB 可启动。为了使其可启动，有几个工具可以帮助从 iso 镜像中提取重要文件，然后将这些文件添加到 USB 驱动器中，使其发挥作用。
### 先决条件

以下是在你的上级操作系统中必须具备的先决条件包。

- **Debian 11** 的 ISO 镜像：使 USB 可启动的主要要求是获得操作系统的 ISO 镜像；要下载蝶变 11 的 ISO 镜像，请点击下面。
- [**下载 Debian 11 ISO**](https://link.juejin.cn/?target=https%3A%2F%2Fwww.debian.org%2Fdevel%2Fdebian-installer%2F "https://www.debian.org/devel/debian-installer/")
- **USB 驱动器**：你需要一个最小空间为 4GB 的笔式驱动器，但建议使用 8GB 的笔式驱动器来完成这个可启动过程。
- **使 USB 可启动的工具**: 由于我们使用的是基于 Linux 的操作系统来制作 USB 可启动的 Debian 11，因此我们在本指南中使用了 **balenaEtcher** 工具来制作 USB 可启动；你可以通过以下链接下载并安装 Linux 的 "**balenaEtcher**"。
 - [下载 balenaEtcher](https://link.juejin.cn/?target=https%3A%2F%2Fwww.balena.io%2Fetcher%2F "https://www.balena.io/etcher/") 你有多种支持的操作系统选择；因为我们使用 Linux 来使 Debian 11 操作系统可启动，所以我们选择了 balenaEtcher 的 "**Linux x64**" 版本。

### 如何在 Linux 操作系统上制作 Debian 11 的可启动 USB
#### 第一步：附加 ISO 镜像

首先，启动 balenaEtcher 工具：你可以看到一个活动选项和两个非活动选项。要激活其他选项，必须先执行活动选项：因此，点击 " **从文件中闪现** "，从你的电脑中寻找 Debian 11 的 ISO 镜像。

** 注意：** 你可以通过导航到 " **从 URL 闪存** "直接附加文件，也可以通过" **克隆驱动器** " 来获得 ISO 文件。然而，我们建议先下载 ISO 镜像，然后再使用 balenaEtcher。

![](https://img-blog.csdnimg.cn/img_convert/a0da487b82f53daac1f28f84e52277d4.jpeg)

从你保存的位置选择镜像，然后点击 "打开"。

![](https://img-blog.csdnimg.cn/img_convert/3dfbaafafb1a553c458d155b69cd8ec8.jpeg)

#### 第二步：选择 USB

1. 将 USB 插入你的系统，点击 "**Select Target**" 选择 USB。
2. 当你点击 "**Select target**" 时，你会看到插入的 USB 驱动器的列表。
3. 勾选 USB 选项并点击 " **选择** " 继续。
#### 第三步：开始制作 USB 可启动的过程

在成功完成前两个步骤后，你会发现 ISO 镜像选项和 USB 选项都已经完成。

![](https://img-blog.csdnimg.cn/img_convert/8d3604b1a43b18ea0d7c0c077534f8d6.webp?x-oss-process=image/format,png)

现在，点击 "**Flash**" 以获得 ISO 图像映射到你的 USB 上，使其可启动。

当你点击 "**Flash**"的时候，你会得到一个认证提示：输入你的密码并点击"**Authenticate**" 来恢复闪电。

![](https://img-blog.csdnimg.cn/img_convert/fcf89681bb33c050970850ff40ca09bc.webp?x-oss-process=image/format,png)

这将需要几分钟时间来完成闪存过程。

![](https://img-blog.csdnimg.cn/img_convert/05d170ff5fe9d6e30b99c82974c6192b.webp?x-oss-process=image/format,png)

一旦这个过程完成，balenaEtcher 将显示 "**Flash Complete**"，如下图所示。

![](https://img-blog.csdnimg.cn/img_convert/3e039654d7e9a37a3010479284f72968.webp?x-oss-process=image/format,png)

### 如何在 Windows 上制作一个 Debian 11 可启动的 USB 盘

您必须下载用于在 Windows 上制作可启动 USB 的工具；我们在本节中使用 Rufus 工具。

**[下载 Rufus](https://link.juejin.cn/?target=https%3A%2F%2Frufus.ie%2Fen%2F "https://rufus.ie/en/")**

**注**：你也可以使用 balenaEtcher 来执行上述任务。

#### 第一步：打开并配置 Rufus

首先，将 USB 连接到您的窗口，然后打开 Rufus；它会自动获取 USB 的详细信息，如下图所示；点击 "**SELECT**"，从您的窗口计算机中选择 Debian 11 镜像。

![](https://img-blog.csdnimg.cn/img_convert/852becebfe16b2948f08e1541adb4c72.webp?x-oss-process=image/format,png)

选择 Debian 11 ISO 镜像，一旦选择，你可以看到 ISO 文件已经被添加。

![](https://img-blog.csdnimg.cn/img_convert/ef06f8a6188fecd81e053b0ba0dff262.webp?x-oss-process=image/format,png)

#### 第二步：启动程序

Rufus 允许您根据自己的要求配置设置；但默认设置是好的；所以，点击窗口末尾的 "开始"，开始制作 USB 可启动。

![](https://img-blog.csdnimg.cn/img_convert/5dbdac84b8f3b2807338291295f09da7.webp?x-oss-process=image/format,png)

这个过程需要几分钟才能完成；一旦完成，你会注意到一个 "**READY**" 状态。

![](https://img-blog.csdnimg.cn/img_convert/831979dffd6d2a11d187fee291f2488d.webp?x-oss-process=image/format,png)
## 启动并配置安装 Debian

1. 首先要关机，开机时进入BIOS界面，我的笔记本是天选四，开机时按住F2即可进入。
2. 调整启动优先级，把USB启动提到第一位，然后退出BIOS。
3. 之后就参考文章 3 & 4 即可。

## 所遇问题

- 安装时、安装完成后笔记本自带的键盘都无法使用
	- 解决方案：其实还没有从源头上解决，替代方案就是直接用USB外接了一个机械键盘使用。
- 安装完成启动后黑屏
	- 解决方案：见参考文章 5
## 参考文章

1. [# 如何制作一个 Debian 11 的可启动 USB](https://juejin.cn/post/7124175803922792455)
2. [# Debian GNU/Linux 安装手册](https://www.debian.org/releases/stable/i386/index.zh-cn.html)
	- 主要看了3.6. 安装前的硬件和操作系统的相关设置
3. [# 鸽子的折腾日记①丨手把手教你安装Debian](https://www.jianshu.com/p/898ef5ad5bbe)
	- 手把手教安装，尊嘟很详细
4. [# InstallingGNU/Linux](https://nju-projectn.github.io/ics-pa-gitbook/ics2020/0.1.html)
5. [# Debian 11 新装系统开机黑屏](https://xja.github.io/black-screen-on-debian-11-new-installation/)