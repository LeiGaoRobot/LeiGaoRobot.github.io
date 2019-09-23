---
title: Linux Command-Line
date: 2019-05-30 10:29:23
categories:
- [Linux]
- [Command Line]
tags:
- linux
- command-line
- command
---

[explainshell](https://explainshell.com/#)

# Daily use

+ **man [any command]**: 查看任意命令的帮助文档
+ Tab: 补全
+ **ctrl-r**: 搜索命令历史记录（按下后，键入要搜索的值，反复按ctrl-r循环切换更多匹配，按Enter键执行找到的命令，或者点击右箭头将结果放在当前行中以允许编辑）
+ **ctrl-w**: 删除最后一个单词
+ **ctrl-u**: 将当前光标中的内容删除回行的开头
+ **alt-b/alt-f**: 按单词向左/右移动
+ **ctrl-a/ctrl-e**: 将光标移动到行首/行尾
+ **ctrl -k**: 清除到行尾
+ **ctrl -l**: 清除屏幕
+ **history**: 查看最近的命令。跟随!n（n命令编号在哪里）再次执行。!$最后一个参数和!!最后一个命令（请参见手册页中的“HISTORY EXPANSION”）。但是，这些通常很容易被ctrl-r和alt-.取代。
+ **cd -**: 要返回上一个工作目录
+ **xargs**: 将参数列表转换成小块分段传递给其他命令，以避免参数列表过长的问题，可以正确处理输入中有空格等特殊字符的情况。对于经常产生大量输出的命令如find、locate和grep来说非常有用。
+ pstree -p: 显示进程树
+ pgrep & pkill: find or signal processes by name
+ man 7 signal: signal detail info
+ **nohup/disown**: want a background process to keep running forever
+ netstat -ln[tp(TCP)/u(UDP)] / ss -pla[t(TCP)/u(UDP)] / lsof -iTCP -sTCP:LISTEN -P -n: 检查监听进程
+ lsof / fuser: open sockets and files
+ uptime: 系统到现在运行了多长时间
+ **alias**: 别名
> save alias see more [arrange for login shells to source it.](https://superuser.com/questions/183870/difference-between-bashrc-and-bash-profile/183980#183980)  
> 传统上，当登录Unix系统时，系统会为启动一个程序。该程序是一个shell，即一个旨在启动其他程序的程序。它是一个命令行shell：通过键入其名称来启动另一个程序。默认shell（Bourne shell）从~/.profile作为登录shell调用时读取命令。
> Bash是一个类似Bourne的shell。它从~/.bash_profile作为登录shell调用时读取命令，如果该文件不存在，则会尝试读取~/.profile。  
> 您可以随时直接调用shell，例如在GUI环境中启动终端仿真器。如果shell不是登录shell，则不会读取~/.profile。当您将bash作为交互式shell启动时（即，不运行脚本），它会读取~/.bashrc（除非作为登录shell调用时，它只读取~/.bash_profile或~/.profile。  
> 因此：  
> + ~/.profile 是放置适用于整个会话的内容的地方，例如您希望在登录时启动的程序（但不是图形程序，它们会进入不同的文件）和环境变量定义。
> + ~/.bashrc 是放置仅适用于bash本身的东西的地方，例如别名和函数定义，shell选项和提示设置。（你也可以在那里放置键绑定，但对于bash，他们通常会进入~/.inputrc。）
> + ~/.bash_profile 可以代替使用~/.profile，但它只能由bash读取，而不能由任何其他shell读取。（如果您希望初始化文件在多台计算机上运行并且您的登录shell不是所有计算机上的bash，那么这主要是一个问题。）~/.bashrc如果shell是交互式的，这是一个合乎逻辑的位置。我推荐以下内容~/.bash_profile：z  
>  ```
> if [ -r ~/.profile ]; then . ~/.profile; fi
> case "$-" in *i*) if [ -r ~/.bashrc ]; then . ~/.bashrc; fi;; esac
> ```
> 在现代unices上，有一个与~/.profile相关的附加复杂性。如果您在图形环境中登录(也就是说，如果您键入密码的程序以图形模式运行)，则不会自动获得一个读取~/.profile的登录shell。根据图形登录程序、随后运行的窗口管理器或桌面环境以及发行版如何配置这些程序，您的~/.的配置文件可以读取，也可以不读取。如果不是，通常还可以在另一个地方定义环境变量和程序，以便在登录时启动，但遗憾的是没有标准位置。  
> 注意，您可能会在这里和那里看到一些建议，将环境变量定义放在~/中。bashrc或总是在终端中启动登录shell。两者都是坏主意。这两种方法中最常见的问题是，环境变量只能在通过终端启动的程序中设置，而不能在直接使用图标、菜单或键盘快捷方式启动的程序中设置。
> 为了完整起见，请按请求:如果.bash_profile不存在，bash还会在返回.profile之前尝试.bash_login。请忘记它的存在。
