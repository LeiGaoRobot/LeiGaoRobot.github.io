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

# Everything is file

# Daily use

+ **cat**: 连接文件, 读取一个或多个文件，然后复制它们到标准输出.
+ **sort**: 排序文本行
+ **uniq**: 报道或省略重复行,uniq 命令经常和 sort 命令结合在一起使用。uniq 从标准输入或单个文件名参数接受数据有序 列表（详情查看 man uniq）
```
ls /bin /usr/bin | sort | uniq | less
ls /bin /usr/bin | sort | uniq -d | less ("-d",显示重复的数据列表)
```
+ **grep**: 打印匹配行
```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | grep zip
bunzip2
bzip2
gunzip
...
```
+ **wc**: wc（字计数）命令是用来显示文件所包含的行数、字数和字节数.
```
[me@linuxbox ~]$ wc ls-output.txt
7902 64566 503634 ls-output.txt
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | wc -l ("-l",限制命令输出只能报道行数)
2728
```
+ **head**: 输出文件第一部分(打印文件开头部分)
+ **tail**: 输出文件最后一部分(打印文件结尾部分)
```
[me@linuxbox ~]$ head -n 5 ls-output.txt  ("-n",打印的行数)
total 343496
...
[me@linuxbox ~]$ tail -n 5 ls-output.txt
...
[me@linuxbox ~]$ tail -f /var/log/messages ("-f", )
Feb 8 13:40:05 twin4 dhclient: DHCPACK from 192.168.1.1
....
```
+ **tee**: 从标准输入读取数据，并同时写到标准输出和文件
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

# I/O redirection

Many of the programs that we have used so far produce output of some kind. This output often consists of two types. First, we have the program’s results; that is, the data the program is designed to produce, and second, we have status and error messages that tell us how the program is getting along. If we look at a command like ls, we can see that it displays its results and its error messages on the screen.

到目前为止，我们用到的许多程序都会产生某种输出。这种输出，经常由两种类型组成。 第一，程序运行结果；这是说，程序要完成的功能。第二，我们得到状态和错误信息， 这些告诉我们程序进展。如果我们观察一个命令，例如 ls，会看到它的运行结果和错误信息 显示在屏幕上。

Keeping with the Unix theme of “everything is a file,” programs such as ls actually send their results to a special file called standard output (often expressed as stdout) and their status messages to another file called standard error (stderr). By default, both standard output and standard error are linked to the screen and not saved into a disk file. In addition, many programs take input from a facility called standard input (stdin) which is, by default, attached to the keyboard.

与 Unix 主题“任何东西都是一个文件”保持一致，像 ls这样的程序实际上把他们的运行结果 输送到一个叫做标准输出的特殊文件（经常用 stdout 表示），而它们的状态信息则送到另一个 叫做标准错误的文件（stderr）。默认情况下，标准输出和标准错误都连接到屏幕，而不是 保存到磁盘文件。除此之外，许多程序从一个叫做标准输入（stdin）的设备得到输入，默认情况下， 标准输入连接到键盘。

## Standard output

I/O redirection allows us to redefine where standard output goes. To redirect standard output to another file besides the screen, we use the “>” redirection operator followed by the name of the file. Why would we want to do this? It’s often useful to store the output of a command in a file. For example, we could tell the shell to send the output of the ls command to the file ls-output.txt instead of the screen:

I/O 重定向允许我们来重定义标准输出的地点。我们使用 “>” 重定向符后接文件名将标准输出重定向到除屏幕 以外的另一个文件。为什么我们要这样做呢？因为有时候把一个命令的运行结果存储到 一个文件很有用处。例如，我们可以告诉 shell 把 ls 命令的运行结果输送到文件 ls-output.txt 中去， 由文件代替屏幕。

```
[me@linuxbox ~]$ ls -l /usr/bin > ls-output.txt
```

when we redirect output with the “>” redirection operator, the destination file is always rewritten from the beginning. Since our ls command generated no results and only an error message, the redirection operation started to rewrite the file and then stopped because of the error, resulting in its truncation. In fact, if we ever need to actually truncate a file (or create a new, empty file) we can use a trick like this:

