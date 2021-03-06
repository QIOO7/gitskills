# Linux命令行笔记

* 本篇以Ubuntu为例，刚安装的Linux系统软件包管理源是国外的源，这就使得Linux的下载速度很慢，为此需要换源，在此推荐清华跟中科大的源(前者快后者全)

## 常用命令行

* Linux命令的格式：`命令 [选项] [参数]`，`命令`这一部分是必须的，是否用选项和参数取决于使用该命令实现的具体目的；选项是以`-`来指明的；命令、选项、参数之间以空格隔开，1个或多个空格都视为1个空格；完成Linux命令输入后，按下回车键即可执行该命令

1. `sudo apt-get update`：查看更新，`sudo`表示使用管理员权限，`apt-get`是Ubuntu用的，在别的Linux系统用的是别的
2. `sudo apt-get upgrade`：更新系统
3. `sudo apt-get install 安装包`：下载安装
4. `nano 文件名`：用文本编辑器打开该文件，文件不存在则创建文件并打开
5. `pwd`：显示当前所在的目录，在终端上执行pwd实际上是去执行了/bin/pwd
6. `ls 路径名`：显示路径目录下的文件，没有路径名默认当前路径(ls即list)；`ls -a`：显示路径目录下的文件，包括隐藏文件(a即all)；`-l`显示目录下文件的更详细的信息(文件权限、文件最后修改时间、文件大小)(l即long)；`-h`将文件大小以K(KB)、M(MB)、G(GB)来表示(h即human-able)；`-n`：显示当前工作目录下包含的文件属性
7. `cd 路径名`：切换路径；`cd ~`：切换到当前用户的家目录；`cd .`：切换到当前路径；`cd ..`：切换到上一级路径；`cd ../..`：切换到上上级路径(在linux中路径分隔符为斜杠/)；`cd -`：切换到上一次的路径
8. `mkdir 目录名`：新建目录；`-p`连续创建多级目录(父目录和子目录)，如果父目录不存在，则需要加入`-p`参数(p即parents)
9.  `mv 旧文件名 新文件名`：修改文件名；`mv 旧目录名 新目录名`：修改目录名；`mv 文件名 目录名`：移动路径(mv即move)
10. `rmdir 目录名`：删除目录，但不能删除非空目录
11. `touch 文件名`: 新建文件，同一目录无法创建同名文件，文件名区分大小写
12. `cp 源文件名 目标文件名`：将当前目标文件拷贝成源文件；`cp 源文件名 目标目录名`：将当前目录下的源文件拷贝到目标目录下；`cp 源目录名 目标目录名`：复制源目录下的文件到目标目录下(cp即copy)；`-r`递归复制指定目录下的子目录和文件(r即recursive递归查找,个人理解递归查找就是查找目标目录路径下的所有文件)
13. `rm 文件名`：删除文件或目录，删除前最好先确定该文件或目录是否可以被删除；`-i`删除文件或目录之前，询问是否同意删除(i即interactive交互)；`-r`递归删除指定目录下的子目录和文件；`-f`强制删除(f即force强制)
14. `cat 文件名`：将文件内容显示到终端中，可以敲入多个文件；`-n`显示内容并在内容前显示行号
15. `clear`：刷新屏幕，保留历史命令操作记录，本质上只是让终端向后翻一页，当向上滚动鼠标时，还是可以看到之前命令的操作记录
16. `reset`：重新初始化屏幕，清除历史命令操作记录
17. `man 页数 命令`：查看man手册中该命令指定页数的说明，不输入页数默认为首页，例：`man man`：查看man手册的说明
18. `info 命令`：查看该命令的使用说明
19. `命令 --help`：查看该命令的使用说明

## 进阶命令行

1. `systemctl status`：显示系统状态
2. `find 目录名 选项 查找条件`：查找符合条件的文件(如果没有指定查找目录，则为当前目录)，如`find . -mtime -2`，查找当前目录下两天内有变动的文件，如`find -name "*.txt"`，查找当前目录下的txt文件，`*`是通配符
3. `grep 选项 要查找的字符串 目标文件名`：查找文件中符合条件的字符串，默认已经显示目标文件名，`-n`显示目标位置的行号(n即number)；`-r`递归查找；`-w`则全字匹配(全字匹配是只有在遇到与要找的词完全匹配的完整的词，才提示找到字串)，目标文件名为`*`则表示查找当前目录下的所有文件和目录
4. `file 文件名`：识别文件类型
5. `which 命令名/应用程序名`：查找命令或应用程序的所在位置；`whereis 命令名/应用程序名`：查找可执行程序的位置和手册页的位置

## 压缩解压命令行

* `gzip`：不加任何选项为压缩单个文件，压缩完该文件会生成后缀为`.gz`的压缩文件，相同的文件内容，如果文件名不同，压缩后的大小也不同
  
