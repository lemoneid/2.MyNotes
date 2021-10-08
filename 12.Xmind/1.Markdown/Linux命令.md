# Linux命令

## Linux认识

### shell

- shell是人机交互的接口，是一种命令解释器。
- 内置：内核中的系统调用
- 非内置：$PATH 寻找可执行程序，从系统中调入内存执行

### printenv

-  打印部分或者所有的环境变量

### set 

- 设置 shell 选项

### export

- 导出环境变量

### alias

- 设置命令别名

### termina

- 终端，是一个封装的程序,一个terminal运行一个shell来扩充功能

### 程序

- 可执行的二进制文件，cmd

### 进程 

- 虚拟内存

	- 对程序存储器的抽象

- 对正在运行的程序的一种抽象
- 文件

	- 对I/O设备的抽象

## 用户

### 1. useradd yzw 名称		新建用户 

### 2. usermod -G sudo yzw   修改用户组,添加到sudo  赋予root权限,执行超管命令

### 3. su - yzw 切换到普通用户

### 4. 切换到root sudo -i       su - root   

## 命令系统

### 帮助手册

- tldr
- man

	- -k

		- 等同于 whatis，关键字

	- -f

		- 等同于 apropos
		- man -f tty

- info

### history

### 通配符

- *

	- 0或多个

- ?

	- 任意一个

- [list]

	- list中任意单一

- [!list] 
[^list]
- [c1-c2]
- [!c1-c2] 
[^c1-c2]
- {s1, s2, s3}
- [:alnum:]       匹配任意一个字母或者数字
[:alpha:]       匹配任意一个字母
[:digit:]       匹配任意一个数字
[:lower:]       匹配任意一个小写字母
[:upper:]       匹配任意一个大写字母

### 任务管理

- &

	- cmd & 

- ；

	- 顺序

- && ||
- ``

	- `cmd`优先执行；将其结果带入父命令执行 

- Ctrl + Z

	- 暂时挂起

- bg

	- 将挂起的命令后台运行
	- bg %num 

- fg

	- 将后台执行的命令转为前台执行
	- fg %num
	- %和fg  默认为最近一次

- jobs

### 信号signal

- 常见信号

	- 1 HUP

		- 终端挂起。控制进程终止

	- 2 INT

		- 键盘中断：终止进程  Ctrl+C

	- 3 QUIT

		- 键盘退出：退出程序  Ctrl+D Ctrl+\

	- 9 KILL

		- 无条件终止进程：可杀死任何进程

	- 15 TERM

		- kill默认，程序结束信号：与kill不同，TERM信号可被阻塞和终止

	- 1 HUP 挂起
2 INT 中断
3 QUIT 结束运行
9 KILL 无条件终止
11 SEGV 段错误
15 TERM 尽可能终止
17 STOP 无条件停止运行,但不终止
18 TSTP 停止或暂停,但继续在后台运行

- kill

	- 发送信号
	- kill -9 pid
	- kill -l

- 进程

	- 结束进程

		- pkill

			- 根据名字，删除单个进程

		- killall

			- 结束同名所有进程

	- 查看进程

		- top

			- 动态进程查看

		- ps -aux -ef
		- pstree

### 管道、重定向

- echo

	- echo $? 上一条执行命令的返回值，0为成功
	- 回响，打印

- I/O设备

	- stdin

		- 0

	- stdout

		- 1

	- stderr

		- 2

	- 典例：ping

- 重定向

	- 输入重定向

		- >   
>>
		- 2>   
2>>
		- $>  相当于二次重定向2>&1 
$>>

	- 输出重定向

		-  <
		- <<END

			- 多行输入；(END为多行输入的结束标志)
通常用于脚本创建新文件时写入固定内容; 
END就是一个结束符，可自定义EOF
			- cat >> tmp << EOF

- 管道

	- |

		- 把前一个命令的执行结果当做后一个命令的输入

### 转义符

- ‘单引号’

	- 硬转义，其内部所有的shell 元字符、通配符都会被关掉。

