## 前言📣

本Linux笔记的课程源自b站的尚硅谷，主讲人为韩顺平老师。在此感谢韩老师和尚硅谷官方，视频链接在这里[🦋](https://www.bilibili.com/video/BV1dW411M7xL)。

## 注意🎈

`#`表示root用户

`$`表示普通用户

centOS安装文件用的是`yum`命令

`ctrl+c`是强制中断程序的运行，进程已终止

`ctrl+z`将任务中止（暂停）

`ctrl+d`表示EOF

## 目录🗂

<!--GFM-TOC -->

- [LINUX](#LINUX)
    - [Vim](#Vim)
    - [文件系统](#文件系统)
    - [关机](#关机)
    - [用户管理](#用户管理)
    - [运行级别](#运行级别)
    - [帮助指令](#帮助指令)
    - [文件目录类指令](#文件目录类指令)
    - [日期时间类指令](#日期时间类指令)
    - [搜索查找类](#搜索查找类)
    - [压缩和解压命令](#压缩和解压命令)
    - [组管理和权限管理](#组管理和权限管理)
    - [任务调度](#任务调度)
    - [Linux磁盘分区、挂载](#Linux磁盘分区挂载)
    - [磁盘情况查询](#磁盘情况查询)
    - [网络配置](#网络配置)
    - [进程管理](#进程管理)
    - [RPM和YUM](#RPM和YUM)

<!--GFM-TOC -->

# LINUX

## Vim

```
***vim***

yy 拷贝当前行
5yy 拷贝当前行及向下的共5行

p 粘贴到光标后
P[paste] 粘贴到光标前

u[undo] 撤销命令

dd 删除当前行
5dd 删除当前行及向下的共5行

/find 查找单词`find`,按n寻找下一个,N寻找上一个
:noh，可以取消搜索

`:set nu` `:set nonu` 显示/取消行号

G 定位到最末行
gg 定位到最首行
4G 定位到第4行


i 在光标处插入
a 在光标后一格插入
o 在下一行插入新行并进入插入模式
O 在上一行插入新行并进入插入模式
I 在行首进入插入模式
A 在行末进入插入模式

v 开始标记
y 复制标记内容

ctrl+b[backward] 上一页
ctrl+f[forward] 下一页
ctrl+u[up] 上移半屏
ctrl+d[down] 下移半屏
```

## 文件系统

Linux操作系统具有一定层次结构，由若干目录和子目录组成，不同于windows操作系统，Linux只有一个根目录，用“/”表示，它采用的是**级层式的树形结构**。
----*在Linux世界里，一切皆文件。*
![在这里插入图片描述](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232047276.jpg)

### 具体的目录结构

- /lib [library]

> 系统默认库路径文件

- /etc [etcetera]

> 所有程序所需要的配置文件

- /bin[**重点**] (/usr/bin、/usr/local/bin）[binary]

> 是Binary的缩写，这个目录存放着**最经常使用的命令**

- /sbin （/usr/sbin、/usr/local/sbin）[superuser binary]

> s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。

- /home[**重点**]

> 存放普通用户的主目录，在Linux中每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

- /root[**重点**]

> 该目录为系统管理员，也称作超级权限者的用户主目录。

- boot[**重点**」

> 存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件T

- 下列目录和linux内核相关，慎用！

> - /proc [process]
>     这个目录是一个虚拟的目录，它是系统内存的映射，访问这个目录来获取系统信息。
> - /srv [service]
>     service缩写，该目录存放一些服务启动之后需要提取的数据。
> - /sys
>     这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统

- /tmp [temporary]

> 这个目录是用来存放一些临时文件的。

- /dev [device]

> 类似于winlows的设备管理器，把所有的硬件用文件的形式存储。

- /media[**重点**]

> linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。

- /mnt [**重点**] [mount]

> 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将外部的存储挂载在/mnt/上，然后进入该目录就可以查看里的内容了。

- /opt [option]

> 这是给主机额外安装软件所摆放的目录。如安装ORACLE数据库就可放到该目录下。默认为空。

- /usr/local[**重点**]

> 这是别一个给主机额外安装软件所安装的目录。一般是通过编译源码方式安装的程序。

- /var[**重点**] [variable]

> 这个目录中存放着在不断扩充着的东西，习惯将经常被修改的目录放在这个目录下。包括各种日志文件。

- /selinux[security-enhanced linux] (类似于360)

> SELinux是一种安全子系统，它能控制程序只能访问特定文件。

### 小结

1. Linux的目录**有且只有**一个根目录
2. Linux的**各个目录存放的内容是规划好**的，**不能**随便乱放文件。
3. Linux以文件的形式管理我们的设备，因此Linux系统，一切皆文件。
4. Linux的文件系统是一个**树形结构**，每个分叉（子目录）有特定的功能。

## 关机

```
***关机***

shutdown -h[halt] now   立刻关机
shutdown -h[halt] 1     1min后关机
shutdown -r[reboot] now 立即重启

halt 关机
reboot 重启

sync 把内存的数据同步到磁盘[建议在关机或重启前执行sync指令，防止数据丢失]
```

## 用户管理

``` 
***用户***

`su[select|switch user] root` `su - root` 切换成Root管理员账户，加`-`显示上次登陆地点时间

logout 需要在Royal TSX内使用，可以注销账户，关闭连接（我测试也返回上一个账户）
exit[ctrl+d] 退出账户，返回上一个账户

添加用户 useradd xm, 用户创建成功后，会自动在`/home`创建`/home/xm`同名家目录
也可以指定目录（必须为创建）useradd -d[directory] /home/dog xq ,dog就是xq的家目录

# passwd xm 给xm指定密码

删除用户必须用root
# userdel xm 删除用户但保留家目录
# userdel -r[recursion|recursively] xm 删除用户及其家目录
通常删除用户，保留家目录

id root 查询用户的uid,gid,组，不存在，返回无此用户

whoami 查看当前登录的用户

用户组(root用户来操作)
# groupadd test 增加组
# groupdel test 删除组
增加用户时直接加上组 # useradd -g[group] 用户组 用户名
# usermod[modify] -g[group] 用户组 用户名


用户和组的相关文件
/etc/passwd,用户配置文件（用户信息）,利用vim查看，最后几行包含内容为：
`better:x:1000:1000:better:/home/better:/bin/zsh`
用户名:密码:用户id:组id:用户家目录:用户的shell

/etc/group，组配置文件（组信息）,最后几行内容：
`better:x:1000:`
组名:口令:组标志号:组内用户列表(隐藏)

/etc/shadow，口令配置文件（密码和登录信息，是加密的），最后几行显示内容：
`better:$6$Ktuy0JkE$Kf./v2yLnrCjTI.jsRvWHlBEIhSbWVygIBmNljG6BfC5KVeG1oukY7fkNQ4unmW0Db.PKMVT6/hFDDUHjpcKP.:18474:0:99999:7:::`
登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
```

## 运行级别

```
***运行级别***
指令运行级别7个，在`/etc/inittab`里配置系统的运行级别(centos7以上不再使用)
0.关机
1.单用户(找回丢失密码)
2.多用户无网络服务
3.多用户有网络服务
4.保留
5.图形界面 <-----所在级别
6.重启

切换运行级别指令:# init [012356]
这样可以用来找回root密码：
我们先进入单用户模式，然后修改root密码，因为进入单用户模式，root不需要密码就可以进入。

步骤：
1.开机在引导时输入 e
2.看到一个界面输入e，再看到一个界面选中第二行(加载内核)，再输入e
3.在出现一行末输入空格+1，和enter，再按b，表示进入了单用户模式。
4.可以使用`passwd root` 修改root密码

```
## 帮助指令

```
***帮助指令***
当我们对某个指令不熟悉时，可以用命令查看这个指令的使用放方法。

man[manual] [命令或配置文件](功能描述，获得帮助信息)
$ man ls

help 命令 (获得shell内置命令的帮助信息)
$ help cd (zsh这个shell没有help命令，bash有)

```
## 文件目录类指令


文件目录类  
```
pwd[Print Working Directory],显示当前工作目录的绝对路径

ls[list] [选项] [目录或文件]
选项 -a[all],-A[almost all],-l[long]长格式,-h[human-readable]，文件大小带单位。
$ ls /
如果后面跟文件 $ ls -l 1.c 会只显示1.c的内容

cd [change directory],有绝对路径和相对路径
cd ~ 或者 cd,返回家目录
cd .. 返回上一级

mkdir[Make Directory] [选项] 要创建的目录
-p[parents],创建多级目录,指多个文件夹
$ mkdir -p /home/better/桌面/1/2/ ,创建了 1/2/

rmdir[remove directory] 删除的空目录
只能删除空的目录

如何删除非空目录
$ rm -rf[recursion|recursively,forcefully] 目录

touch 创建空文件,可同时创建多个
$ touch hello1.txt hello2.txt

cp拷贝指令[copy]
cp [选项] source destination
选项: -r[recursion|recursively],递归复制整个文件夹
$ cp /1.txt /home ,拷贝在/home/1.txt,文件名未变
$ cp /1.txt /2.txt ,拷贝后的文件为2.txt,拷贝文件的目标的父文件夹必须是存在的文件夹
$ cp -r dir1/ dir2/(dir2不存在) ,将dir1/目录的内容，复制到dir2/内。
$ cp -r dir1/ dir2/(dir2存在) ,将dir1目录的内容，复制到dir2/dir1/内。
	   如果最后一个命令参数为一个已经存在的目录名，cp会将每一个源文件
       复制到那个目录下(维持原文件名).
$ cp ./* /home,也可以拷贝多个文件,home是已经存在的目录，且不会拷贝`./`里的目录，只拷贝文件,加个-r选项,可以拷贝目录。

强制覆盖
$ \cp -r dir1/ dir2/
```

删除指令  
```
# rm -rf /* ，这个指令禁止执行！
rm[remove] [选项] 要删除的文件或目录
选项：-r[recursively]递归删除整个文件夹，-f[forcefully]强制删除不提示
$ \rm 也是强制删除(相当于 -f )

$ rm或cp或mv -i[interactive]，表示可以提示是否删除或覆盖文件，我在zsh配置文件里配置了[-i]选项
```

移动指令  
```
mv 移动文件与目录或重命名
$ mv oldnameFile newnameFile 重命名
$ mv /1.c /home , 表示移动到/home/1.c
$ mv /1.c /home/2.c ，表示移动到/home/2.c 
```

cat指令查看文件内容  
```
cat[concatenate] [选项] 文件
选项：-n[number],显示行号,只能浏览浏览文件，不能修改文件，为了浏览方便,带上管道命令 |more|less
$ cat -n 1.c|more 或者 |less, 可以分页显示
```

more指令  

more指令是一个基于VI编辑器的文本过滤器，它以全屏幕的方式按页显示文本文件的内容、more指令中内置了若干快捷键。  

```
$ more /etc/profile
以下为快捷键
--------------------------------------
空格       向下滚一屏
ctrl+f    向下滚一屏
ENTER     向下翻一行
3+enter   向下翻3行
q         立刻立刻more。不再显示该文件内容
b/ctrl+b  返回上一屏
=         输出当前行号
:f        输出文件名和当前行号
--------------------------------------
更多快捷键：
-------------------------------------------------------------------------------
<space>                 Display next k lines of text [current screen size]
z                       Display next k lines of text [current screen size]*
<return>                Display next k lines of text [1]*
d or ctrl-D             Scroll k lines [current scroll size, initially 11]*
q or Q or <interrupt>   Exit from more
s                       Skip forward k lines of text [1]
f                       Skip forward k screenfuls of text [1]
b or ctrl-B             Skip backwards k screenfuls of text [1]
'                       Go to place where previous search started
=                       Display current line number
/<regular expression>   Search for kth occurrence of regular expression [1]
n                       Search for kth occurrence of last r.e [1]
!<cmd> or :!<cmd>       Execute <cmd> in a subshell
v                       Start up /usr/bin/vi at current line
ctrl-L                  Redraw screen
:n                      Go to kth next file [1]
:p                      Go to kth previous file [1]
:f                      Display current file name and line number
.                       Repeat previous command
-------------------------------------------------------------------------------
```

less指令  
less指令用来分屏查看文件内容，less指令在显示文件内容时，并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于显示较大型文件具有较高效率。  

```
$ less -N(显示行号) -m(显示百分比) /etc/profile
快捷键
------------------------------------------------
空格       向下滚动一屏
b         向上滚动一屏
回车       向下滚动一行
y         向上滚动一行
d         向下滚动半屏
u         向上滚动半屏
h         less的帮助
g         跳到第一行
G         跳到最后一行
/字串      向下搜寻[字串]的功能，n:向下查找，N:向上查找
?字串      向上搜寻[字串]的功能，n:向上查找，N:向下查找
q         退出less
------------------------------------------------
更全的：
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Left  one half screen width (or N positions).
  ESC-(  LeftArrow  *  Right one half screen width (or N positions).
  F                    Forward forever; like "tail -f".
  r  ^R  ^L            Repaint screen.
  R                    Repaint screen, discarding buffered input.
---------------------------------------------------------------------------
```

```
>指令和>>指令,他们可以创建文件（如果文件不存在）
>为输出重定向，>>为追加
1) ls -l > 文件         列表的内容覆盖到文件
2) ls -la >> 文件		  列表的内容追加到文件
3) cat 文件1 > 文件2     文件1内容覆盖文件2
4) echo "内容" >> 文件

cal[calendar]，显示日历


echo 指令
echo [选项] [输出内容]
应用，使用echo指令输出环境变量，输出当前的环境路径
$ echo $PATH 
/usr/local/bin:/usr/bin:/home/better/bin:/usr/local/sbin:/usr/sbin

head 命令
$ head [-n 5][-5] 文件，显示文件的开头5行，默认为10行
tail 命令
$ tail [-n 5][-5] 文件，显示文件的结尾5行，默认为10行
$ tail -f[follow] 文件，实时追踪该文档的所有更新,ctrl+c退出


ln指令
软链接🔗，也叫符号链接，类似于windows里的快捷方式，主要存放了链接其他文件的路径
$ ln -s[symbolic] [原文件或目录] [软链接名] （功能：给原文件创建一个软链接）
其中，如果软链接一个目录，进入这个目录，pwd后，仍在软链接所在位置,`我的电脑`是一个软链接
如下：`/home/better/桌面/我的电脑/home/better`
`/home/better/桌面/我的电脑/home/better/桌面/我的电脑/home/……`

删除软链接注意！
$ rm -rf 我的电脑, 不要加`/`，如果加`/`，会吧该目录下面的内容删除。

history指令
查看已经执行过历史命令，也可以执行历史命令
$ history     查看所有历史命令
$ history 10  查看最近使用过的10个命令
$ !5          执行历史编号为5的指令
```

## 日期时间类指令

```
***时间日期类***

date指令，显示当前日期
1)date             			显示当前时间
2)date +%Y                  显示当前年份
3)date +%m                  显示当前月份
4)date +%d                  显示当前是哪一天
5)date "+%Y-%m-%d %H:%M:%S" 显示年月日时分秒（`+`不要丢）

设置日期
$ date -s[set] "2020-10-10 11:22:22"

cal[calendar]查看日历
$ cal 31 3 2018
-------------------------------------
用法：
 cal [选项] [[[日] 月] 年]
选项：
 -1, --one        只显示当前月份(默认)
 -3, --three      显示上个月、当月和下个月
 -s, --sunday     周日作为一周第一天
 -m, --monday     周一用为一周第一天
 -j, --julian     输出儒略日
 -y, --year       输出整年
-------------------------------------

```

## 搜索查找类

```
***搜索查找类***

find指令
find指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端
find [搜索范围] [选项]
选项:
-name<查询文件名>  按照指定的文件名查找模式查找文件
$ find /home -name 1.txt 或 *.txt
-user<用户名>    查找属于指定用户名所有文件
$ find /opt -user root
-size<文件大小>  按照指定的文件大小查找文件
$ find / -size +20M/+20k         大于20M
               -20M              小于20M
                20M              等于20M
按ctrl+c退出检索
```
locate指令  
locate指令可以快速定位文件路径。locate指令利用事先建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件，locate指令无需遍历整个文件系统，查询速度较快。为了保证查询结果的准确度，管理员必须定期更新locate时刻。  

```
$ locate 搜索文件
第一次运行前，必须使用updatedb[data-base]指令创建locate数据库。
# updatedb / $ sudo[Superuser do] updatedb

grep指令和管道符号|
grep过滤查找，管道符,"|",表示将前一个命令的处理结果输出传递给后面的命令处理
grep [选项] 查找内容 源文件
-n[list-number] 显示匹配行及行号
-i[ignore-case] 忽略字母大小写
$ grep -ni hello 1.c 或者 $ cat 1.c | grep -ni hello

```

## 压缩和解压命令

```
***压缩和解压命令***

gzip和gunzip指令
gzip[GNU zip]用于压缩文件，只能压缩为*.gz文件,gunzip[GNU unzip]用于解开被gzip压缩的文件。
但是压缩后，原文件就没有了。
$ gzip 1.c        ==>   生成`1.c.gz`, `1.c`就没有了
$ gunzip 1.c.gz   ==>   r生成`1.c`  , `1.c.gz`就没有了
在 Linux 中，打包和压缩是分开处理的。而 gzip 命令只会压缩，不能打包，所以才会出现没有打包目录，而只把目录下的文件进行压缩的情况。


zip/unzip命令
zip用于压缩文件，unzip用于解压的，这个在项目打包发布中很有用的
zip [选项] dest.zip 要压缩的目录或文件  
$ zip -r dest.zip /home/
-r[recursively] 递归压缩，即压缩目录~

unzip [选项] source.zip
unzip选项：-d<directory>,指定解压后文件的存放目录
$ unzip -d dest/ source.zip，dest目录可以不存在

tar[tape archive]指令
tar指令是打包指令，最后打包的文件是`.tar.gz`的文件。
tar [选项] dest.tar.gz 打包内容 （打包目录或文件）
-c   产生.tar打包文件[create]
-v   显示详细信息[verbose]
-f   指定压缩后的文件名[file]
-z   打包同时压缩[gzip]
-x   解包.tar文件[extract]
$ tar -zcvf a.tar.gz 1.c 2.c (f在最后一个)
$ tar -zcvf a.tar.gz /home/  注意和/home/*的区别
解压
$ tar -zxvf a.tar.gz
$ tar -zxvf a.tar.gz -C[directory指定解压目录] /home/ 注意，指定解压目录必须存在
```

## 组管理和权限管理

```
Linux中的每个用户必须属于一个组，不能独立于组外。
Liunx每个文件具有1.所有者2.所在组3.其他组的概念

1)所有者
2)所在组
3)其它组
4)改变用户所在的组

文件/目录的所有者
一般来说，文件的创建者，便成为该文件的所有者
查看文件的所有者:
$ ls -ahl[all,human-readable,long],
`-rw-rw-r--.  1 better better    0 8月   1 20:51 1.c`
中间两个分别为所有者和所在组。而所在的组，一般是所有者所在的组，但是也可以改变。

修改文件所有者
chown[change owner] 用户名 文件名, 但是文件的所在组没有变化。

修改文件所在组
chgrp[change group] 组名 文件名 ，但是文件的所有者没有变。

其它组：除文件的所有者和所在组的用户外，系统的其他用户都是文件的其它组。

改变用户所在组
1)# usermod -g[group] 组名 用户
2)# usermod -d 目录名 用户名，改变该用户登录的初始目录


*权限的基本介绍*
ls -l显示:
`-rw-r--r--.  1 better better    0 8月   1 20:51 1.c`

第一个字符`-`表示文件类型,`-`是普通文件，`d`是目录，`l`是软链接，`c`是字符设备(鼠标，键盘),`b`是块文件，硬盘

第二到第四个字符`rw-`表示文件所有者拥有的权限，r是读，w是写，-是没有权限

第5到第7个字符`r--`表示文件所在组的用户的权限，`r--`只读

第8到第10个字符`r--`表示文件其它组的用户的权限，`r--`只读

`1` ，如果是文件，表示硬链接的数，一般是1，如果是目录，表示该目录的子目录的个数。

better是文件所有者，后面的better是文件所在组

`0`   表示文件的大小，不加单位指单位是字节,Byte
如果是目录的话，该值为4096(字节)

`8月  1 20:51`是文件的最后修改时间

```

rwx权限  
1. rwx作用到文件  
    1) [r]代表可读，可以读取查看  
    2) [w]代表可写,可以修改，但是不代表可以删除该文件，删除一个文件的前提条件是对该文件所在的目录有写权限，才能删除文件  
    3) [x]代表可执行[execute]:可以被执行  
2. rwx作用到目录  
    1) [r]代表可读，可以读取，ls查看目录内容  
    r权限：拥有此权限表示可以读取目录结构列表，也就是说可以查看目录下的文件名和子目录名，注意：仅仅指的是名字。  
    2) [w]代表可写，可以修改，在该目录内 创建+删除+重命名 文件或目录  
    w权限：拥有此权限表示具有更改该目录结构列表的权限，总之，目录的w权限与该目录下的文件名或子目录名的变动有关，注意：指的是名字。具体如下：  
           1.在该目录下新建新的文件或子目录。   
           2.删除该目录下已经存在的文件或子目录（不论该文件或子目录的权限如何），注意：这点很重要，用户能否删除一个文件或目录，看的是该用户是否具有该文件或目录所在的目录的w权限。  
           3.将该目录下已经存在的文件或子目录进行重命名。  
           4.转移该目录内的文件或子目录的位置。  
    3) [x]代表可执行，可以进入该目录  
           x权限：拥有目录的x权限表示用户可以进入该目录成为工作目录，能不能进入一个目录，只与该目录的x权限有关，如果用户对于某个目录不具有x权限，则无法切换到该目录下，也就无法执行该目录下的任何命令，即使具有该目录的r权限。且如果用户对于某目录不具有x权限，则该用户不能查询该目录下的文件的内容，注意：指的是内容，如果有r 权限是可以查看该目录下的文件名列表或子目录列表的。所以要开放目录给任何人浏览时，应该至少要给与r及x权限。  

```
**权限管理**
chmod[change mode] 修改文件或目录权限
1)u:所有者 g:所在组 o:其他人 a:所有人(u、g、o的总和)
 $ chmod u=rwx,g=rx,o=x 文件，给该文件的所有者读写执行的权限，所在组读和执行的权限，其他组执行的权限,当文件某个权限有x时，就会在终端显示成绿色。
 
 $ chmod o+w 文件，其它组用户增加写权限
 $ chmod a-x 文件，给所有用户减去执行权限
 $ chmod u-x,g+w 1.c，这样写。
如果使其它组没有权限，chmod 'o=' 或者 'o=-' 或者 'o=--' 或者 'o=---'

2)数字方式
r=4, w=2, x=1
rwx   = 4+2+1 = 7
rx    = 4+1   =5
x     = 1 
无权限 = 0
chmod 751 1.c ,表示chmod u=7,g=5,o=1 1.c，即chmod u=rwx,g=rx,o=x 1.c
改变目录及其子文件子目录可以 chmod -R 777 1.c

*修改文件所有者chown*
1)# chown newowner file 改变文件的所有者
2)# chown newowner:newgroup file 改变文件的所有者和所在组
3)-R[--recursive] 如果是目录，则使得其下所有文件或目录递归生效

修改文件所在组
# chgrp newgroup 文件或目录
# chgrp -R newgroup 目录
/home 该目录下，除root外，其他用户没有w权限

只有root用户可以修改文件所在组和所有者
对于文件目录的权限，只有所有者和root用户可以修改
```

## 任务调度

```
crond任务调度,系统在某个时间执行的特定的命令或程序
分类：
1.系统工作：有些重要的工作必须周而复始地执行。如病毒扫描等
2.个别用户工作：个别用户可能希望执行某些程序，比如备份
语法
crontab [选项]
-e[edit] 编辑crontab定时任务
-l[Displays the current crontab on standard output.]     查询crontab任务
-r[Removes the current crontab]     删除当前用户所有的crontab任务 
service crond restart 重启任务调度
 
1.如果只是简单的任务，可以不用写脚本，直接在crontab中加入任务即可
2.对于比较复杂的任务，需要些脚本（shell编程）

1)在crontab中输入 `*/1 * * * * ls -l /home >> /home/better/桌面/1.txt` 
 表示每小时的每分钟执行ls -l /home >> /home/better/桌面/1.txt 命令

5个占位符的说明
第一个`*`表示一小时当中的第几分钟 0-59
第二个`*`表示一天中的第几小时    0-23
第三个`*`表示一个月中的第几天    1-31
第四个`*`表示一年中的第几月      1-12
第五个`*`表示一周当中的星期几     0-7（0和7表示星期日）

参数说明
*     代表任何时间
,     代表不连续的时间，`8,9,10`表示这三个时间都执行任务
-     代表连续的时间范围。比如`1-6`表示连续六个时间
*/n   代表每隔多久执行一次， */1和*效果一样
```

![image-20200803162445685](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232048717.jpg)

```
任务调度的应用
1）我们编写脚本文件实现每隔1分钟将日期追加到文件
①编写文件 /home/better/桌面/task.sh
  添加内容 date >> /home/better/桌面/1.txt
②给task.sh一个可执行权限（根据谁要执行这个脚本来确定权限）
③crontab -e 
④添加`* * * * * /home/better/桌面/task.sh`
```

## Linux磁盘分区、挂载

```
分区方式
1)MBR分区：[Master Boot Record]
  1.最多支持四个主分区
  2.系统只能安装在主分区
  3.扩展分区要占一个主分区
  4.MBR最大只支持2TB，但拥有最好的兼容性
2)GPT分区[GUID Partition Table]
  1.支持无限多个主分区（但操作系统可能限制，windows最多128个分区）
  2.最大支持18EB的大容量
  3.windows7 64位以后支持gpt
```

windows分区

![image-20200804001015963](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232049675.jpg)

Linux分区  

Linux来说无论有几个分区，分给哪一目录使用，它归根结底就只有一个根目录，一个独立且唯一的文件结构, Linux中每个分区都是用来组成整个文件系统的一部分。  
Linux采用了一种叫“载入”的处理方法，它的整个文件系统中包含了一整套的文件和目录，且将一个分区和一个目录联系起来。这时要载入的一个分区将使它的存储空间在一个目录获得。  


![image-20200803191629543](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232049027.jpg)

硬盘说明
1)   Linux硬盘分IDE硬盘和SCSI硬盘，目前基本上是SCSI硬盘  
2)  对于IDE硬盘， 驱动器标识符为“hdx\~",其中“hd”表明分区所在设备的类型，这里是指IDE硬盘了。“x"为盘号(a为基本盘，b为基本从属盘，c为辅助主盘，d为辅助从属盘),“~”代表分区，前四个分区用数字1到4表示，它们是主分区或扩展分区，从5开始就是逻辑分区。例，hda3表示为第一个IDE硬盘上的第三个主分区或扩展分区,hdb2表示为第二个IDE硬盘上的第二个主分区或扩展分区.  
3)  对于SCSI硬盘则标识为'sdx~", SCSI硬盘是用“sd"来表示分区所在设备的类型的，其余则和IDE硬盘的表示方法一样。  

```
$ lsblk[list block device] -f ， 查看自己的系统分区情况
Swap分区在系统的运行内存不够用的时候，把物理内存中的一部分空间释放出来，以供当前运行的程序使用。
----------------------------------------------------------------------------------
NAME            FSTYPE  LABEL   UUID                                   MOUNTPOINT
sda
├─sda1          xfs             71020384-c026-493d-9b87-138b700b8022   /boot
└─sda2          LVM2_me         KmJqpC-MiUP-aGvk-0UWh-ycM9-yn83-cJo6dp
  ├─centos-root xfs             15a68c53-18ab-4960-a185-f382e1c3070e   /
  └─centos-swap swap            f0a429f4-5d07-4488-bb09-a541ba69590c   [SWAP]
sr0             iso9660 CentOS 7 x86_64
                                2020-04-22-00-54-00-00                 /run/media
-----------------------------------------------------------------------------
$ lsblk 查看具体大小
--------------------------------------------------------------------------
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0   20G  0 disk
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   19G  0 part
  ├─centos-root 253:0    0   17G  0 lvm  /
  └─centos-swap 253:1    0    2G  0 lvm  [SWAP]
sr0              11:0    1  4.5G  0 rom  /run/media/better/CentOS 7 x86
--------------------------------------------------------------------------
```

![image-20200803193315870](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232050481.jpg)

```
挂载案例
增加一块2G硬盘，标识为sdb1，挂载到/home/newdisk
1)虚拟机添加硬盘 ，在设置里添加
2)分区    fdisk /dev/sdb（下图）
3)格式化   mkfs -t ext4 /dev/sdb1
4)挂载    先创建文件/home/newdisk  挂载 mount /dev/sdb1 /home/newdisk
5)设置可以自动挂载(永久挂载) 
  vim /etc/fstab
  增加内容，`/dev/sdb1（分区）    /home/newdisk(挂载点)   ext4(类型)    defaults  0 0`
  mount -a 自动挂载即刻生效
  
卸载 umount /dev/sdb1 或者 umount /home/newdisk

```

![image-20200803201327105](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232051761.jpg)



## 磁盘情况查询

```
查询系统整体磁盘使用情况
$ df[disk find] [-h]/[-lh]
--------------------------------------------------------------
文件系统                 容量  已用  可用 已用% 挂载点
devtmpfs                 894M     0  894M    0% /dev
tmpfs                    910M     0  910M    0% /dev/shm
tmpfs                    910M   11M  900M    2% /run
tmpfs                    910M     0  910M    0% /sys/fs/cgroup
/dev/mapper/centos-root   17G  4.8G   13G   29% /
/dev/sda1               1014M  187M  828M   19% /boot
tmpfs                    182M   28K  182M    1% /run/user/1000
--------------------------------------------------------------

查询指定目录的磁盘占用情况
du -h [目录]
默认为当前目录，-s指定目录占用大小汇总，-h带计量单位，-a含文件
--max-depth=1 子目录深度，-c列出明细的同时，增加汇总值
-s仅仅显示该目录的占用大小，c是列出明细也显示总的占用大小，a包含文件。
--------------------------------------------------------------------
$ du -ach --max-depth=1 /home/better
58M	/home/better/.mozilla
4.0K	/home/better/.bash_logout
4.0K	/home/better/.bash_profile
4.0K	/home/better/.bashrc
du: 无法读取目录"/home/better/.cache/gnome-control-center": 权限不够
91M	/home/better/.cache
4.0K	/home/better/.dbus
du: 无法读取目录"/home/better/.config/gnome-control-center": 权限不够
124K	/home/better/.config
8.0K	/home/better/.ICEauthority
19M	/home/better/.local
4.0K	/home/better/.esd_auth
0	/home/better/桌面
0	/home/better/下载
0	/home/better/模板
0	/home/better/公共
0	/home/better/文档
0	/home/better/音乐
876K	/home/better/图片
0	/home/better/视频
4.0K	/home/better/.bash_history
13M	/home/better/.oh-my-zsh
0	/home/better/.pki
40K	/home/better/.zcompdump-localhost-5.0.2
20K	/home/better/.zsh_history
4.0K	/home/better/.lesshst
4.0K	/home/better/.zshrc
4.0K	/home/better/.viminfo
181M	/home/better
181M	总用量
--------------------------------------------------------------------------

另外的工作使用指令
1）统计/home文件夹下文件的个数
  $ ls -l /home | grep "^-" | wc -l[lines]   ,(ls -la可以查询包括隐藏文件在内的文件)
  wc -l是统计前面的行数
  "^-"是正则表达式，表示找以`-`开头的一行
2) 统计/home文件夹下目录的个数
  $ ls -l /home | grep "^d" | wc -l
3) 统计/home文件夹下文件的个数，包括子文件夹里的
  $ ls -lR /home | grep "^-" | wc -l
4) 统计/home文件夹下目录的个数，包括子文件夹里的
  $ ls -lR /home | grep "^d" | wc -l
5) 以树状显示目录结构
  # yum install tree
  $ tree /home
  如果中文无法显示，使用 $ tree -N
  -N[ Print  non-printable  characters  as  is  instead of as
  escaped octal numbers.]
  -L 1 , 显示1层目录
  
  
```

## 网络配置

### 网络配置原理图

NAT模式（网络环境）

windows有两块网卡，一个是虚拟网卡，这个可以和linux联通，另一个是无线网卡，可以通过网关和因特网连接，这样虚拟机就可以通过本机再和因特网相连。

![image-20200804104236867](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232051184.jpg)

### 查看网络IP和网关

```
linux&mac $ ifconfig 
win       $ ipconfig
在mac利用 ifconfig 可以查看vmnet8虚拟网卡的ip地址(inet)，子网掩码(netmask)
在mac利用 ifconfig en0 可以查看本机网卡的ip地址等等
---------------------------------------------------------------------------------
→ ifconfig en0
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=400<CHANNEL_IO>
	ether a4:83:e7:42:ce:24
	inet6 fe80::55:1e2a:2c4d:3e%en0 prefixlen 64 secured scopeid 0x6
	inet 192.168.1.4 netmask 0xffffff00 broadcast 192.168.1.255
	inet6 2409:8a3c:810d:af00:1459:6faf:f263:b4da prefixlen 64 autoconf secured
	inet6 2409:8a3c:810d:af00:edd6:d6c7:375d:eaff prefixlen 64 autoconf temporary
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect
	status: active
---------------------------------------------------------------------------------
利用ifconfig vmnet8 查看虚拟网卡的ip
---------------------------------------------------------------------------
→ ifconfig vmnet8
vmnet8: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	ether 00:50:56:c0:00:08
	inet 172.16.104.1 netmask 0xffffff00 broadcast 172.16.104.255
---------------------------------------------------------------------------

查看虚拟网卡的网关和子网掩码
/Library/Preferences/VMware\ Fusion/vmnet8/nat.conf 里更改
（或者 `VMware Fusion` 这样表示是同一个文件夹名称）
-----------------------
# NAT gateway address
ip = 172.16.104.2
netmask = 255.255.255.0
----------------------
```

### ping测试主机之间网络连通性

```
$ ping 目标主机 （测试当前服务器是否可以连接目标主机）

检测主机连接命令ping:
是一种网络检测检测工具，它主要是用检测远程主机是否正常，或是两部主机间
的介质是否为断、网线是否脱落或网卡故障。
如: ping对方ip地址
```

### 设置linux自动获取ip

在设置中打开，但每次自动获取的ip不一定一样

<img src="https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232051912.jpeg" alt="image-20200804121214072" style="zoom: 33%;" />

### 设置linux指定ip

```
$ vim /etc/sysconfig/network-scripts/ifcfg-ens33
重启网络服务 service network restart
再用 ifconfig 查看ip为自己设置的ip
------------------------------------------
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"        //静态的，默认是dhcp
IPADDR="172.16.104.134"   //静态的ip地址（$ ifconfig查看）
NETMASK="255.255.255.0"   //子网掩码 ($ ifconfig)
GATEWAY="172.16.104.2"    //网关地址 ($ route -n)
DNS1="172.16.104.2"       //DNS服务器($ cat /etc/resolv.conf)
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="b33ea49f-94b8-4ed1-8440-09596e61ceca"
DEVICE="ens33"
ONBOOT="yes"              //自动启动
------------------------------------------

```

## 进程管理

1)在LINUX中，每个执行的程序(代码)都称为一个进程。每一个进程都分配-一个ID号。  
2)每一个进程，都会对应一个父进程，而这个父进程可以复制多个子进程。例如www服务器。  
3)每个进程都可能以两种方式存在的。前台与后台，所谓前台进程就是用户目前的屏幕上可以进行操作的。后台进程则是实际在操作，但由于屏幕上无法看到的进程，通常使用后台方式执行。  
4)一般系统的服务都是以后台进程的方式存在，而且都会常驻在系统中。直到关机才才结束。  

### 查看进程

```
ps[processes snapshot]指令可查看目前系统的软件执行情况，可以不加参数
ps可显示
PID    进程识别号
TTY    终端机号
TIME   此进程所占用CPU时间
CMD    正在执行的命令或进程名
选项
-a 显示当前终端的所有进程信息
-u 以用户的格式显示进程信息
-x 显示后台进程运行的参数

$ ps -aux
---
用户名      进程id 
 |           |  占用的cpu 
 |           |   | 占用内存 使用的虚拟内存（单位KB）
 |           |   |    |      |  使用的物理内存（单位KB）
 |           |   |    |      |     |  使用的终端 进程的状态`S:休眠,R:运行`
 |           |   |    |      |     |   |       |  启动时间 占用cpu时间 进程执行时命令行
 |           |   |    |      |     |   |       |    |       |        |
USER        PID %CPU %MEM    VSZ   RSS TTY    STAT START   TIME COMMAND
root        2   0.0  0.0     0     0   ?      S    06:10   0:00 [kthreadd]
---
更具体的，STAT进程状态，有很多
S 睡眠，s 表示该进程是会话的先导进程，N表示进程拥有比普通优先级更低的优先级
R 正在运，D 短期等等，Z僵死进程，T 被跟踪或者被停止

利用grep过滤
$ ps -aux|grep xxx ，注意这条指令也会被算进进程

$ ps -ef  查看进程的父进程
`UID         PID   PPID  C STIME TTY          TIME CMD` PPID为父进程id
查找父进程 $ ps -ef | grep sshd

```

### 终止进程

```
kill & killall

kill [选项] 进程号（通过进程号杀死进程）
-9 强迫进程终止

killall 进程名称(通过进程名来杀死进程，支持通配符，在负载过大而变慢时使用)
通配符如 A* 表示以A开头的进程

应用
1)踢掉某个非法用户
  先 ps -aux | grep sshd
  再`better 25675 0.0 0.1 161012  2384 ?  S    13:06   0:00 sshd: better@pts/0`
  其中pts/0表示[pseudoterminal master and slave]，伪终端的意思
  查看进程id，25675，kill 25675即可。
2)终止远程登录服务sshd，然后重启sshd服务
  通过 ps -aux | grep sshd
  `root   1154  0.0  0.2 112924 4352 ?  Ss  06:10 0:00 /usr/sbin/sshd -D`
  $ kill 1154
  重启  service sshd restart
3)终止多个gedit编辑器
  killadll gedit
4)强制杀掉一个终端
  $ kill -9 xxxx 
```

### 查看进程树

```
pstree [选项],更加直观的来看进程信息
-p 显示进程PID
-u 显示进程的所属用户
```

### 服务管理

服务的本质就是进程，但是是运行在后台的，通常都会监听某个端口，等待其他程序的请求，比如(mysql-3306、sshd-22、防火墙等)，因此我们又称之为守护进程  

```
service管理指令
service 服务名 [start|stop|restart|reload|status]
在Centos7.0后 不再使用service，而是systemctl
systemctl [start|stop|restart|reload|status] 服务名

案例
1)查看防火墙状态、重启、关闭
 $ systemctl status firewalld   |  $ service iptables status 
 $ systemctl stop   firewalld   |  $ service iptables stop 
 $ systemctl start  firewalld   |  $ service iptables start
另外，这种关闭的方式仅仅临时生效，重启系统后，回归以前的设置。
如果要永久关闭或启动，利用chkconfig指令。

2)其中telnet指令可以检查linux的某个端口是否在监听，并且可以访问
 telnet ip 端口
 telnet 172.16.xxx.xxx 22 显示`SSH-2.0-OpenSSH_7.4`即可
 
查看服务名
方式1，使用setup, 找到自己的系统服务。
方式2，ls -l /etc/init.d/ 注意最后加`/`
   然而在centos7以上，在另一个地方，ls -l /usr/lib/systemd/
   

服务的运行级别（runlevel）
查看或者修改默认级别， vim /etc/inittab（centos7以上不再使用），以下为centos7内容
------------------------------------------------------------------------
# inittab is no longer used when using systemd.
# systemd uses 'targets' instead of runlevels. By default, there are two main 
targets:
#
# multi-user.target: analogous to runlevel 3
# graphical.target: analogous to runlevel 5
#
# To view current default target, run:
# systemctl get-default
#
# To set a default target, run:
# systemctl set-default TARGET.target
------------------------------------------------------------------------
```

![image-20200804163734908](https://gitlab.com/imingx/picgo/-/raw/main/2024/202408232052186.jpg)

```
开机流程
开机—>BIOS->/boot->init进程->运行级别->运行级对应的服务
```

```
chkconfig指令，设置完后重启才能生效
通过chkconfig指令可以给每个服务的各个运行级别设置自启动/关闭
基本语法
1)查看服务 chkconfig --list | grep xxx
2)chkconfig xxx --list ,跟1）一样
3)chkconfig --level 5 服务名 on/off ，在某个运行级别下启动/不启动
  不写`--level 5`表示在所有级别下

---------------------------------------------------------- 
$ chkconfig --list (centos 7 以上显示以下内容,target就是runlevel)
注：该输出结果只显示 SysV 服务，并不包含
原生 systemd 服务。SysV 配置数据
可能被原生 systemd 配置覆盖。

      要列出 systemd 服务，请执行 'systemctl list-unit-files'。
      查看在具体 target 启用的服务请执行
      'systemctl list-dependencies [target]'。
-----------------------------------------------------------
所以在centos7及以上
使用$ systemctl list-unit-files | grep sshd 来查看
```

### 进程监控

```
动态监控进程

top指令，top和ps命令很相似，它们都用来显示正在执行的进程。Top与ps最大的不同之处，在于top
在执行一段时间可以更新正在运行的进程
top [选项]
-------------------------------------------
-d 秒数   指定top每隔几秒刷新，默认3秒
-i       使top不显示任何闲置或者僵死进程  
-p       通过指定监控进程ID来仅仅监控某个进程状态
-------------------------------------------
交互操作(大写)
---------------------------
P     以CPU使用率排序（默认）
M     以内存的使用率排序
N     以PID排序
q     退出top
---------------------------
显示内容为以下
-----------------------------------------------------------------------
top - 17:23:09 up 10:04,  2 users,  load average: 0.01, 0.02, 0.05
Tasks: 217 total,   2 running, 215 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.2 us,  0.2 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,0.0 st
KiB Mem :  1863040 total,   144728 free,   813728 used,   904584 buff/cache
KiB Swap:  2097148 total,  2096884 free,      264 used.   845844 avail Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+
  2655 better    20   0  642816  28540  19860 S   0.3  1.5   1:04.41
-----------------------------------------------------------------------

各名词解释
-----------------------------------------------------------------------

17:23:09        当前时间
up 10:04        系统运行时间，时:分
2 users         登录的用户数

load average    系统负载，即任务队列的平均长度，三个数值分别是
0.01,0.02,0.05  1、5、15分钟到目前的平均值

Task:217 total  进程总数
2 running       正在运行的进程数
215 sleeping    睡眠的进程数
0 stopped       停止的进程数
0 zombie        僵尸进程数
0.2 us          用户空间占用CPU百分比
0.2 sy          内核空间占用CPU百分比
0.0 ni          用户进程空间内改变过优先级的进程占用CPU百分比
99.7 id         空闲CPU百分比
0.0 wa          等待输入输出的CPU时间百分比
0.0 hi          硬中断（Hardware IRQ）占用CPU的百分比
0.0 si          软中断（Software Interrupts）占用CPU的百分比
0.0 st   
KiB Mem:x total 物理内存总量
x free          空闲内存总量        | 空闲交换区总量
x used          使用的物理内存总量   | 使用的交换区总量
x buff/cache    用作内核缓存的内存量  
KiB Swap:xtotal 交换区总量
x avail Mem     代表可用于进程下一次分配的物理内存数量
-----------------------------------------------------------------------
PID	    进程id
PPID	父进程id
RUSER	Real user name
UID	    进程所有者的用户id
USER	进程所有者的用户名
GROUP	进程所有者的组名
TTY	    启动进程的终端名。不是从终端启动的进程则显示为 ?
PR	    优先级
NI	    nice值。负值表示高优先级，正值表示低优先级
P	    最后使用的CPU，仅在多CPU环境下有意义
%CPU	上次更新到现在的CPU时间占用百分比
TIME	进程使用的CPU时间总计，单位秒
TIME+	进程使用的CPU时间总计，单位1/100秒
%MEM	进程使用的物理内存百分比
VIRT	进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
SWAP	进程使用的虚拟内存中，被换出的大小，单位kb
RES 	进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
CODE	可执行代码占用的物理内存大小，单位kb
DATA	可执行代码以外的部分(数据段+栈)占用的物理内存大小，单位kb
SHR	    共享内存大小，单位kb
nFLT	页面错误次数
nDRT	最后一次写入到现在，被修改过的页面数。
S  		进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程
COMMAND	命令名/命令行
WCHAN	若该进程在睡眠，则显示睡眠中的系统函数名
Flags	任务标志
-----------------------------------------------------------------------

top翻页按键
shift+<、shift+>，好像不太完备

案例
1) 监视特定用户
  top执行后，按`u`，再输入用户名，确定
2) 终止指定的进程
  输入`k`,输入PID即可  
```

```
监控网络状态
netstat [选项]
-an 按一定顺序排列输出
-p  显示哪个进程在调用
$ netstat -anp，查看所有的
$ netstat -anp | grep sshd
```

## RPM和YUM

### RPM包的管理

```
介绍：
一种用于互联网下载包的打包及安装工具，它包含在某些Linux分发版中。它生成
具有.RPM扩展名的文件。RPM是RedHat Package Manager ( RedHat软件包管理工
中具)的缩写，类似windows的setup.exe，这一文件格式名称虽然打上了RedHat的
标志，但理念是通用的。
Linux的分发版本都有采用(suse,redhat, centos 等等)，可以算是公认的行业标
准了。

rpm包的简单查询指令：
$ rpm -qa | less      查询所安装的所有rpm软件包
$ rpm -qa | grep xx   查询某个软件是否安装
$ rpm -q  软件包名     查询软件包是否安装
$ rpm -qi 软件包名     查询软件包信息
$ rpm -ql 软件包名     查询软件包中的文件
$ rpm -qf 文件全路径名  查询文件所属的软件包
|
 rpm -qf /etc/passwd
 rpm -qf /root/install.log
 
--
$ rpm -qa | grep firefox
firefox-68.5.0-2.el7.centos.x86_64
--

rpm包名基本格式: 
一个rpm包名: firefox-68.5.0-2.el7.centos.x86_64
名称:firefox
版本号: 68.5.0-2
适用操作系统: el7.centos.x86_64
表示centos7.x的64位系统
如果是i686、i386表示32位系统，noarch表示通用。


卸载rpm包
rpm -e RPM包的名称
如果要卸载的rpm包是其他软件包所依赖的，那么卸载会产生错误
如果要强制卸载，就要 rpm -e --nodeps foo

安装rpm包
rpm -ivh RPM包全路径名称
-i[install] 安装
-v[verbos]  提示
-h[hash]    进度条

步骤，先找到rpm包，挂载上安装centos的iso文件，然后到/media/去找rpm包
然后 cp firefox-68.5.0-2.el7.centos.x86_64.rpm /opt/
进入/opt/然后 rpm -ivh firefox-68.5.0-2.el7.centos.x86_64.rpm
即可
```

### YUM

```
Yum是一个shell前端软件包管理器，基于RPM包管理，能够从指定的服务器自动下载RPM包安装
可以自动处理依赖性关系，并且一次安装所以依赖的软件包

- yum可以自己设置镜像，更改yum源，待办
基本指令
$ yum list | grep xx  查询yum服务器是否有需要的软件
$ yum install xxx     下载安装指定yum包，默认安装最新版的
```



