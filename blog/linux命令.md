### Linux 介绍

#### Linux的基本原则：

1、由目的单一的小程序组成；组合小程序完成复杂任务；
2、一切皆文件；
3、尽量避免捕获用户接口；
4、配置文件保存为纯文本格式；

#### 命令提示符

	命令提示符，prompt, bash(shell)
		#: root
		$: 普通用户
	命令：

#### 命令格式：

	命令  选项  参数
		选项：
			短选项： -
				多个选项可以组合：-a -b = -ab
			长选项： --
		参数：命令的作用对象

### 基础常用命令

#### ls

	-l：长格式
		文件类型：
			-：普通文件 (f)
			d: 目录文件
			b: 块设备文件 (block)
			c: 字符设备文件 (character)
			l: 符号链接文件(symbolic link file)
			p: 命令管道文件(pipe)
			s: 套接字文件(socket)
		文件权限：9位，每3位一组，3组 权限（U,G,O）每一组：rwx(读，写，执行), r-- ，第一组：文件的属主用户权限。第二组：文件的属组用户权限，第三组：其他用户权限
		文件硬链接的次数
		文件的属主(owner)
		文件的属组(group)
		文件大小(size)，单位是字节
		时间戳(timestamp)：最近一次被修改的时间
			访问:access
			修改:modify，文件内容发生了改变
			改变:change，metadata，元数据
	-h：做单位转换
	-a: 显示以.开头的隐藏文件
		. 表示当前目录
		.. 表示父目录
	-A
	-d: 显示目录自身属性
	-i: index node, inode
	-r: 逆序显示
	-R: 递归(recursive)显示

#### cd: change directory

	家目录，主目录, home directory
	cd ~USERNAME: 进入指定用户的家目录
	cd -:在当前目录和前一次所在的目录之间来回切换

#### 命令类型：

	内置命令(shell内置)，内部，内建
	外部命令：在文件系统的某个路径下有一个与命令名称相应的可执行文件
	type: 显示指定属于哪种类型

#### date：时间管理

#### hwclock

	硬件时钟
	系统时钟

#### 获得命令的使用帮助

* 内部命令：

 help COMMAND 比如：help cd
* 外部命令：

COMMAND --help 比如：date --help

命令手册：manual

man COMMAND

whatis COMMAND

分章节：

1：用户命令(/bin, /usr/bin, /usr/local/bin)

2：系统调用

3：库用户

4：特殊文件(设备文件)

5：文件格式(配置文件的语法)

6：游戏

7：杂项(Miscellaneous)

8: 管理命令(/sbin, /usr/sbin, /usr/local/sbin)

MAN：
	NAME：命令名称及功能简要说明
	SYNOPSIS：用法说明，包括可用的选项
	DESCRIPTION：命令功能的详尽说明，可能包括每一个选项的意义
	OPTIONS：说明每一个选项的意义
	FILES：此命令相关的配置文件
	BUGS：
	EXAMPLES：使用示例
	SEE ALSO：另外参照

翻屏：
	向后翻一屏：SPACE
	向前翻一屏：b
	向后翻一行：ENTER
	向前翻一行：k

查找：
/KEYWORD: 向后
n: 下一个
N：前一个 

q: 退出

练习：
	使用date单独获取系统当前的年份、月份、日、小时、分钟、秒

hwclock
	-w: 将硬件时间修改为系统时间
	-s: 将系统时间修改为硬件时间


#### echo

如何显示 echo “The year is 2013."  echo "Today is 26.”为两行？

echo -e jflasdfksdfl\\\nfnlsdf

### 文件系统：

rootfs: 根文件系统 /

FHS：Linux

/boot: 系统启动相关的文件，如内核、initrd，以及grub(bootloader)
/dev: 设备文件

设备文件：

​	块设备：随机访问，数据块
​	字符设备：线性访问，按字符为单位
​	设备号：主设备号（major）和次设备号（minor）

/etc：配置文件
/home：用户的家目录，每一个用户的家目录通常默认为/home/USERNAME
/root：管理员的家目录；
/lib：库文件

