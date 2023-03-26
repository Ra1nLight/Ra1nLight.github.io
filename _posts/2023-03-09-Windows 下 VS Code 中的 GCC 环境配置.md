---
title: Windows 下 VS Code 中的 GCC 环境配置
date: 2023-03-09 17:50:00 +0800
categories: [经验分享]
tags: [VS Code, C/C++, GCC, Windows, 环境配置]
math: true
---

对于刚接触 VS Code 的初学者来说，配置 C/C++ 开发环境是个很麻烦的问题，即使网上有一大堆教程也一头雾水。其实配环境并不难~~会者不难~~，哥们凭借自己配环境和指导别人配环境的经验记录一下 Windows 下 C/C++ 开发环境的配置过程。学会之后甚至还能举一反三，对配置其他语言的开发环境很有帮助。

## 安装 VS Code

直接去[官网](https://code.visualstudio.com/Download)下载安装就行。装好之后在扩展商店下载汉化包和 C/C++ 扩展包。另外，VS Code 牛就牛在它有很多各种功能的扩展，包括美化包、额外功能增强包等等，用好了可以极大提高生产力。关于扩展包的推荐可以看看其他文章或者自己探索。

![IT52G7MT3AXORPGAYQ.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/111012/10/34158/44379/64097c20F85990067/a54ead8a0315046b.png)

## 安装 mingw-w64 工具链

### MSYS2 安装

推荐使用 [MSYS2](https://mirrors.tuna.tsinghua.edu.cn/msys2/distrib/x86_64/msys2-x86_64-20230127.exe)（资源来自 [THU 镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/msys2/)） 来安装 mingw-w64 工具链。从 MSYS2 安装的所有工具链都在 MSYS2 的安装目录下。*也可以直接把别人的 `mingw-w64`{: .filepath} 文件夹复制过来直接用。*

![7HEXPFX91QH1T1.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/211753/16/26307/4751/640985deFf15cb365/393419bedf948ca1.png)

### 获取 mingw-w64

MSYS2 安装完成之后将启动 MSYS2 终端。在终端中输入以下命令安装 mingw-w64：

```console
$ pacman -S --needed base-devel mingw-w64-x86_64-toolchain
```

直接按回车接受默认值，一步步确认后等待安装完成。

![0YTSTS6M98CLZZT1C.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/181572/24/33451/44424/640989d0F9bf38ac1/f54e900b16c923db.png)

## 添加环境变量

把安装好的 mingw-w64 的路径添加到 Windows 的环境变量中。

1. 找到 `mingw-w64`{: .filepath} 文件夹（在**你的** MSYS2 的安装目录下），进入 `mingw64\bin`{: .filepath} 文件夹，复制路径。例如：`C:\msys64\mingw64\bin`{: .filepath}。
2. 打开“控制面板”$\rightarrow$“系统和安全”$\rightarrow$“系统”$\rightarrow$“高级系统设置”$\rightarrow$“高级”$\rightarrow$“环境变量”（或者直接在搜索栏搜索并打开“编辑系统环境变量”$\rightarrow$“环境变量”）。

    ![AZ44B7H6_4BJY.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/104394/32/38048/33596/64098d9bFfb795b9a/5ee9d20a9a82cf8d.png)

3. 在用户变量框中选中 Path$\rightarrow$“编辑”$\rightarrow$“新建”$\rightarrow$“粘贴刚才复制的路径”$\rightarrow$“确定”$\rightarrow$“确定”。**对系统变量中的 Path 做同样的操作也可以实现，且将会对计算机上的所有用户生效。**

    ![1YE4DSRADICKtAJJV.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/64522/35/24222/20185/64098d9cF96eab9c6/8dbebd9e7215bbda.png)

4. 打开一个**新的**终端，验证 mingw-w64 安装：

   ```console
   $ gcc --version
   $ g++ --version
   $ gdb --version
   ```

   如果安装成功则会显示类似下图中的内容。如果没有，那么考虑可能是 mingw-w64 没有正确安装或者环境变量路径没有正确填写，需要验证之前的步骤是否出错。

   ![2SFOBW6_I2B4LECH.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/178777/6/33303/12805/64098fdbF029a3d60/1f50261cf59a930c.png)

## 为 VS Code 添加配置

### 启动配置

在你想要的位置创建一个文件夹，然后用 VS Code 打开，在弹出的工作区信任对话框中选择**信任作者**~~因为你就是作者~~，并根据需要选择是否信任所有子文件夹。**新创建的这个文件夹将会存放调试配置文件。**

![I3U5JR954TYNKQXI7V.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/155674/14/35571/10097/6409925bF914a9704/fb64d6a991132a4e.png)

接下来，在打开的文件夹下写一个任意的 c 源代码文件。编写完成之后在左边选择“运行和调试”$\rightarrow$“C++(GDB/LLDB)”$\rightarrow$“C/C++: gcc.exe 生成和调试活动文件”。

![BJ83NY8YTFPRCF3WH.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/136725/11/33985/47011/6409956eF080b6bf3/a241d419b2d71bff.png)

![JED0WAQIBJ3OFCOH.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/78477/6/18865/5325/640994eaF1e16356b/75312a9931d216f7.png)

然后，VS Code 会自动在文件夹下创建一个 `.vscode`{: .filepath} 子文件夹并往其中添加 gcc 启动配置 `tasks.json`{: .filepath}，接着尝试运行。如果成功，VS Code 下方的终端会显示程序的运行过程和输出，同时也可以在其中进行输入交互。

![F_8A1DP43AASHUJP47.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/14836/26/16753/5479/6409988dF2c856286/04e1760befb4bc3f.png)

> 在一般情况下，gcc 无法识别中文路径，如果弹框报错 ```no such file or directory```，请确认源代码全路径不包含中文。
{: .prompt-warning }

### 调试配置

自定义一个调试配置文件让调试更轻松。创建 ```launch.json```{: .filepath}，同样选择“C++(GDB/LLDB)”，按照下图进行操作自动添加配置。

![4GX7GJRCR5XC82WZEG0.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/129803/12/35260/15250/64099bd0Fd5a1ff78/b87a071887acaec8.png)

![YRX7SKTQLIVBFEHKM.png](https://kjimg10.360buyimg.com/ott/jfs/t20250308/45404/21/23664/44440/64099e05F4ddc419d/24e1c36b45c56280.png)

将自动生成的配置中的以下几个字段修改一下：

```json
{
"program": "${fileDirname}\\${fileBasenameNoExtension}.exe",    // 自动识别将要调试的文件的位置
"externalConsole": true,    // 启动一个新的终端窗口，非必须
"miDebuggerPath": ""        // 指定 gdb 路径，这里没填就是让它自己从环境变量中寻找
}
```

修改完成后就可以很方便地在 VS Code 中给源代码下断点调试了。我们可以根据需要研究一下各个配置选项的含义，选择最适合自己的配置进行调试。其他编程语言的调试配置同样也可以在这个文件中添加并编辑。

## 总结

到此为止，对 VS Code 中的 C/C++ 环境配置已经基本完成了。VS Code 左边打开的所有文件夹属于一个工作区，工作区中的所有文件都遵循工作区中存在的 `.vscode`{: .filepath} 文件夹之下的配置文件。此时你可以把其他代码文件或文件夹添加到工作区以进行你的工作。如果文章有错漏或者有不解的地方请联系我。

**Happy coding! ♪(´▽｀)**