- "双引号"

	- 软转义，其内部只允许出现特定的shell 元字符
	- $用于参数替换; 
	- `(反单引号，esc键下面)用于命令替换;
	- \用于转义单个字符

- \反斜杠

	- 去除其后紧跟的元字符或通配符的特殊意义

### shell元字符

- =

	- 赋值，var=value 中间无空格

- $

	- 变量值替换

		- ${变量名}
		- $0...$9..${10}

			- 参数

		- $[]整数计算
		- 实例：mkdir $(echo a{A{1,2},B{3,4}}b);

- ``

	- 取命令的执行结果， 与$有相似之处
	- 实例：mkdir `(echo a{A{1,2},B{3,4}}b)`

- !

	- 执行历史中的命令
	- !!
!n

- ~

	- home目录

- #

	- 注释

- -

	- 上一次工作目录

- :

	- 真值，空命令

- /

	- 目录分隔符

## Linux系统信息

### uptime

- 系统运行时长和平均负载

### w

- 当前登录系统的用户信息

	- 子主题 1

### who

- 显示当前登录系统的用户信息

### whoami

### last

- 显示用户最近登录的信息

	- last -n 10

### uname

- 打印当前系统信息

	- uname -a

### data

- 显示或设置系统时间与如期

### cal

- 显示日历

### df

- 监测磁盘空间

### du

- 监测文件、目录和子目录的磁盘使用情况

###  fdsk

- fdisk -l
- 查看系统分区信息	

### free

- 显示空闲内存数量

### linux目录

- / 虚拟目录的根目录。通常不会在这里存储文件
/bin 二进制目录,存放许多用户级的GNU工具
/boot 启动目录,存放启动文件
/dev 设备目录,Linux在这里创建设备节点
/etc 系统配置文件目录
/home 主目录,Linux在这里创建用户目录
/lib 库目录,存放系统和应用程序的库文件
/media 媒体目录,可移动媒体设备的常用挂载点
/mnt 挂载目录,另一个可移动媒体设备的常用挂载点
/opt 可选目录,常用于存放第三方软件包和数据文件
/proc 进程目录,存放现有硬件及当前进程的相关信息
/root root用户的主目录
/sbin 系统二进制目录,存放许多GNU管理员级工具
/run 运行目录,存放系统运作时的运行时数据
/srv 服务目录,存放本地服务的相关文件
/sys 系统目录,存放系统硬件信息的相关文件
/tmp 临时目录,可以在该目录中创建和删除临时工作文件
/usr 用户二进制目录,大量用户级的GNU工具和数据文件都存储在这里
/var 可变目录,用以存放经常变化的文件,比如日志文件

## 文件目录

### 相对路径

### 绝对路径

### 远程路径

- 协议://用户名:密码@位置/路径:端口

### 文件类型

- regular file 普通文件
d diretcoty 目录
l link 链接
b block 块设备 存取数据以供以系统存取的接口设备即硬盘
c character 字符设备 串口设备键盘鼠标...
s socket 套接字
p pipe 管道

- - d l b c s p

### 链接文件

- 符号链接

	- 符号链接就是一个实实在在的文件,它指向存放在虚拟目录结构中某个地方的另一个文件。
这两个通过符号链接在一起的文件,彼此的内容并不相同。
可以使目录或文件，可不再同一磁盘
	- ln -s file/dir symbolic_link

		- 查看inode编号 ls -i

- 硬链接

	- 硬链接会创建独立的虚拟文件,其中包含了原始文件的信息及位置。但是它们从根本上而言是同一个文件。
引用硬链接文件等同于引用了源文件。要创建硬链接,原始文件也必须事先存在
是文件，在同一磁盘
	- ln file hard_link

### 文件权限

- chmod #更改文件权限

	- chmod a+x file #给file文件的ugo都赋予执行权限
	- chmod o-x file #给file文件o减去执行权限
	- chmod 755 file #设置file文件的权限为rwxr-xr-x
	- chmod u=rwx,go=rx file #设置file文件的权限为rwxr-xr

- chown #更改文件所属用户

	- chown yzw:wei file #修改file的所属用户是yzw，所属组为wei
	- chown -R yzw:wie directory #修改目录directory及目录下的所有文件ug
	- chown yzw file #修改file的所属用户为yzw

- chgrp #更改文件所属组

	- chgrp root fiel #修改file所属组为root

### pwd

- [-LP]

	- -L:逻辑工作目录;   链接类似于快捷方式
-P:物理工作目录;    找到真正目录

### cd

cd 切换到home
cd - 更切换到先前的工作目录。
cd ~user_name 更改工作目录到用户家目录

- . .. - ~username

### env

- 打印环境变量

### mkdir

- [pm] <dir>

	- -p 自动创建父目录
-m 设置权限

### rmdir

- [p]

### ls

-a 	--all 列出所有文件,包括隐藏文件。
-d 	--directory通常,列出这个目录中的内容,而不是目录本身。与-l 结合,可看到所指定目录的详细信息,而不是目录中的内容。
-h	不是以字节数来显示文件的大小，以长格式显示结果。
-l	以长格式显示结果。
-r	--reverse以相反的顺序来显示结果。通常,ls 命令的输出结果
按照字母升序排列。
-S 命令输出结果按照文件大小来排序。
-t 按照修改时间来排序。

- [adhlrSti]

	- -d <file> 显示目录本身,而非内容
-F       在每个名字后加上指示符，用以区分目录和文件，若是目录，则加‘/’
-h       以长格式列出时，以人们可读格式输出，例如文件大小不能以字节数显示
-l       以长格式显示结果
-r       以相反的顺序来显示结果,默认按照字母升序排列
-S       输出结果以文件大小来排序
-t       按照修改时间排序

- ls -Fr
- ls -alf

### cp

- [irapdslu] <sour> <des>

	- -i 若文件存在，询问用户
-r 递归复制
-a pdr的集合
-p  连同文件属性cp
-d 若源文件为连接文件的属性，则复制连接文件的属性
-u 原文件比目的文件新才cp

### rm

- [irf]

	- -f force
	- -f一般指 format、file、force

### mv

- [ifu] <source...> <dest>

	- -i  重写已有文件之前，提示用户确认信息
-u 只更新目标文件或文件夹中没有的内容
-v 显示详实操作信息

- 可用于重命名

### 用于文件路径和名称的获取
不需要参数文件真实存在

- dirname

	- dirname /test/123/456
/test/123

- basename

	- basename /test/123/456
456

### file

### less

G 移动到最后一行
1G or g 移动到开头一行

- G g /string n h q
- - /string 向下查找;  n : 继续向下
- /?string 反向查找;  N: 继续反向

### more

- /string 向下查找string关键字
:f  显示文件名称和当前显示的行数
q 离开

### cat

- [-AbEbTv]

	- -A 相当于-vET
-v 列出看不出的字符，类似于vim可视模式； vim中 `:set list`
-E 显示断行符为$
-T 显示TAB为^I
-b 显示行号，不包括空行
-n  连同空行列出行号

### tac

### nl

- [-bnw] 

	- -b a :相当于 cat -n
-b t :相当于 cat -b
-n ln，rn，rz :屏幕最左，字段最右，字段最右显示同时前面自动补全0
-w \<num>  :行号所占位数

### tail

- [-n num]

	- -n num : 显示文件后num行
-n -num :除去前num行，都显示

### head

- [-n num] 

	- -n num : 显示文件前num行
-n -num :除去后num行，都显示

### od

- [ab]

	- 程序以字节序列存储
	- od -b test.c
	- od -a test.c

### touch

-  [-acdmt]

	- -a:仅修改访问时间 

- 主要用于修改时间,
一般就是创建空白文件.

### 文件隐藏属性

- chattr

	- [ +-= ] [ ASacdistu ]

		- - A : 不修改atime, 节省磁盘，避免忙碌
- S : 同步写入。写入磁盘，再返回；程序到磁盘中间有 缓冲写（内核写入磁盘），超过块(4k)再写入；--> 数据库，保证数据一致性。
- a : append(追加),只能增加数据； --> 适合用于日志，防止删除
- c : 自动压缩,解压 --> 主要用于备份系统中
- d: 不会被dump程序备份
- i : 不能删除、修改、建立连接 --> 若删除，先删除权限
- s : 文件删除时, 直接从磁盘删除  --> 用于敏感数据
- u : 文件删除时, 数据内容存在磁盘中 --> 默认，很高效

- lsattr

	-  [-adR] 

		- -a : 打印隐藏文件的隐藏属性
-d : 如果是目录，仅打印目录的信息
-R ：递归

## 文件查询

### --time

- -mtime

	-  modify    默认，内容数据改动时才更新

- - ctime

	- change   文件的权限， 属性改动时更新

- - atime

	- access    文件的内容被取用access时，更新

- ls -l --time=ctime  

### which

- 查找PATH路径下所有的可执行文件

### whereis

- [-bmsu]

	- -b ：只查找二进制文件
-m ：之查找manual路径下的文件
-s ： 只查找source源文件
-u ： 查找其他文件

- 寻找特定文件

### locate

-  [-ir]

	- -i ：忽略大小写
-r ：后面可接正则表达式

- 相关文件： /etc/updatedb.conf   和  /var/lib/mlocate
updatedb： 更新数据库，索引更新

### find

-  [PATH] [option] [action]
- 与时间相关 
-atime
-ctime
-mtime

	- -mtime n ： n天前的"一天之内"修改的文件
-mtime +n ：n天前，不包含n，修改过的文件 
-mtime -n ：n天之内，包含n，修改过的文件
-newer file ：比file还要新的文件

- 与用户或用户组相关

	- -uid n ：用户UID为n
-gid n ： 群组GID为n
-user name ：用户名为name
-group name ：群组名为name
nouser ： 文件所有者不存在
nogroup ：文件所在组不存在

- 与文件权限及名称相关

	- -name filename ：文件名为filename
-size [+-] SIZE ：查找比SIZE大或小的
-type TYPE ：f b c d l s p
-perm mode ：mode 刚好等于的文件
-perm -mode ：全部包含mode的文件 查找指定权限的文件

- 执行命令

	- -ok
	- -exec

		-  find -exec ls -l {} \;

- 实例

	-  find ~ -mtime -3 -type f -user yanzhiwei -size -1024 -name "*.c" -perm -644 2>/dev/null -exec ls -l {} \;
# -exec执行， {}用于替换替换内容，\; 转义：需要; 而不是顺序执行
	- $ find ~ -mtime -3 -type f -user yanzhiwei -size -1024 -name "*.c" -perm -644 2>/dev/null | xargs ls -al
    #xargs   转换参数， stdin获取转到参数

## 数据提取

### cut

- [-dfc]

	- -d c

		- 以c字符分割

	- -f num

		- 显示num字段的内容 [n-; n-m; -m]

	- -b num

		- 字节

	- -c num

		- 字符

### sort

- [-fbMnrtuk]

	- -b

		- 默认整行排序，忽略开头空格

	- -f

		- 排序不区分大小写

	- -n

		- 基于数字值排序

	- -r

		- 按相反顺序排序

	- -k

		- 对从field1到fiel2之间的字符排序

	- -M

		- 以月份名称排序

	- -o

		- 把排好序的输出结果发送到文件

	- -t

		- 定义域分隔符，默认情况下为空格或制表符

	- -u

		- 删除重复行

- sort -t '/' -k 7 file

	- 以斜线为分割符号，且按照第七个字段来排序

- sort -k 3.7nbr -k 3.1nbr -k 3.4nbr file

	- 起始于第三个字段的第七个字符,到第三个字段的末尾结束；另外还指定了第三个字段的第一个和第四个字符做反向数值排序

### uniq

- uniq只会删除相邻的重复行
- [ic]

	- -c

		- 输出所有的重复行，每行开头显示重数

	- -d

		- 只输出重复行，而不是特有的文本行

	- -f n

		- 忽略每行开头的n个字段，字段由空格隔开

	- -i

		- 比较文本行时忽略大小写

	- -s n

		- 跳过每行开头的n个字符

	- -n

		- 只输出独有的文本行

### tr

- [cdst]

	- -d

		- 表示删除特定字符

- tr -d '\r' < old-file > new-file

	- 将old-file中的换行符\r删掉，将转换的内容保存到新文件new-file

- tr [:lower:] A

### wc

- [-lwn]

	- -l

		- 仅列出行号

	- -w

		- 仅列出多字节

	- -m

		- 仅列出多少字符

### tee

- -a

	- append

- 双向重导项
- ll | tee file

### xargs

- [-0pne]

	- -0

		- 讲特殊字符还原为普通字符

	- -p

		- 执行指令前询问

	- -n num

		- 每次执行cmd命令所需参数

### split

- [-bl]

	- -b SIZE

		- 切分为SIZE大小的文件

	- -l num

		- 以num行为大小切分

### regx

- 基本匹配字符

	-  . 匹配任意单个字符，不能匹配空行
	-   [] 匹配指定范围内的任意单个字符
	-   [^] 取反
	-   [:alnum:] 或 [0-9a-zA-Z]
	-   [:alpha:] 或 [a-zA-Z]
	-   [:upper:] 或 [A-Z]
	-   [:lower:] 或 [a-z]
	-   [:blank:] 空白字符（空格和制表符）
	-   [:space:] 水平和垂直的空白字符（比[:blank:]包含的范围广）
	-   [:cntrl:] 不可打印的控制字符（退格、删除、警铃...）
	-   [:digit:] 十进制数字 或[0-9]
	-   [:xdigit:]十六进制数字
	-   [:graph:] 可打印的非空白字符
	-   [:print:] 可打印字符
	-   [:punct:] 标点符号

- 配置次数

	- *  匹配前面的字符任意次，包括0次，贪婪模式：尽可能长的匹配
	-  .*  任意长度的任意字符，不包括0次
	-  \?  匹配其前面的字符0 或 1次
	-  \+  匹配其前面的字符至少1次
	-  \{n\}  匹配前面的字符n次
	-  \{m,n\}  匹配前面的字符至少m 次，至多n次
	-  \{,n\}  匹配前面的字符至多n次
	-  \{n,\}  匹配前面的字符至少n次

- 位置锚定

	-  ^  行首锚定，用于模式的最左侧
	-  $  行尾锚定，用于模式的最右侧
	-  ^PATTERN$，用于模式匹配整行
	-  ^$ 空行
	-  ^[[:space:]].*$  空白行
	-  \< 或 \b  词首锚定，用于单词模式的左侧
	-  \> 或 \b  词尾锚定；用于单词模式的右侧
	-  \<PATTERN\>

- 分组和后向引用

	- ① 分组

		- \(\) 将一个或多个字符捆绑在一起，当作一个整体进行处理
		- 分组括号中的模式匹配到的内容会被正则表达式引擎记录于内部的变量中，这些变量的命名方式为: \1, \2, \3, ...

	- ② 后向引用

		- 引用前面的分组括号中的模式所匹配字符，而非模式本身
		- \1 表示从左侧起第一个左括号以及与之匹配右括号之间的模式所匹配到的字符
		- \2 表示从左侧起第2个左括号以及与之匹配右括号之间的模式所匹配到的字符，以此类推
		- \& 表示前面的分组中所有字符

	- ③ 流程分析如下

		- gerp "\(H.\{4\}\) world \1" reg
   整个正则第1个分组     引用第1个分组中的正则匹配结果

### 扩展正则

- 除了\<, \b : 语首、\>, \b : 语尾；
使用其他正则都可以去掉\；
- 字符匹配

	-  .  任意单个字符
	-  []  指定范围的字符
	-  [^] 不在指定范围的字符
	-    次数匹配：
	-  * ：匹配前面字符任意次
	-  ?  : 0 或1次
	-  + ：1 次或多次
	-  {m} ：匹配m次 次
	-  {m,n} ：至少m ，至多n次

- 位置锚定

	-  ^ : 行首
	-  $ : 行尾
	-  \<, \b : 语首
	-  \>, \b : 语尾
	-    分组：()
	-  后向引用：\1, \2, ...

### 三剑客

- grep    '字符'             文件
sed     '命令'              文件
awk    '条件{命令}'     文件
单引号内就是正则表达式的用法

### grep

- grep [options] regex [file...]

	- -i

		- 忽略大小写

	- -v

		- 打印不匹配的项，即取反

	- -c

		- 打印匹配数量，而不是文本行本身

	- -l

		- 打印包含匹配项的文本名

	- -L

		- 打印不包含匹配项的文本名

	- -n

		- 在每个匹配行之前打印出其位于文件中的相应行号

	- -h

		- 应用于多文件搜索，不输出文件名

- 实例

	- grep   'Ty\{2,3\}'    file_name

		- 找到Tyy,Tyyy的所有行；(注意{}在 shell中有特殊含义，故需要转义)

	- grep   '^The'   file_name 

		- 以The开头的所有行

	- grep    'g*g'     file_name

		- 找到g , gg , ggg等的所有
(*代表重复前一个字符0～～无穷多次）

### sed

- sed [-nefri] '[地址定界] command' file(s)

	-  -n：不输出模式空间内容到屏幕，即不自动打印，只打印匹配到的行

		- sed -n "/aaa/p" demo  #-n不显示没匹配的行

	-  -e：多点编辑，对每行处理时，可以有多个Script

		- sed -e "s/a/A/" -e "s/b/B/" demo  #-e多点编辑

	-  -f：把Script写到文件当中，在执行sed时-f 指定文件路径，如果是多个Script，换行写

		-  sed -f sedscript.txt demo

	-  -r：支持扩展的正则表达式
	-  -i：直接将处理的结果写入文件
	-  -i.bak：在将处理的结果写入文件之前备份一份

- 地址定界

	- 不给地址：对全文进行处理
	-  单地址：

		-  #: 指定的行
		-  /pattern/：被此处模式所能够匹配到的每一行

	-  地址范围：

		-  #,#

			- sed -n "1,2p" demo  #打印1-2行

		-  #,+#
		-  /pat1/,/pat2/
		-  #,/pat1/

	-  ~：步进

		-   sed -n '1~2p'  只打印奇数行 （1~2 从第1行，一次加2行）

			-  sed "1~2s/[aA]/E/g" demo  #将奇数行的a或A替换为E

		-   sed -n '2~2p'  只打印偶数行

- command

	- d：删除模式空间匹配的行，并立即启用下一轮循环

		-  sed "2d" demo  #删除第2行
		- sed '/^$/d;G' #删除空行
		- sed '/^$/d' data1.txt #删除空行

	-  p：打印当前模式空间内容，追加到默认输出之后

		- sed -n "2p" demo  #打印第2行

	-  a：在指定行后面追加文本，支持使用\n实现多行追加

		- sed "2a123" demo  #在第2行后加123

	-  i：在行前面插入文本，支持使用\n实现多行追加

		- sed "1i123" demo  #在第1行前加123

	-  c：替换行为单行或多行文本，支持使用\n实现多行追加

		- sed "3c123\n456" demo  #替换第3行内容

	-  w：保存模式匹配的行至指定文件

		- sed -n "3w/root/demo3" demo  #保存第3行的内容到demo3文件中

	-  r：读取指定文件的文本至模式空间中匹配到的行后

		- sed -n "=" demo  #=打印行号

	-  =：为模式空间中的行打印行号

		- sed -n "=" demo  #=打印行号

	-  !：模式空间中匹配行取反处理

		- sed -n '2!p' demo  #打印除了第2行的内容

	-  s///：查找替换，支持使用其它分隔符，如：s@@@，s###；

		- 加g表示行内全局替换；
		- sed 's@[a-z]@\u&@g' demo  #将全文的小写字母替换为大写字母
		- .sed  -i  's/a\[t\]\./p_temp->/g' file_name
 把file_name文件中的a[t]. 全部替换p_temp-> 
(-i 会直接将修改写入文件，[ ] 和 . 是特殊符号，需要用\来转义一下)
		- sed 's!/bin/bash!/bin/csh!' /etc/passwd
感叹号被用作字符串分隔符

### awk

- 用法

	- awk [options] 'program' var=value file…

		-  -v var=value：赋值一个用户定义变量，将外部变量传递给awk

	- awk [options] -f programfile var=value file…

		-  -f scripfile：从脚本文件中读取awk命令

	- awk [options] 'BEGIN{ action;… } pattern{ action;… } END{ action;… }' file ...

		- -F fs：fs指定输入分隔符，fs可以是字符串或正则表达式，如-F:
		- BEGIN{}:  仅在开始处理文件中的文本之前执行一次
		- END{} ：仅在文本处理完成之后执行

- 变量

	- 内置和自定义变量，每个变量前加 -v 命令选项
	-  FS ：输入字段分隔符，默认为空白字符
	-  OFS ：输出字段分隔符，默认为空白字符

		-  awk -v FS=':' -v OFS='---' '{print $1,$2}' awkdemo  #OFS指定输出分隔符

	-  NF ：字段数量，共有多少字段， $NF引用最后一列，$(NF-1)引用倒数第2列

		- awk -F: '{print $(NF-1)}' awkdemo  #显示倒数第2列

	-  NR ：行号，后可跟多个文件，第二个文件行号继续从第一个文件最后行号开始

		- awk END'{print NR}' awkdemo awkdemo1

	-  FNR ：各文件分别计数, 行号，后跟一个文件和NR一样，跟多个文件，第二个文件行号从1开始

		-  awk '{print FNR}' awkdemo awkdemo1

	-  FILENAME ：当前文件名
	-  ARGC ：命令行参数的个数
	-  ARGV ：数组，保存的是命令行所给定的各参数，查看参数

		- awk 'BEGIN {print ARGV[0]}' awkdemo awkdemo1

- printf

	- -：左对齐（默认右对齐） %-15s

		- awk -F: '{printf "%-20s---%-10.3f\n",$1,$3}' /etc/passwd

	-  +：显示数值的正负符号 %+d

- 操作符

	-  算术操作符

		-  x+y, x-y, x*y, x/y, x^y, x%y
		-  -x:  转换为负数
		-  +x:  转换为数值

	-  赋值操作符

		-  =, +=, -=, *=, /=, %=, ^=
		-  ++, --

	- 比较操作符

		- ==, !=, >, >=, <, <=

	- 模式匹配符

		- ~ ：左边是否和右边匹配包含 !~ ：是否不匹配

			- df -h |awk -F: '$0 ~ /^\/dev/'---
查询以/dev开头的磁盘信息

	- 逻辑操作符

		- 与&& ，或|| ，非!

	- 函数调用

		-  function_name(argu1, argu2, ...)

	- 条件表达式

		- selector?true-exp: false-exp

- 高阶用法

	- if(condition1){statement1}else if(condition2){statement2}else{statement3}  多分支

		- 对awk 取得的整行或某个字段做条件判断

	- while(condition){statement;…}

		- 对一行内的多个字段逐一类似处理时使用
		- 对数组中的各元素逐一处理时使用
		-  awk 'BEGIN{i=1;sum=0;while(i<=100){sum+=i;i++};print sum}'
#计算1+2+3+...+100=5050

	- do {statement;…}while(condition)
	- for(expr1;expr2;expr3) {statement;…}

		- for(var in array) {for-body}

			- 特殊用法：遍历数组中的元素

		- awk -F: '{for(i=1;i<=NF;i++) {print$i,length($i)}}' awkdemo
# 显示每一行的每个单词和其长度

	- switch(expression) {case VALUE1 or /REGEXP/:statement1; case VALUE2 or /REGEXP2/: statement2;...; default: statementn}

		- break
		- continue
		- next：提前结束对本行处理而直接进入下一行处理（awk 自身循环）

			-  awk -F: '{if(NR%2!=0) next; print $1,$3}' /etc/passwd
#只打印偶数行

	- array[index-expression] #数组

		- 可使用任意字符串；字符串要使用双引号括起来
		- 如果某数组元素事先不存在，在引用时，awk 会自动创建此元素，并将其值初始化为“空串”
		- awk '{!arr[$0]++;print $0,arr[$0]}' awkdemo2
#打印文件内容，和该行重复第几次出现
		- awk '!arr[$0]++' awkdemo2 #-去除重复的行

	- 数值处理

		- rand()：返回0和1之间一个随机数，需有个种子 srand()，没有种子，一直输出0.237788

			-  awk 'BEGIN{srand(); print int(rand()*100%50)+1}'

		- length([s]) ：返回指定字符串的长度

	- awk自定义函数

		- function name ( parameter, parameter, ... ) {
    statements
    return expression
}

			- 和bash区别：定义函数（）中需加参数，return返回值不是$?，是相当于echo输出
			- # cat fun.awk
function max(v1,v2) {
    v1>v2?var=v1:var=v2
    return var
}
BEGIN{a=3;b=2;print max(a,b)}
[root@along ~]
# awk -f fun.awk
3

	-  awk中调用shell 命令

		- system 命令

			- 空格是awk 中的字符串连接符，如果system中需要使用awk中的变量可以使用空格分隔，或者说除了awk 的变量外其他一律用"" 引用 起来。
			-  awk 'BEGIN{score=100; system("echo your score is " score) }'
#your score is 100

		- awk 脚本

			- [root@along ~]# cat f1.awk
{if($3>=1000)print $1,$3}
[root@along ~]# cat f2.awk
#!/bin/awk -f
{if($3 >= 1000)print $1,$3}
[root@along ~]# chmod +x f2.awk
[root@along ~]# ./f2.awk -F: /etc/passwd
along 1000
			- 传参
[root@along ~]# cat test.awk
#!/bin/awk -f
{if($3 >=min && $3<=max)print $1,$3}
[root@along ~]# chmod +x test.awk
[root@along ~]# ./test.awk -F: min=100 max=200 /etc/passwd
systemd-network 192

## shell脚本编程

### 解释

- 脚本：写入一个过程(若干命令)，自动执行
- 解释型语言，编译型语言

### #! 表示下面的代码应用什么来解释
必须在文件的第一行指定要使用的shel

- #!/bin/bash
echo "Hello world"

### 变量

- 没有空格,无需声明

	- - a=12
	- - a=helloworld
	- - a='pwd'     先执行``
	- - a=$a:a        路径,:拼接在一起

- 局部变量

	- local a=12 局部
	- ​	readonly a 只读

- 特殊变量

	- 位置变量

		- $0 : 获取当前执行shell脚本的文件名，包括路径；程序本身
		- $n : $1,  $[10]
		- $* :获取当前shell全部参数 `"$1$2$3$4"`
		- $#:    获取参数个数   
#有求长度求数量的意思
		- $@:获取这个程序所有参数，保留空白，
"$1" "$2" "$3"`可用于传给其他程序

	- 状态变量

		- $? :判断上一指令是否成功，0成功，非0失败
		- $$ : 获取当前进程的pid
		- $! : 上一个指令的pid