​	静态库,  .a
​	动态库， .dll, .so (shared object)
​	/lib/modules：内核模块文件

/lib64

/media：挂载点目录，移动设备

/mnt：挂载点目录，额外的临时文件系统

/opt：可选目录，第三方程序的安装目录

/proc：伪文件系统，内核映射文件,如果删除，系统重新启动会重新初始化

/sys：伪文件系统，跟硬件设备相关的属性映射文件,如果删除，系统重新启动会重新初始化

/tmp：临时文件, /var/tmp

/var：可变化的文件

/bin: 可执行文件, 用户命令

/sbin：管理命令

/usr：应用程序的安装目录

绝对路径：以跟目录为起点到目标的路径。
相对路径：以当前目录为起点到目标的路径

#### 查找文件命令 find

find pass*
在当前目录下查找以 pass 开头的文件
find /etc/pass*
在/etc 目录中查找以 pass 开头的文件
find /etc/pass* -print 在/etc 目录中查找以 pass 开头的文件,并显示出来

#### 在文件内容中查找关键字 grep

grep “rpm” /etc/passwd 在/etc/passwd 文件中查找关键字 rpm

#### mkdir：创建空目录

-p:创建多级目录
-v: verbose

/root/x/y/z

/mnt/test/x/m,y
mkdir -pv /mnt/test/x/m /mnt/test/y
mkdir -pv /mnt/test/{x/m,y}


####tree：查看目录树

删除目录：rmdir (remove directory)
	-p删除空目录
​	

文件创建和删除
#### touch

	-a
	-m
	-t
	-c
	如果文件已经存在，touch将会修改文件的时间信息。
#### stat 查看文件信息

创建文件，可以使用文件编辑器

#### nano：小型文件编辑器

vi(另外一个文件)

删除文件：rm

```
-i  删除之前确认

-f  删除之前不确认

-r  递归删除

rm filename  (rm -r  删除文件夹     rm -rf 强制删除文件或文件夹)

rm -rf /  linux自杀
```



#### cp： copy

cp SRC DEST

```
-r

-i 存在覆盖前确认

-f

-p

-a：归档复制，常用于备份
```


cp file1 file2 file3
一个文件到一个文件
多个文件到一个目录
cp /etc/{passwd,inittab,rc.d/rc.sysinit} /tmp/

#### mv: move

移动文件，重命名文件

mv SRC DEST
mv -t DEST SRC

#### 目录管理：

ls、cd、pwd、mkdir、rmdir、tree

#### 文件管理：

touch、stat、file、rm、cp、mv、nano,vi,vim

#### 日期时间：

date、clock、hwclock、cal ,ntpdate

ntpdate -u ip：使得本地时间的互联网上的某台服务器的时间保持同步。

#### 查看文本：

cat：查看整个文件

tac：从后往前查看整个文件

more，less：分屏显示。less可以实现一行一行进行翻页。

head - num、tail - num：只看文件的前几行或者后几行。

#### 分屏显示：

more、less

* more: 向后翻
* less: 

head:查看前n行 

tail:查看后n行

-n 

tail -f: 查看文件尾部，不退出，等待显示后续追加至此文件的新内容；

#### vi