当我们使用 “>” 重定向符来重定向输出结果时，目标文件总是从开头被重写。 因为我们 ls 命令没有产生运行结果，只有错误信息，重定向操作开始重写文件，然后 由于错误而停止，导致文件内容清空。事实上，如果我们需要清空一个文件内容（或者创建一个 新的空文件），可以使用这样的技巧：

```
[me@linuxbox ~]$ > ls-output.txt
```

Simply using the redirection operator with no command preceding it will truncate an existing file or create a new, empty file.

简单地使用重定向符，没有命令在它之前，这会清空一个已存在文件的内容或是 创建一个新的空文件。

So, how can we append redirected output to a file instead of overwriting the file from the beginning? For that, we use the “>>” redirection operator, like so:

所以，怎样才能把重定向结果追加到文件内容后面，而不是从开头重写文件？为了这个目的， 我们使用”>>“重定向符，像这样：

```
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
```

Using the “>>” operator will result in the output being appended to the file. If the file does not already exist, it is created just as though the “>” operator had been used. Let’s put it to the test:

使用”>>“操作符，将导致输出结果添加到文件内容之后。如果文件不存在，文件会 被创建，就如使用了”>”操作符。把它放到测试中：

```
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
[me@linuxbox ~]$ ls -l /usr/bin >> ls-output.txt
[me@linuxbox ~]$ ls -l ls-output.txt
-rw-rw-r-- 1 me   me    503634 2008-02-01 15:45 ls-output.txt
```

We repeated the command three times resulting in an output file three 
我们重复执行命令三次，导致输出文件大小是原来的三倍

## Standard error

Redirecting standard error lacks the ease of a dedicated redirection operator. To redirect standard error we must refer to its file descriptor. A program can produce output on any of several numbered file streams. While we have referred to the first three of these file streams as standard input, output and error, the shell references them internally as file descriptors zero, one and two, respectively. The shell provides a notation for redirecting files using the file descriptor number. Since standard error is the same as file descriptor number two, we can redirect standard error with this notation:

标准错误重定向没有专用的重定向操作符。为了重定向标准错误，我们必须参考其文件描述符。 一个程序可以在几个编号的文件流中的任一个上产生输出。虽然我们已经将这些文件流的前 三个称作标准输入、输出和错误，shell 内部分别将其称为文件描述符0、1和2。shell 使用文件描述符提供 了一种表示法来重定向文件。因为标准错误和文件描述符2一样，我们用这种 表示法来重定向标准错误：

```
[me@linuxbox ~]$ ls -l /bin/usr 2> ls-error.txt
```

The file descriptor “2” is placed immediately before the redirection operator to perform the redirection of standard error to the file ls-error.txt.

文件描述符”2”，紧挨着放在重定向操作符之前，来执行重定向标准错误到文件 ls-error.txt 任务。

## Redirect both standard output and standard error

There are cases in which we may wish to capture all of the output of a command to a single file. To do this, we must redirect both standard output and standard error at the same time. There are two ways to do this. First, the traditional way, which works with old versions of the shell:

有时我们希望将一个命令的所有输出保存到一个文件。为此，我们 必须同时重定向标准输出和标准错误。有两种方法来完成任务。第一个是传统的方法， 在旧版本 shell 中也有效：

```
[me@linuxbox ~]$ ls -l /bin/usr > ls-output.txt 2>&1
```

Using this method, we perform two redirections. First we redirect standard output to the file ls-output.txt and then we redirect file descriptor two (standard error) to file descriptor one (standard output) using the notation 2>&1.

使用这种方法，我们完成两个重定向。首先重定向标准输出到文件 ls-output.txt，然后 重定向文件描述符2（标准错误）到文件描述符1（标准输出）使用表示法2>&1。

Notice that the order of the redirections is significant. The redirection of standard error must always occur after redirecting standard output or it doesn’t work. In the example above,

注意重定向的顺序安排非常重要。标准错误的重定向必须总是出现在标准输出 重定向之后，要不然它不起作用。上面的例子，

```
>ls-output.txt 2>&1
```

standard error is directed to the screen.

则标准错误定向到屏幕。

Recent versions of bash provide a second, more streamlined method for performing this combined redirection:

