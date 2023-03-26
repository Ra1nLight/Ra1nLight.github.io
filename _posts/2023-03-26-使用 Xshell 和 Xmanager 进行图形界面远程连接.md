---
title: 使用 Xshell 和 Xmanager 进行图形界面远程连接
date: 2023-03-26 21:30:17 +0800
categories: [学习记录, 网络安全实验]
tags: [Xshell, Xmanager, Linux, 远程连接]
---

最近我在搓网络安全实验课，学校给的实验操作平台在网页上。但是网页上的操作系统图形界面跟鼠标的交互太抽象了，用起来让人难以忍受。因此我就用 Xshell 和 Xmanager 进行远程连接，这样就可以在本地使用终端和打开图形界面操作了。

## Xshell 的应用

老师已经给了文档教程，照着文档的图做就有本地终端用了。

![6420387ea682492fccf101ed.png](https://pic.imgdb.cn/item/6420387ea682492fccf101ed.png)

![642038aea682492fccf151cb.png](https://pic.imgdb.cn/item/642038aea682492fccf151cb.png)

![642038f7a682492fccf1cf01.png](https://pic.imgdb.cn/item/642038f7a682492fccf1cf01.png)

![6420482fa682492fcc0dd23d.png](https://pic.imgdb.cn/item/6420482fa682492fcc0dd23d.png)

## Xmanager 的应用

### 安装 Xmanger

Xmanager 好像不免费，我这里是用的官网给的 30 天试用版。以后还有需要的话就考虑整个破解版。

没什么需要注意的，直接默认安装，Xmanager 会自动寻找 Xshell 并互相完成基本配置。安装完成之后用 Xshell 连接上主机并在终端输入 `xclock`，如果出现一个时钟的图形界面，就说明可以正常使用了。

![64204712a682492fcc0c04fd.png](https://pic.imgdb.cn/item/64204712a682492fcc0c04fd.png)

### 配置和连接

在打开主机并用 Xshell 连上之后，运行 Xmanager 提供的 Xstart，同样新建一个会话并填上目标主机和端口号和用户名密码，再从下拉框中选择预设命令。我这里的远程主机是 Kali，所以我选了 xterm（Linux）。

![64203ed5a682492fccfe3d38.png](https://pic.imgdb.cn/item/64203ed5a682492fccfe3d38.png)

保存，运行。但我这里会弹窗提示**找不到 Xmanager**，很奇怪。未能解决。

![642042e9a682492fcc053c07.png](https://pic.imgdb.cn/item/642042e9a682492fcc053c07.png)

### 使用

在 Xstart 点运行不成功，但是把预设命令复制到终端里面运行居然可以。在弹出的白色终端里运行程序（比如 `firefox`，`burpsuite`），就可以在你的电脑打开一个图形界面窗口使用了。

![642045f0a682492fcc0a48b9.png](https://pic.imgdb.cn/item/642045f0a682492fcc0a48b9.png)

## 总结

用了之后感觉就像在操作本机应用程序一样，很爽。操作延迟也很不错。~~今晚校园网搞得连接慢的要死，还给我整掉线好几回。~~