```###
一般模式下命令：
i：光标之前插入
a：光标之后插入
o：换行插入

I：本行最前插入
A：本行最后插入
O：向上换行

vi +7:直接编辑第五行
vi +:直接在最后一行进行编辑
vi +/path :直接在第一个path出现的地方进行编辑，进入后按n键可以寻找写一个path位置

h，j，k，l：光标移动的左下上右

以单词进行移动：
	w：移至下一个单词的词首
	e：移至下一个单词的词尾
	b：移至当前单词或者前一个单词的词首

行内切换：
	0：绝对行首
	^：行首的第一个非空白字符
	$:绝对行尾
	
行间切换：
	G:跳转到最后一行
	gg：跳转到第一行

删除：d
	x：删除光标所在处字符
	nx：删除光标所在处的n个字符
	dd：删除一行
	dG：删除光标所在行到末尾行的所有内容
	D：删除光标所在处到行末的所有内容
撤销：
	u：撤销
	ctr + r :向前撤销
r：替换光标所在处的内容
R:替换光标所在处一直到行末的内容依次替换
shift + zz（大写的ZZ）:保存并退出快捷键
v：进入字符可视化模式
V：进入行可视化模式
ctr+v进入块可视化模式

底行模式命令：
	.：表示当前行
	$:表示最后一行
	+#：向下的#行
	set nu :显示行号
	set nonu:取消行号
	数字：跳转到第几行
	n1,n2d：删除n1到n2的行内容

复制：
	y：和d用法相同
粘贴：
	p
	
查找：
	/输入要查找的内容，使用n查找写一个
	？输入要查找的内容，使用n查找上一个

查找并替换：末行使用s命令
	add1,add2s@path@String@gi
	add1,add2:标识查找范围的行号
	path:查找的内容
	String：将要替换的内容
	g：全局查找
	i：忽略大小写

和shell进行交互
	在低行模式下：！命令：就可以执行shell命令。!mkdir aa
	
配置文件位置：
etc/vimrc
etc/virc
```

### 文本处理，对字符串进行处理

#### 字符串切割cut:

	-d: 指定字段分隔符，默认是空格
	-f: 指定要显示的字段
		-f 1,3：第一个和第三个
		-f 1-3：第一个到第三个
	echo "a b c d e e" | cut -d ' ' -f1 :获取切割后的第一个字符串。

#### 文本排序：sort

	-n：数值排序
	-r: 降序
	-t: 字段分隔符
	-k: 以哪个字段为关键字进行排序
	-u: 排序后相同的行只显示一次
	-f: 排序时忽略字符大小写

#### 文本统计：wc (word count)

	-l：统计行数
	-w：统计单词的数量 
	-c：统计字节的数量
	-m:统计字符的数量
	-L：打印最长的一行
#### sed基本用法：

sed: Stream EDitor。将文本从文件中取出，处理后打印到控制台，并不会修改文件中的内容

	行编辑器 (全屏编辑器: vi)

sed: 模式空间
默认不编辑原文件，仅对模式空间中的数据做处理；而后，处理结束后，将模式空间打印至屏幕；


sed [options] 'AddressCommand' file ...：分别对应：选项，命令，文件
	-n: 静默模式，不再默认显示模式空间中的内容
	-i: 直接修改原文件
	-e SCRIPT -e SCRIPT:可以同时执行多个脚本
	-f /PATH/TO/SED_SCRIPT
		sed -f /path/to/scripts  file
	-r: 表示使用扩展正则表达式


Command：
	d: 删除符合条件的行；
	p: 显示符合条件的行；
	a \string: 在指定的行后面追加新行，内容为string
		\n：可以用于换行
	i \string: 在指定的行前面添加新行，内容为string
	r FILE: 将指定的文件的内容添加至符合条件的行处
	w FILE: 将地址指定的范围内的行另存至指定的文件中; 
	s/pattern/string/修饰符: 查找并替换，默认只替换每行中第一次被模式匹配到的字符串
		加修饰符
		g: 全局替换
		i: 忽略字符大小写
	s///: s###, s@@@	
		\(\), \1, \2
		
	l..e: like-->liker
		  love-->lover
		  
		  like-->Like
		  love-->Love
	
	&: 引用模式匹配整个串
	
	举例：
	1、删除/etc/grub.conf文件中行首的空白符；
	sed -r 's@^[[:space:]]+@@g' /etc/grub.conf
	
	2、替换/etc/inittab文件中"id:3:initdefault:"一行中的数字为5；
	sed 's@(id:)[0-9](:initdefault:)@\15\2@g' /etc/inittab
	
	3、删除/etc/inittab文件中的空白行；
	sed '/^$/d' /etc/inittab

#### awk:

	awk是一个强大的文本分析工具，
	相对于grep的查找，sed的编辑，
	awk在其对数据分析并生成报告时，显得尤为强大。
	简单来说awk就是把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。


