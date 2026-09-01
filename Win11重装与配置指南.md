# Windows 11 重装与配置指南

## 一、重装前

### 1. 备份数据

重要数据同时备份到云盘和移动硬盘。主要包括：

- 文档、桌面、下载、图片和视频；
- Obsidian 仓库、Typora 文档及附件；
- 浏览器书签、密码和扩展（如果登录了Edge或者Chrome账号，并且开启了同步，可以在重装之前手动点击一下同步。注意同步的选项是否勾选了书签、密码、拓展等）；
- 聊天记录（QQ和微信都支持把聊天记录全部导出到手机，等重装完系统之后可以再导回到电脑）；
- 重要软件配置（例如CC Switch中的key、Clash订阅链接/配置文件）；

备份完成后抽查文件是否能够正常打开。

### 2. 记录软件清单

查看“设置 → 应用 → 已安装的应用”，把重装后仍然需要的软件记录到 `软件列表.txt`。

### 3. 保存 WSL 关键文件

WSL 和开发环境可以重新安装，不必备份整个发行版。只保留重要内容：

- 未推送到 GitHub 的项目和提交；
- 未跟踪文件以及被 `.gitignore` 忽略的重要文件（例如一些数据库文件）；
- `.env`、本地数据库和其他无法重新生成的数据；
- `~/.ssh`、`~/.gitconfig` 等配置。

SSH 私钥和项目凭据不要放到公开仓库中。

### 4. 准备 FlClash

重装后可能暂时不方便访问 GitHub，因此提前做好以下准备：

- 从 [FlClash GitHub Releases](https://github.com/chen08209/FlClash/releases) 下载 Windows 安装包并放到移动硬盘；
- 备份订阅链接、配置文件和自定义规则；
- 重装后先安装 FlClash、恢复配置并确认网络正常。

订阅链接属于访问凭据，不要写进公开文档或公开仓库。

## 二、安装 Windows 11

1. 从[微软官网](https://www.microsoft.com/software-download/windows11)下载 Windows 11 ISO。（现在推荐https://www.bilibili.com/video/BV14y4U6DEjc 26H2预览版镜像，相对稳定，功能和性能都比之前好）
2. 从 [Ventoy 官网](https://www.ventoy.net/en/download.html)下载 Ventoy，并安装到移动硬盘或 U 盘。
3. 把 Windows 11 ISO 放进 Ventoy 数据分区。
4. 重启电脑，从启动菜单选择 Ventoy 所在设备。
5. 在 Ventoy 中选择 Windows 11 镜像。
6. 选择 Windows 11 专业版并进行自定义安装。
7. 核对磁盘后，只删除原系统所在分区，不操作备份盘或数据盘。

安装 Ventoy 会修改目标磁盘，操作前注意不要选错盘。安装介质和重要数据的唯一备份不要放在同一块盘上。

### 跳过联网和微软账号
在装Windows 11时，默认会要求登录Windows账号，但是可能由于微软的网络问题/网卡驱动还没有安装而无法登录，可以选择跳过。
参考视频：[Windows 11 安装时跳过联网登录微软账号](https://www.bilibili.com/video/BV1YGj665EK7)

按 `Shift + F10` （或者`Shift + Fn + F10` ）打开命令提示符，然后运行：
start ms-cxh:localonly

该方法可能随 Windows 版本变化而失效。

## 三、重装后的配置顺序

1. 运行 Windows Update，安装更新并重启。可能需要重启多次。
2. Windows 激活 + office 安装/激活：https://github.com/massgravel/microsoft-activation-scripts
3. 安装 FlClash，导入订阅和配置。
4. 安装 WSL 和 Ubuntu，恢复项目、密钥及必要配置。
5. 按软件清单安装常用软件。

## 四、软件安装方式

软件来源按以下顺序选择：

1. 微软商店（微软商店中的软件有一部分运行在沙盒中，卸载之后不容易有残留，而且更安全。还支持自动更新）
2. winget（如果嫌复杂可以跳过这个。可视化界面：https://github.com/Devolutions/UniGetUI
3. 软件官网或官方 GitHub Releases。注意，必应搜索结果可能包含伪造的官网。建议日常搜索引擎用谷歌。
4. 火绒应用商店等可信软件商店。

百度网盘、夸克网盘等比较脏/不希望直接安装到主系统的软件，可以安装 VMware，新建一个 Windows 11 虚拟机并在虚拟机中运行。VMware可以配置共享文件夹，通过这个文件夹来传递文件。

## 五、开发环境

Windows 主要安装桌面软件，编译器、语言环境、包管理器、容器和服务放在 WSL 中。一般选择 Ubuntu，多数软件会专门在Ubuntu上测试，遇到问题的可能性小些。

打开 PowerShell：
```powershell
wsl --install --distribution Ubuntu
```
主要使用 Linux 工具的项目放在 WSL 的 `~/`（用户目录），不要放在 `/mnt/c/...`。因为从WSL中访问Windows文件的性能比较差。

## 六、软件清单

### 效率

- FlClash
- Everything
- NanaZip
- 火绒
- VMware
- Microsoft To Do
- Typora
- Office
- 欧路词典
- SumatraPDF
- OpenLess（语音输入工具） / 豆包语音输入法（目前处于内测阶段，可以找我要Windows安装包）
- OBS Studio
- VLC

### 沟通与远程

- QQ
- 微信
- 腾讯会议
- UU 远程

### 云盘与下载

- 阿里云盘
- 坚果云
- Gopeed（一个下载工具，装了这个软件中的插件，可以通过网页来下载百度网盘、夸克网盘的一些东西，而不依赖于百度网盘、夸克网盘的客户端。它还支持接管日常的下载，下载速度会更快。还支持BT下载。）

### 开发与 AI

- Visual Studio Code
- ChatGPT（建议让其运行在WSL中，路径：设置-常规-集成终端 Shell、智能体环境）

### 系统增强

- Windhawk 及推荐的插件
  - Alt+Tab Window Delayer
  - Remove Taskbar Window Suffixes
  - 任务栏 Dock 动画
  - Turn Off Change File Extension Warning

