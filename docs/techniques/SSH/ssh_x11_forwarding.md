# 使用服务器上的GUI应用：X11 Forwarding

> 这篇文章假设你有GNU/Linux和SSH的基础知识，因此不会详细地介绍每个细节。

考虑这样的场景：

- 在虚拟机上进行开发，操作GUI时，需要借助虚拟机自带的显示器；
- 有时不需要完整的桌面环境，打开一个窗口足矣；

这时候X11 Forwarding就十分有用了，它允许你在你的桌面环境中直接和虚拟机的GUI交互。

由于[X](https://en.wikipedia.org/wiki/X_Window_System)是基于网络的窗口系统，你也可以和远在天边的VPS进行GUI交互（当然会有延迟）。

## 安装X Server

> 我个人建议使用[VcXsrv](https://sourceforge.net/projects/vcxsrv/)。
> 
> 你也可以通过执行`winget install marha.VcXsrv`来安装。

在开始菜单中运行`XLaunch`，一路下一步即可。你可以点击`托盘图标/Applications/xcalc`来启动自带的计算器应用，并验证显示和点击等操作。

## 配置SSH Client

### PuTTY

### OpenSSH for Windows

### Visual Studio Code - Remote SSH