awk '{pattern + action}' {commands}
	其中 pattern 表示 AWK 在数据中查找的内容，而 action 是在找到匹配内容时所执行的一系列命令。
	花括号（{}）不需要在程序中始终出现，但它们用于根据特定的模式对一系列指令进行分组。
	pattern就是要表示的正则表达式，用斜杠括起来。	

案例：

* 显示最近登录的5个帐号

last -n 5 | awk  '{print $1}'
读入有'\n'换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域
$0则表示所有域,$1表示第一个域,$n表示第n个域。默认域分隔符是"空白键" 或 "[tab]键",
所以$1表示登录用户，$3表示登录用户ip,以此类推。

last -n 5 | awk -F ,  '{print $1}'：指定“,”为分隔符

* 如果只是显示/etc/passwd的账户

cat /etc/passwd |awk  -F ':'  '{print $1}'  
root
daemon
bin
sys
这种是awk+action的示例，每行都会执行action{print $1}。

-F指定域分隔符为':'。

 

* 如果只是显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以tab键分割

  cat /etc/passwd |awk  -F ':'  '{print \$2\$7}'

  cat /etc/passwd |awk  -F ':'  '{print "用户名"\$2"    shell"\$7}'root    /bin/bash
  daemon  /bin/sh
  bin     /bin/sh
  sys     /bin/sh


  如果只是显示/etc/passwd的账户和账户对应的shell,而账户与shell之间以逗号分割,而且在所有行添加列名name,shell,在最后一行添加"blue,/bin/nosh"。

* 复制代码

  cat /etc/passwd |awk  -F ':'  'BEGIN {print "name,shell"}  {print $1","​$7} END {print "blue,/bin/nosh"}'
  name,shell
  root,/bin/bash
  daemon,/bin/sh
  bin,/bin/sh
  sys,/bin/sh
  ....
  blue,/bin/nosh

  awk工作流程是这样的：先执行BEGING，然后读取文件，读入有/n换行符分割的一条记录，然后将记录按指定的域分隔符划分域，填充域，\$0则表示所有域,\$1表示第一个域,\$n表示第n个域,随后开始执行模式所对应的动作action。接着开始读入第二条记录······直到所有的记录都读完，最后执行END操作。



* 搜索/etc/passwd有root关键字的所有行

  awk -F: '/root/' /etc/passwd

  root:x:0:0:root:/root:/bin/bash

  这种是pattern的使用示例，匹配了pattern(这里是root)的行才会执行action(没有指定action，默认输出每行的内容)。

  搜索支持正则，例如找root开头的: awk -F: '/^root/' /etc/passwd


* 搜索/etc/passwd有root关键字的所有行，并显示对应的shell
  awk -F: '/root/{print $7}' /etc/passwd

  搜索/etc/passwd以root关键字开始的所有行，并显示对应的shell             

  awk -F: '/root/{^print $7}' /etc/passwd

  搜索/etc/passwd以root关键字结尾的所有行，并显示对应的shell          

  awk -F: '/root$/{print $7}' /etc/passwd

* awk内置变量


    awk有许多内置变量用来设置环境信息，这些变量可以被改变，下面给出了最常用的一些变量。

    ARGC               命令行参数个数
    ARGV               命令行参数排列
    ENVIRON            支持队列中系统环境变量的使用
    FILENAME           awk浏览的文件名
    FNR                浏览文件的记录数
    FS                 设置输入域分隔符，等价于命令行 -F选项
    NF                 浏览记录的域的个数
    NR                 已读的记录数(常用)
    OFS                输出域分隔符
    ORS                输出记录分隔符
    RS                 控制记录分隔符
    
    \$0变量是指整条记录。\$1表示当前行的第一个域,$2表示当前行的第二个域,......以此类推。

* 统计/etc/passwd:文件名，每行的行号，每行的列数，对应的完整行内容:
  awk  -F ':'  '{print "filename:" FILENAME ",linenumber:" NR ",columns:" NF ",linecontent:"$0}' /etc/passwd
  filename:/etc/passwd,linenumber:1,columns:7,linecontent:root:x:0:0:root:/root:/bin/bash
  filename:/etc/passwd,linenumber:2,columns:7,linecontent:daemon:x:1:1:daemon:/usr/sbin:/bin/sh
  filename:/etc/passwd,linenumber:3,columns:7,linecontent:bin:x:2:2:bin:/bin:/bin/sh
  filename:/etc/passwd,linenumber:4,columns:7,linecontent:sys:x:3:3:sys:/dev:/bin/sh