### echo

- echo -e 开启转义\n换行  
- echo 转义符\"

### 函数

- function _fun_ () {
	echo   #返回值
	return #状态值
}

	- function factorial {
if [ $1 -eq 1 ]
then
echo 1
else
local temp=$[ $1 - 1 ]
local result='factorial $temp'
echo $[ $result * $1 ]
fi
}

### 流程控制

- if else

	- if [[ condition ]]; then
elif [[ condition]]; then
else 
fi
	- 双括号[[ condition ]]
使用高级数学表达

		- val++ 后增
		- val-- 后减
		- ++val 先增
		- --val 先减
		- ! 逻辑求反
		- ~ 位求反
		- ** 幂运算
		- << 左位移
		- >> 右位移
		- & 位布尔和
		- | 位布尔或
		- && 逻辑和
		- || 逻辑或

	- 双方括号[[ expression ]]
针对字符串比较

		- 提供模式匹配(pattern matching)
		- if [[ $USER == r* ]]
then
echo "Hello $USER"
else
echo "Sorry, I do not know you"
fi

			- 双等号将右边的字符串( r* )视为一个模式,
并应用模式匹配规则。

- while

	- while [[ condition ]]; do
done 

- for

	- for i in words; do
done

		- for test in Nevada "New Hampshire" "New Mexico" "New York"
