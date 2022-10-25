#                 作业 9.12
计科 1903 张枭 201906062629

2.2 date：显示当前时间日期
Wed Oct  5 14:32:36 CST 2022
cd:change directory
cp:把一个文件复制到另一个地方
pwd：现在所处的文件夹
rm：删除
mkdir：创建direcotry
echo：显示字符
who：显示当前登录用户
ls：显示当前文件夹下文件
cat：显示文件内容
more：用于在命令提示符下查看文本文件，如果文件很大，一次显示一屏
man：显示manul

2.3 date -j -f '%m-%d-%Y' "01-01-2049" +'%A'
>Friday

2.5 
![[Screen Shot 2022-10-06 at 14.11.41.png]]

2.7说出下列每项信息各对应哪一类文件：

1.  1.drwxr-xr-x   目录文件
2.  2./bin  链接文件
3.  3./etc/passwd  普通文件
4.  4.Brw-rw-rw-  设备文件
5.  5./dev/fd0    字符设备文件
6.  6./usr/lib    目录文件
7.  7.-rwx--x--x   普通文件

2.9  请给出下列命令执行的结果：
cd 回到用户主目录
cd .. 上级目录
cd ../.. 上级目录的上级目录
cd / 回到主目录

2.10 cp ,copy与 mv命令的异同？

相当于复制与剪贴的区别。
Cp,copy命令把文件源文件内容复制给目标文件后，源文件仍然存在。
mv命令将文件从一个目录移到另一个目录中，该文件就从原目录中消失，文件个数不变。
不能直接用copy作为复制文件的命令。因为Linux系统提供的众多命令都是有一定规则和限制的，cp是copy的缩写，是Linux默认的复制文件的命令，而copy并不是Linux的合法命令。
  
2.11 用什么命令能把两个文件合并成一个文件？
（1） cat file1.txt file2.txt > file.txt  file1 file2合并到file中，会覆盖原有内容。
（2）cat file1.txt >> file2.txt  追加到文件的末尾

2.15 目录ABC下有两个子目录a1,b2以及5个普通文件。如果想彻底删除ABC目录，应该使用什么目录。
(1) Rm -rf ABC  
(2) 如果5个普通文件在a1,b2之下，则可以使用一下命令：
cd ABC/a1
   Rm *
   Cd ../b2
   Rm *
   Cd ../..
Rmdir -p ABC
(3)如果5个普通文件不全在a1,b2之下，则使用一下命令：
Cd ABC
Rm -r *
Cd..
Rmdir ABC

2.16如何用一个命令行统计给定目录中有多少个子目录？![[Screen Shot 2022-10-06 at 14.19.59.png]]

2.17类似DOS下的dir,del,type命令的Linux命令各是什么？
Ls   rm   cat