* 使用printf替代print,可以让代码更加简洁，易读

  awk  -F ':'  '{printf("filename:%s,linenumber:%s,columns:%s,linecontent:%s\n",FILENAME,NR,NF,$0)}' /etc/passwd


  print和printf
  awk中同时提供了print和printf两种打印输出的函数。

  其中print函数的参数可以是变量、数值或者字符串。字符串必须用双引号引用，参数用逗号分隔。如果没有逗号，参数就串联在一起而无法区分。这里，逗号的作用与输出文件的分隔符的作用是一样的，只是后者是空格而已。

  printf函数，其用法和c语言中printf基本相似,可以格式化字符串,输出复杂时，printf更加好用，代码更易懂。

 

* awk编程

  变量和赋值

  除了awk的内置变量，awk还可以自定义变量。

  下面统计/etc/passwd的账户人数

  awk '{count++;print $0;} END{print "user count is ", count}' /etc/passwd
  root:x:0:0:root:/root:/bin/bash
  ......
  user count is  40
  count是自定义变量。之前的action{}里都是只有一个print,其实print只是一个语句，而action{}可以有多个语句，以;号隔开。

  这里没有初始化count，虽然默认是0，但是妥当的做法还是初始化为0:

  awk 'BEGIN {count=0;print "[start]user count is ", count} {count=count+1;print $0;} END{print "[end]user count is ", count}' /etc/passwd
  [start]user count is  0
  root:x:0:0:root:/root:/bin/bash
  ...
  [end]user count is  40

* 统计某个文件夹下的文件占用的字节数

  ls -l |awk 'BEGIN {size=0;} {size=size+$5;} END{print "[end]size is ", size}'
  [end]size is  8657198


  如果以M为单位显示:

  ls -l |awk 'BEGIN {size=0;} {size=size+$5;} END{print "[end]size is ", size/1024/1024,"M"}' 
  [end]size is  8.25889 M
  注意，统计不包括文件夹的子目录。

 

* 条件语句

 awk中的条件语句是从C语言中借鉴来的，见如下声明方式：

* 复制代码

    if (expression) {
    statement;
    statement;
    ... ...
    }
```
if (expression) {
    statement;
} else {
    statement2;
}
```

```
if (expression) {
    statement1;
} else if (expression1) {
    statement2;
} else {
    statement3;
}
```

* 统计某个文件夹下的文件占用的字节数,过滤4096大小的文件(一般都是文件夹):

  ls -l |awk 'BEGIN {size=0;print "[start]size is ", size} {if($5!=4096){size=size+$5;}} END{print "[end]size is ", size/1024/1024,"M"}' 
  [end]size is  8.22339 M

* 循环语句

  awk中的循环语句同样借鉴于C语言，支持while、do/while、for、break、continue，这些关键字的语义和C语言中的语义完全相同。


* 数组

    因为awk中数组的下标可以是数字和字母，数组的下标通常被称为关键字(key)。值和关键字都存储在内部的一张针对key/value应用hash的表格里。由于hash不是顺序存储，因此在显示数组内容时会发现，它们并不是按照你预料的顺序显示出来的。数组和变量一样，都是在使用时自动创建的，awk也同样会自动判断其存储的是数字还是字符串。一般而言，awk中的数组用来从记录中收集信息，可以用于计算总和、统计单词以及跟踪模板被匹配的次数等等。


* 显示/etc/passwd的账户

  awk -F ':' 'BEGIN {count=0;} {name[count] = $1;count++;}; END{for (i = 0; i < NR; i++) print i, name[i]}' /etc/passwd
  0 root
  1 daemon
  2 bin
  3 sys
  4 sync
  5 games
  ......

  这里使用for循环遍历数组