do
echo "Now going to $test"
done

	- for (( i=1; i<=j; i++ )); do
done

- until

	- until [[ condition ]]; do
done

- case

	- case word in
	pattern )
	;;
	* )
	;;
esac

		- case $USER in
rich | barbara)
echo "Welcome, $USER"
echo "Please enjoy your visit";;
testing)
echo "Special testing account";;
jessica)
echo "Do not forget to log off when you're done";;
*)
echo "Sorry, you are not allowed here";;
esac

- read

	- 从标准输入(键盘)或另一个文件描述符中接受输入

- exec
- 更改字段分隔符

	- 特殊的环境变量 IFS ,叫作内部字段分隔符

		- file="states"
IFS=$'\n'
for state in $(cat $file)
do
echo "Visit beautiful $state"
done
		- IFS=$'\n':;"

			- 这个赋值会将换行符、冒号、分号和双引号作为字段分隔符

	- FS.OLD=$IFS
IFS=$'\n'
<在代码中使用新的IFS值>
IFS=$IFS.OLD
这就保证了在脚本的后续操作中使用的是 IFS 的默认值。

- 控制循环

	- break 命令
	- continue 命令

### 比较

- man test ，[]等同于 test 表达式，
 [[ condition ]]  ,  不要用[]， 注意空格