1. `gzip -l 压缩文件名`：列出压缩文件的内容(l即list)
2. `gzip -kd  以.gz结尾的单个压缩文件名`：解压同时保留输入文件(k即keep，d即decompress解压缩)
3. 特殊情况：`man pwd`会解压`/usr/share/man/man1/pwd.1.gz`这个文件，然后读取该文件中固定的格式的一些信息，然后显示到终端中。

* `bzip2`：不加任何选项为压缩单个文件，压缩完该文件会生成后缀为`.bz2`的压缩文件，并删除原有的文件，所以推荐使用`bzip2 -k`压缩源文件，选项同`gzip`

* `gzip`、`bizp2`只能对一个文件进行压缩，而不能对多个文件和目录进行压缩，一般情况下，小文件使用`gzip`来压缩，大文件使用`bzip2`来压缩

* `tar`：对多个目录、文件进行打包和压缩

1. `tar -czvf 压缩文件名 目录名`：使用`gzip`方式压缩，`tar -czvf`与`tar czvf`是一样的效果，`c`表示创建用来生成文件包(c即create)；`z`表示使用`gzip`方式进行处理，与`c`结合就表示压缩，与`x`结合就表示解压缩；`v`详细报告tar处理的信息(v即verbose)；`f`表示文件，后面接着一个文件名(f即file)
2. `tar cjvf 压缩文件名 目录名`：使用`bzip2`方式压缩，`j`表示使用`bzip2`方式进行处理，与`c`结合就表示压缩，与`x`结合就表示解压缩
3. `tar xzvf 压缩文件名 -C 指定目录`：使用`gzip`方式解压到指定目录，没用`C`指定目录则为当前目录，`x`表示从文件包中提取文件
4. `tar xjvf 压缩文件名 -C 指定目录`：使用`bzip2`方式解压到指定目录，没用`C`指定目录则为当前目录
5. `tar tvf 压缩文件名`：查看，`t`表示查看压缩的文件

## vi编辑器一般模式下的快捷键

* `vi 文件名`：打开文件、新建文件

1. `:w`：保存文件；`:q`：退出文件；`:wq`：保存并退出；`:q!`：强制退出，但不会保存被修改的内容
2. 移动光标方向键：`h`：左；`j`：下；`k`：上；`l`：右
3. `i`：在光标前开始插入文本；`a`：在光标后开始插入文本；`o`：在当前行之下新开一行，并到行首
4. `ngg`：光标移至第n行的行首(n为数字)；`G`：定位最后一行行首
5. `0`：光标移至当前行行首；`$`：光标移至当前行行末；`fx`：搜索当前行中下一个出现字母x的地方
6. `yy`：复制当前行(y即yank复制)；`nyy`：当前行及其后的n-1行
7. `dd`：删除光标所在行(d即delete)；`ndd`：删除当前行及其后的n-1行
8. `x`：删除光标所在位置的字符；
9. `u`：销上一步操作；
10. `p`：粘贴到光标下一行(p即paste)；`P`：粘贴到光标上一行
11. `..`：重复前一个操作
12. `/字符串`：从光标开始处向文件尾搜索字符串，而后再输入`n`：同一个方向重复上次搜索命令(n即next)；而后再输入`N`：反方向重复上次搜索命令
13. `:%s/字符串1/字符串2/g`：将文件中所有的字符串1均用字符串2替换，而后按`y`表示确定，按`n`表示取消；`:%s/字符串1/字符串2/gc`：确定将文件中所有的字符串1均用字符串2替换(s即substitute替换，g即global全局的，c即confirm确认)

## gcc的使用方法

* `gcc [选项] 文件名`，输入文件的后缀名和选项共同决定gcc到底执行那些操作，常用选项：`-v`：查看gcc编译器的版本，显示gcc执行时的详细过程；`-o 文件名` 指定输出文件名为file，这个名称不能跟源文件名同名；`-E` 只预处理，不会编译、汇编、链接；`-S` 只编译，不会汇编、链接；`-c` 编译和汇编，不会链接

1. `gcc .c文件名`输出一个`.out文件`，然后可以使用`./.out文件名`命令来执行该应用程序
2. `gcc -o 可执行程序文件名 .c文件名`：输出可执行程序文件，然后可以使用`./可执行程序文件名`命令来执行该应用程序
3. `gcc -E -o .i文件名 .c同名文件`
4. `gcc -S -o .s文件名 .i同名文件`
5. `gcc -c -o .o文件名 .s后同名文件`：gcc会对`.c文件`默认进行预处理操作，`-c`再来指明了编译、汇编，从而得到`.o文件`
6. `gcc -o 可执行程序文件名 .o文件名`：将`.o文件`进行链接，得到可执行应用程序(链接就是将汇编生成的OBJ文件、系统库的OBJ文件、库文件链接起来，
最终生成可以在特定平台运行的可执行程序)