* linux 引号


    1、反引号：``  ,命令替换
    2、单引号：''   ，字符串
    3、双引号: ""  ,变量替换

* 管道：前一个命令的输出，作为后一个命令的输入

 命令1 | 命令2 | 命令3 | ...

 统计/usr/bin/目录下的文件个数；
 ls /usr/bin | wc -l

 判断 /home/goldin目录是否有文件

 取出当前系统上所有用户的shell，要求，每种shell只显示一次，并且按顺序进行显示；
 cut -d: -f7 /etc/passwd | sort -u
 取出/etc/inittab文件的第6行；
 head -6 /etc/inittab | tail -1
 取出/etc/passwd文件中倒数第9个用户的用户名和shell，显示到屏幕上并将其保存至/tmp/users文件中；
 tail -9 /etc/passwd | head -1 | cut -d: -f1,7 | tee /tmp/users
 显示/etc目录下所有以pa开头的文件，并统计其个数；
 ls -d /etc/pa* | wc -l

### 用户管理

用户管理：

	useradd, userdel, usermod, passwd, chsh, chfn, finger, id, chage

组管理：
	groupadd, groupdel, groupmod, gpasswd

权限管理：
	chown, chgrp, chmod, umask
/etc/passwd:
用户名：密码：UID:GID：注释：家目录：默认SHELL

/etc/group:
组名：密码：GID:以此组为其附加组的用户列表

/etc/shadow：
用户名：密码：最近一次修改密码的时间：最短使用期限：最长使用期限：警告时间：非活动时间：过期时间：

#### 用户管理：

	useradd, userdel, usermod, passwd, chsh, chfn, finger, id, chage
* useradd  [options]  USERNAME 

 -u UID
 -g GID（基本组）
 -G GID,...  （附加组）
 -c "COMMENT"
 -d /path/to/directory
 -s SHELL
 -m -k
 -M
 -r: 添加系统用户

 ​

* userdel:

userdel [option] USERNAME

	-r: 同时删除用户的家目录

id：查看用户的帐号属性信息
	-u
	-g
	-G
	-n

finger: 查看用户帐号信息
finger USERNAME

* 修改用户帐号属性：

  usermod

  -u UID 
  -g GID
  -a -G GID：不使用-a选项，会覆盖此前的附加组；
  -c
  -d -m：
  -s
  -l
  -L：锁定帐号
  -U：解锁帐号

* chsh: 修改用户的默认shell

* chfn：修改注释信息

* 密码管理：

  passwd [USERNAME]

  --stdin
  -l
  -u
  -d: 删除用户密码

* pwck：检查用户帐号完整性

#### 组管理：

* 创建组:groupadd

groupadd 

	-g GID
	-r：添加为系统组

* groupmod

 -g GID
 -n GRPNAME

* groupdel

* gpasswd：为组设定密码

  newgrp GRPNAME <--> exit	

* chage

 -d: 最近一次的修改时间
 -E: 过期时间
 -I：非活动时间
 -m: 最短使用期限
 -M: 最长使用期限
 -W: 警告时间

* 权限管理：

  r: 
  w：
  x：
  111 101 101
  三类用户：
  u: 属主
  g: 属组
  o: 其它用户

  chown: 改变文件属主(只有管理员可以使用此命令)

  chown USERNAME file,...

  -R: 修改目录及其内部文件的属主
  --reference=/path/to/somefile file,...

chown USERNAME:GRPNAME file,..

chown USERNAME.GRPNAME file,...

chgrp GRPNAME file,...

	-R
	--reference=/path/to/somefile file,...

* chmod: 修改文件的权限

  修改三类用户的权限：
  chmod MODE file,...

  -R
  --reference=/path/to/somefile file,...

rwxr-x---

ps -aux

netstat -ntpl

grep
find

yum install lrzsz  上传文件rz 

-linux 安全性

* 登陆

 等日志查看
 限制某些IP才能ssh登陆
 ...
 密码一个月换一次
 设置密码：特殊符号，大写，小写，1223455，最少8位