- 数值比较
bash shell只能处理整数

	- -eq
	- -ge
	- -gt
	- -le
	- -lt
	- -ne

- 字符串比较

	- =
	- !=
	- <
	- >
	- -n str1

		- 检查 str1 的长度是否非0

	- -z str1

		- 检查 str1 的长度是否为0

	- 字符串顺序

		- 大于号和小于号必须转义,
否则shell会把它们当作重定向符号,
把字符串值当作文件名

			- if [ $val1 \> $val2 ]

		- 大于和小于顺序和 sort 命令所采用的不同。

			- 在比较测试中,大写字母被认为是小于小写字母的
			- 比较测试中使用的是标准的ASCII顺序

- 文件比较

	- -d file 检查 file 是否存在并是一个目录
	- -e file 检查 file 是否存在
	- -f file 检查 file 是否存在并是一个文件
	- -r file 检查 file 是否存在并可读
	- -s file 检查 file 是否存在并非空

		- if [ -f $file_name ]
then
if [ -s $file_name ]
then

	- -w file 检查 file 是否存在并可写
	- -x file 检查 file 是否存在并可执行
	- -O file 检查 file 是否存在并属当前用户所有
	- -G file 检查 file 是否存在并且默认组与当前用户相同
	- file1 -nt file2 检查 file1 是否比 file2 新
	- file1 -ot file2 检查 file1 是否比 file2 旧