现在的 bash 版本提供了第二种方法，更精简合理的方法来执行这种联合的重定向。

```
[me@linuxbox ~]$ ls -l /bin/usr &> ls-output.txt
```

In this example, we use the single notation &> to redirect both standard output and standard error to the file ls-output.txt.

在这个例子里面，我们使用单单一个表示法 &> 来重定向标准输出和错误到文件 ls-output.txt。

## Bit bucket

Sometimes “silence is golden,” and we don’t want output from a command, we just want to throw it away. This applies particularly to error and status messages. The system provides a way to do this by redirecting output to a special file called “/dev/null”. This file is a system device called a bit bucket which accepts input and does nothing with it. To suppress error messages from a command, we do this:

有时候“沉默是金”，我们不想要一个命令的输出结果，只想把它们扔掉。这种情况 尤其适用于错误和状态信息。系统通过重定向输出结果到一个叫做”/dev/null”的特殊文件， 为我们提供了解决问题的方法。这个文件是系统设备，叫做位存储桶，它可以 接受输入，并且对输入不做任何处理。为了隐瞒命令错误信息，我们这样做：

```
[me@linuxbox ~]$ ls -l /bin/usr 2> /dev/null
```

> /dev/null in Unix Culture
> Unix 文化中的/dev/null
> The bit bucket is an ancient Unix concept and due to its universality, has appeared in many parts of Unix culture. When someone says he/she is sending your comments to /dev/null, now you know what it means. For more examples, see the Wikipedia article on “/dev/null”.
> 位存储桶是个古老的 Unix 概念，由于它的普遍性，它的身影出现在 Unix 文化的 许多部分。当有人说他/她正在发送你的评论到/dev/null，现在你应该知道那是 什么意思了。更多的例子，可以阅读 Wikipedia 关于”/dev/null”的文章。

# pipelines

The ability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator “|” (vertical bar), the standard output of one command can be piped into the standard input of another:

命令从标准输入读取数据并输送到标准输出的能力被一个称为管道线的 shell 特性所利用。 使用管道操作符”|”（竖杠），一个命令的标准输出可以通过管道送至另一个命令的标准输入：

```
command1 | command2
```

To fully demonstrate this, we are going to need some commands. Remember how we said there was one we already knew that accepts standard input? It’s less. We can use less to display, page-by-page, the output of any command that sends its results to standard output:

为了全面地说明这个命令，我们需要一些命令。是否记得我们说过，我们已经知道有一个 命令接受标准输入？它是 less 命令。我们用 less 来一页一页地显示任何命令的输出，命令把 它的运行结果输送到标准输出：

```
[me@linuxbox ~]$ ls -l /usr/bin | less
```

Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow and then output it. The first one we will try is sort. Imagine we wanted to make a combined list of all of the executable programs in /bin and /usr/bin, put them in sorted order and view it:

管道线经常用来对数据完成复杂的操作。有可能会把几个命令放在一起组成一个管道线。 通常，以这种方式使用的命令被称为过滤器。过滤器接受输入，以某种方式改变它，然后 输出它。第一个我们想试验的过滤器是 sort。想象一下，我们想把目录/bin 和/usr/bin 中 的可执行程序都联合在一起，再把它们排序，然后浏览执行结果：

```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | less
```

Since we specified two directories (/bin and /usr/bin), the output of ls would have consisted of two sorted lists, one for each directory. By including sort in our pipeline, we changed the data to produce a single, sorted list.

因为我们指定了两个目录（/bin 和/usr/bin），ls 命令的输出结果由有序列表组成， 各自针对一个目录。通过在管道线中包含 sort，我们改变输出数据，从而产生一个 有序列表。


# grep

grep is a powerful program used to find text patterns within files. It’s used like this:

grep 是个很强大的程序，用来找到文件中的匹配文本。这样使用 grep 命令：

```
grep pattern [file...]
```

There are a couple of handy options for grep: “-i” which causes grep to ignore case when performing the search (normally searches are case sensitive) and “-v” which tells grep to only print lines that do not match the pattern.

grep 有一些方便的选项：”-i”使得 grep 在执行搜索时忽略大小写（通常，搜索是大小写 敏感的），”-v”选项会告诉 grep 只打印不匹配的行。