* 防火墙

 规则
 添加规则
 配置文件
### 常见系统管理(凡是涉及到修改，就一定要用root权限)

轻易不要使用su去切换到root的身份
普通用户使用sudo来执行root权限的命令
如，将hadoop用户添加到sudoers文件中去
root    ALL=(ALL)       ALL
hadoop  ALL=(ALL)       ALL

#### 磁盘空间信息查看

df -h  查看磁盘空间状态信息
du -sh * 查看当前目录下所有子目录和文件的汇总大小    

#### 进程信息查看 

free  查看内存使用状况
top   查看实时刷新的系统进程信息，当前系统中消耗资源最多的进程

ps -ef  查看系统中当前瞬间的进程信息快照

jps 查看java程序端口

ps -ef | grep myshell.sh  搜索myshell进程的信息
kill -9 pid  杀掉进程  （-9 表示强制杀死）

### 文件归档压缩(1：打包--归档； 2：压缩)

1、归档
tar -cvf testdir.tar testdir/
2、压缩
gzip testdir.tar  

gzip -d :解压

gzip  file
bzip2  file 

tar -czvf  testdir.tar.gz testdir/
tar -xzvf testdir.tar.gz  解压到当前目录下
tar -zxvf testdir.tar.gz -C Downloads/   解压到指定的Downloads目录下


zip test.zip testdir

### 网络管理

修改ip地址的配置
sudo vi /etc/sysconfig/network-scripts/ifcfg-eth0 修改该配置文件即可改ip地址
或者在root权限下用setup指令通过一个带提示的伪图形界面来修改

显示网络状态信息
	netstat 
	-a 显示所有链接和监听端口
	-t 显示tcp相关选项
	-u 显示udp相关选项
	-n 拒绝显示别名 ， 能显示数字的尽量显示数字
	-p 显示建立相关链接的程序名

查看ip地址
ifconfig


修改主机名
sudo vi  /etc/sysconfig/network  修改其中的hostname配置项
要想立即生效  可以执行指令  hostname nidezhujiming 

HOSTNAME=yun12-01

管理内网的"主机名---ip地址"本地映射
sudo vi /etc/hosts
192.168.2.250  yun12-01


重启网络服务
查看防火墙的状态：service iptables status
root权限下   service network restart 
关闭防火墙服务  service iptables stop
关闭防火墙自动启动(开机时不开启防火墙)   chkconfig iptables off

修改系统的默认启动级别
vi /etc/inittab

   0 - halt (Do NOT set initdefault to this)
   1 - Single user mode
   2 - Multiuser, without NFS (The same as 3, if you do not have networking)
   3 - Full multiuser mode
   4 - unused
   5 - X11
   6 - reboot (Do NOT set initdefault to this)

id:3:initdefault:
~
用level 3 就启动全功能状态的字符界面 

查看当前的进程连接网络的信息
netstat -nltp   

### 常用工具指令

wc   统计文本信息（行数，词数，字符数）

date  查看或者修改系统的日期和时间

echo  输出字符串或者变量的值

### linux中的软件安装 

jdk
将安装包解压到你的安装路径下
然后修改环境变量  sudo vi /etc/profile
然后  source /etc/profile  来生效
tomcat
Eclipse


mysql
redhat 公司的RPM方式的包管理 也是很常用的软件包管理器

rpm -qa | grep mysql
sudo rpm -e mysql-libs-5.1.66-2.el6_3.i686 --nodeps
sudo rpm -ivh MySQL-server-5.1.73-1.glibc23.i386.rpm 

export TOMCAT_HOME=/home/bxp/software/tomcat

export JAVA_HOME=/usr/lib/jvm/java-8-oracle

export PATH=\$JAVA_HOME/bin:\$PATH

export CLASSPATH=.:\$JAVA_HOME/lib/dt.jar:\$JAVA_HOME/lib/tools.jar

### 配置文件：

保存用户信息的文件：/etc/passwd
保存密码的文件：/etc/shadow
保存用户组的文件：/etc/group
保存用户组密码的文件：/etc/gshadow
用户配置文件：/etc/default/useradd

