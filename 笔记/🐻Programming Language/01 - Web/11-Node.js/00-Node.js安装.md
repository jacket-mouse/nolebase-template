---
title: 00-Node.js安装
---
## nvm

- **下载和安装NVM**： 从[NVM的GitHub仓库](https://github.com/coreybutler/nvm-windows/releases)下载适用于Windows的NVM安装程序，并按照说明进行安装。
- **验证NVM安装**： 打开命令提示符或PowerShell，输入以下命令来验证NVM是否安装正确：
	`nvm --version`
    如果显示版本号，说明NVM已经正确安装。
- **检查`PATH`环境变量**：
	- 在“系统变量”下找到并选择`Path`，点击“编辑”。
	- 确保NVM的安装路径和Node.js的路径都在`Path`变量中。例如：
```C++
    C:\Users\<YourUsername>\AppData\Roaming\nvm 
    C:\Users\<YourUsername>\AppData\Roaming\nvm\v<node-version>
```
- **设置NVM_HOME和NVM_SYMLINK**（如果没有）：
	- 在“系统变量”中，点击“新建”。
	    - 变量名：`NVM_HOME`
	    - 变量值：`C:\Users\<YourUsername>\AppData\Roaming\nvm`
	- 点击“新建”。
	    - 变量名：`NVM_SYMLINK`
	    - 变量值：`C:\Program Files\nodejs`（或你想安装Node.js的路径）
	- 使用命令检验：
```shell
	echo %NVM_HOME%
	echo %NVM_SYMLINK%
```
 如果移动了nvm下载的位置，那么除了上述内容需要修改外，还要改nvm文件夹里的`setting.txt`文件内容。

### 示例：环境变量设置

假设你的用户名是`User`，NVM和Node.js的路径设置如下：

1. `NVM_HOME`：`C:\Users\User\AppData\Roaming\nvm`
2. `NVM_SYMLINK`：`C:\Program Files\nodejs`

`PATH`环境变量应包含：
```c++
C:\Users\User\AppData\Roaming\nvm 
C:\Users\User\AppData\Roaming\nvm\v<node-version> 
C:\Program Files\nodejs`
```
## 安装和使用Node.js

使用NVM安装和切换Node.js版本。

1. **安装Node.js**：`nvm install <version>`例如，安装最新的LTS版本：`nvm install --lts`
2. **切换Node.js版本**：`nvm use <version>`例如，切换到最新安装的LTS版本：    `nvm use --lts`
3. **验证Node.js版本**：`node --version`
