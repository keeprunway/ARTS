# ARTS

## 1. Algorithm

> 项目地址：[sailfish-leetcode/AddTwoNumbers.java at master · Sailfishc/sailfish-leetcode · GitHub](https://github.com/Sailfishc/sailfish-leetcode/blob/master/src/main/java/AddTwoNumbers.java)

```
*/***
* * 整个链表yinggaishi*
* * 0 -> node1 -> node2 -> node3*
* * 然后返回的链表元素从第二个元素开始*
* ****@param***l1*
* ****@param***l2*
* ****@return**
**/*
public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    // 创建一个哑结点
    ListNode headNode = new ListNode(0);
    ListNode p = l1, q = l2, cur = headNode;
    int carry = 0;
    // 如果p或者q其中有一个不为空，那么就执行
    while (p != null || q != null) {
        // 如果其中有一个链表的元素为null了，那么赋值为0
        int x = (p != null ? p.val : 0);
        int y = (q != null ? q.val : 0);
        int sum = x + y + carry;
        // 表示进位
        carry = sum / 10;
        cur.next = new ListNode(sum % 10);
        cur = cur.next;
        if (p != null) {
            p = p.next;
        }
        if (q != null) {
            q = q.next;
        }
    }
    if (carry > 0) {
        cur.next = new ListNode(carry);
    }
    return headNode.next;
}
```

## 2. Review

- 原文地址：[the best programming language - Coding Geek](http://coding-geek.com/the-best-programming-language/)

> 最好的语言需要一些情形

- 是否需要性能
- 生态系统如何
- 社区如何，出现问题是否容易解决
- 团队的技能是什么
- 商业选择

> 最后结论：A programming language is just a tool; what matters is the way you overcome your problems
> 程序语言仅仅是工具，重要的是解决你的问题

## 3. T：技术技巧

> List：
> 3.1. Linux 文件名rename操作
> 3.2. perl 正则的相关知识

### 3.1.Linux 文件名rename操作

想要批量修改文件打后缀名，比如*.txt想改为*.c.
``` shell
rename 's/\.txt/.c' ./*
```
- Man rename
```
RENAME(1p)            User Contributed Perl Documentation           RENAME(1p)
NAME
       rename - renames multiple files
SYNOPSIS
       rename [ -h|-m|-V ] [ -v ] [ -n ] [ -f ] [ -e|-E perlexpr]*|perlexpr
       [ files ]
DESCRIPTION
       "rename" renames the filenames supplied according to the rule specified
       as the first argument.  The perlexpr argument is a Perl expression
       which is expected to modify the $_ string in Perl for at least some of
       the filenames specified.  If a given filename is not modified by the
       expression, it will not be renamed.  If no filenames are given on the
       command line, filenames will be read via standard input.
       For example, to rename all files matching "*.bak" to strip the
       extension, you might say
               rename 's/\e.bak$//' *.bak
       To translate uppercase names to lower, you'd use
               rename 'y/A-Z/a-z/' *
OPTIONS
       -v, -verbose
               Verbose: print names of files successfully renamed.
       -n, -nono
               No action: print names of files to be renamed, but don't
               rename.
       -f, -force
               Over write: allow existing files to be over-written.
       -h, -help
               Help: print SYNOPSIS and OPTIONS.
       -m, -man
               Manual: print manual page.
       -V, -version
               Version: show version number.
       -e      Expression: code to act on files name.
               May be repeated to build up code (like "perl -e").  If no -e,
               the first argument is used as code.
       -E      Statement: code to act on files name, as -e but terminated by
               ';'.
```
> 特别注意到man中的描述指出perlexpr。表示该rename匹配模式是perl实现的，满足perl的正则表达
- Example：
```
# 替换空格
rename  's/[ ]+/_/g'   *
rename  's/[[:space:]]+/_/g'   *
# 统一在文件头部添加上hello 
rename  's/^/hello/'    *
# 统一把.html扩展名修改为.htm
rename  's/.html$/.htm/'     *
统一在尾部追加.zip后缀：
rename  's/$/.zip/'   *
统一去掉.zip后缀：
rename  's/.zip$//'   *

#规则化数字编号名，比如1.jpg, 2.jpg ..... 100.jpg , 现在要使文件名全部三位即1.jpg .... 001.jpg
#运行两次命令：
rename  's/^/00/'  [0-9].jpg     # 这一步把1.jpg ..... 9.jpg 变幻为001.jpg .... 009.jpg
rename  's/^/0/'  [0-9][0-9].jpg   # 这一步把10.jpg ..... 99.jpg 变幻为010.jpg ..... 090.jpg
```
 参考: [linux rename 正则表达式](https://www.jianshu.com/p/e11eaeb32653); [linux下rename用法--批量重命名](https://www.2cto.com/os/201201/117383.html)
 
### 3.2. perl 正则的相关知识
Perl正则表达式,常用形式
- 匹配：`m/<regexp>/` (可以省略m，直接写成`/regexp/`)
- 替换：`s/<pattern>/<replacement>/`
- 转化：`tr/<pattern>/<replacement>/`

转换跟替换不同，替换是将replacement整个字符串替换pattern字符串，而转换则是用replacement逐个字符替换pattern逐个字符，结果依赖于replacement与pattern字符个数

#### 3.2.1替换
替换表达方式如下，还有一系列参数，貌似不怎么用得着。
`s/PATTERN/REPLACEMENT/egimosx`
`egimosx`操作修饰符号

#### 3.2.2转化
转化有两种等价表达方式，如下：
`tr/SEARCHLIST/REPLACEMENTLIST/cds` `y/SEARCHLIST/REPLACEMENTLIST/cds`
> `cds`操作修饰符号,分别代表转化所有未指定字符/删除所有指定字符/把多个相同的输出字符缩成一个

转化同替换不同，用REPLACEMENTLIST逐个字符替换SEARCHLIST逐个字符，比如'tr/Sam/Stm/'，用S替代S，t替代a，m替代m。结果依赖于两者字符长短，下面以文件名FastSpiSam3C.nc为例进行说明：
``` shell
jelline@jelline:~$ rename -n 'tr/Sam3/Stm/' FastSpiSam3C.nc　/*替换字符短，用最后一个字符m替换3*/
 FastSpiSam3C.nc renamed as FtstSpiStmmC.nc 
jelline@jelline:~$ rename -n 'tr/Sam3/Stm32/' FastSpiSam3C.nc /*替换字符长，多出字符被忽略*/ 
FastSpiSam3C.nc renamed as FtstSpiStm3C.nc
```
详细见 [Perl 正则表达式](http://www.runoob.com/perl/perl-regular-expressions.html)


## 4. Share：分享

这里打分享主要也是学习，不过在学习过程中发现有些博客打内容有问题，所以提出来算是分享啦。

- 由来是从windows中拷贝类文档.txt .c 一类，结果编码出问题，不能在linux中utf8显示。
> 4.1.转换编码
>
> 4.2.批量转换

### 4.1.iconv转换文档编码
- 命令`file -i filename`查看文件的字符编码,另外apt安装打enca
- 命令iconv转换字符集， `iconv -f iso-8859-1 -t utf-8 readme.txt `

> 参考：
> [Ubuntu下批量转换文件的字符编码](http://sparkandshine.net/ubuntu-batch-convert-files-character-set/)

### 4.2. 批量转换
在上1中的参考中也有批量转换打实现。不过其中for 循环的位置有问题。查阅参考后，总结效率相对不错打两种方法。
- while循环
``` bash
    While read LINE     # 不转义 read -r
    do
    echo $LINE
    done  < $FILENAME
```

- for 循环
```
    for line in $(cat filename)    # 于1中参考不一致的地方。需要有$(cat  xxx  )
    do
    echo $line
    done
```
> 参考:
> [Shell逐行读取文件的4种方法](https://www.jb51.net/article/59041.htm);[Shell脚本循环读取文件中的每一行](http://www.linuxdiyf.com/linux/25722.html)

### 4.3 最后源码

```
    #!/usr/bin/env bash

    tmp_file="tmp.txt"
    echo "$tmp_file"
    trap "rm -f $tmp_file" exit

    find . -name "*.c" > $tmp_file

    for file in "$(cat ./$tmp_file)"        #for   问题所在，引入打变量作为文件名要合成具体地址。
#    cat $tmp_file | while read file        #while
    do
        echo "$file"
        #iconv -f iso-8859-1 -t utf-8 $file
        iconv -f gbk -t utf-8 $file -o "$file.new"
        echo "$file done"
        mv "$file.new" $file #replace the old file
    done
```


## 5.每周总结

> 本周主要做了如下事情：

- 健身
- 基本工作内容
- 深入学习Http
- 了解机器学习
- 学习设计模式

> 健身

从今年年初开始健身，身体明显发生了一些改变，主要改变有几点：
- 去年跑3公里就不想跑了，今年跑10公里也不怎么累
- 长跑中锻炼心态，逼迫自己不要太着急，慢点慢点

> 工作内容

- 在开发过程中重构了一个接口，但是因为在之前没有做出设计，在过代码的时候被否，也给自己一些思考

> 深入学习Http

- Http用的很多，但是了解的也很基础，之前看了一遍`图解Http`但是没有总结，这次深入学习，学习Http，给自己的目标是写一篇或者多篇高质量的Http文章
- 网络中，特别是TCP的一些策略还是比较值得学习

> 了解机器学习

- 机器学习在一些特定的领域还是比较有发展，有些代码不太好解决的问题机器学习很方便的可以解决，先了解下

> 学习设计模式
> 推荐书籍：

- 图解设计模式
- 大话设计模式
- 重构
- 重构与模式