### 计算

- $[ $val + 5 ]
- `echo "scale=小数点位数; 表达式" | bc`

### 数组

- 定义

	- declare -a arr
	- arr[subscript]=value
	- arr=(val1 val2 val3...)

- 操作

	- ${arry[*]}
${arry[@]}
输出数组内容
	- ${#arry[@]}
确定数组元素个数
	- ${!arry[@]}
数组下标
	- array+=(a,b,c) 追加
	- sort 排序
	- unset 删除数组和元素

## vim使用技巧

### ggVG+y  全选复制

- 或这Ctrl+C  复制到系统剪贴板

### :set nu   vim打开命令模式，显示行号

### :set paste   设置粘贴

### :set list   显示隐藏字符

## 网络

### ssh

- ssh 用户名@公网    39.97.167.241	
连接远程主机

### sshfs 远程服务器挂载

- sudo sshfs -o nonempty,allow_other,exec yanzhiwei@aliyun:/ /mnt/tecmint

### umount

- 卸载挂载

### 应用

- nautilus 文件资源器

### 免密登录

- 1. sudo vim /etc /hosts		修改hosts文件

	- 公网 aliyun
	-  将公钥拷贝到云主机

- 2. ssh-keygen  生成秘钥对
- 3. ssh-copy-id yzw@aliyun
- 4. ssh 检查

### ping 网络ip

- ping:发送包接受包，检测主机是否正常

### scp 目录文件 yanzhiwie@公网ip:. 

- 上传文件到云主机;
下载同

### sftp

### netstat - 打印网络连接,路由表,接口统计数据,伪装连接,和多路广播成员

- -ie

	- 查看网络接口

- netstat -alntu

	- -t tcp
	- -u udp

### ftp - 因特网文件传输程序

### wget - 非交互式网络下载器

## 压缩

### tar

- -c: 建立压缩档案

	- tar -cf all.tar *.jpg

		- 这条命令是将所有.jpg的文件打成一个名为all.tar的包

- -x：解压

	- tar -xf all.tar

		- 这条命令是解出all.tar包中所有文件

- -t：查看内容

	- ar -tf all.tar

		- 这条命令是列出all.tar包中所有文件

- -r：向压缩归档文件末尾追加文件

	- tar -rf all.tar *.gif

		- 这条命令是将所有.gif的文件增加到all.tar的包里面去

- -u：更新原压缩包中的文件

	- ar -uf all.tar logo.gif

		- 这条命令是更新原来tar包all.tar中logo.gif文件

- -z：有gzip属性的
- -j：有bz2属性的
- -Z：有compress属性的

	- tar -cZf jpg.tar.Z *.jpg  //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

- -v：显示所有过程
- -O：将文件解开到标准输出

### rar a jpg.rar *.jpg 

- unrar e
- rar格式的压缩

### zip jpg.zip *.jpg

- unzip
- zip格式的压缩

## 软件包管理

### dpkg

- dpkg --list  

	- 列出安装的所有软件包

- dpkg --status package_name

	- 查看是否安装了某个软件

- dpkg --install package_file

	-   从软件包安装软件

### apt-get

- sudo apt-get install name  

	- 从网上资源库安装名为name的软件

- sudo apt-get update;sudo apt-get upgrade

	- 更新软件

- sudo apt-get remove package_name

	- 卸载软件

### aptitude

- 解决依赖问题

## 其他

### type

- 查看命令类型

### exit

- 结束终端

### clear

- 清屏

### history 

- 显示历史列表

### shutdown

- 关机或者重启系统

### seq

### 键盘

- Ctrl+a

	- 移动光标到行首

- Ctrl+e

	- 移动光标到行尾

- 幕后控制台

	- Ctrl+Alt+F1,2,3..6

- Tab

	- 自动补全

- Alt+?

	- 显示可能的自动补全列表，也可以按两次Tab键来实现

- Alt+*

	- 插入所有可能的自动补全

- ctrl+s

	- 终止屏幕输出（即停止回显），你敲的依然有效，只是看不见

- ctrl+q

	- 恢复屏幕输出

### asciinema play   播放演示

### curl ifconfig.me 当前外网ip公网地址
curl cip.cc

### 查看Linux的内网IP地址
命令：ifconfig -a

*XMind - Trial Version*