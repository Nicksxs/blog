title: pcre-intro-and-a-simple-package
date: 2015-01-16 14:30:20
categories: C++
tags: [mfc, c++]
---
### [Pcre](http://www.pcre.org/)
> Perl Compatible Regular Expressions (PCRE) is a regular  
 expression C library inspired by the regular expression  
 capabilities in the Perl programming language, written   
 by Philip Hazel, starting in summer 1997.

因为最近工作内容的一部分需要做字符串的识别处理，所以就顺便用上了之前在PHP中用过的正则，在C/C++中本身不包含正则库，这里使用的pcre，对MFC开发，在[这里](http://www.psyon.org/projects/pcre-win32/index.php)提供了静态链接库，在引入lib跟.h文件后即可使用。
<!--more-->

### Regular Expression Syntax
然后是一些[正则语法](http://www.pcre.org/original/doc/html/pcresyntax.html)，官方的语法文档比较科学严谨，特别是对类似于贪婪匹配等细节的说明，当然一般的使用可以在网上找到很多匹配语法，例如[这个](http://www.regextester.com/pregsyntax.html)。

### PCRE函数介绍

>pcre_compile
原型：
``` C++
#include <pcre.h>
pcre *pcre_compile(const char *pattern, int options, const char **errptr, int *erroffset, const unsigned char *tableptr);
```
功能：将一个正则表达式编译成一个内部表示，在匹配多个字符串时，可以加速匹配。其同pcre_compile2功能一样只是缺少一个参数errorcodeptr。
参数：
`pattern`   正则表达式
`options`     为0，或者其他参数选项
`errptr`       出错消息
`erroffset`  出错位置
`tableptr`   指向一个字符数组的指针，可以设置为空NULL


>pcre_exec
原型：
``` C++
#include <pcre.h>
int pcre_exec(const pcre *code, const pcre_extra *extra, const char *subject, int length, int startoffset, int options, int *ovector, int ovecsize)
```
功能：使用编译好的模式进行匹配，采用与Perl相似的算法，返回匹配串的偏移位置。
参数：
`code`         编译好的模式
`extra`        指向一个pcre_extra结构体，可以为NULL
`subject`      需要匹配的字符串
`length`       匹配的字符串长度（Byte）
`startoffset`  匹配的开始位置
`options`      选项位
`ovector`      指向一个结果的整型数组
`ovecsize`     数组大小。

这里是两个最常用的函数的简单说明，pcre的静态库提供了一系列的函数以供使用，可以参考这个[博客](http://blog.csdn.net/sulliy/article/details/6247155)说明，另外对于以上函数的具体参数详细说明可以参考官网[此处](http://www.pcre.org/original/doc/html/)

### 一个丑陋的封装
``` C++
void COcxDemoDlg::pcre_exec_all(const pcre * re, PCRE_SPTR src, vector<pair<int, int>> &vc)
{
	int rc;
	int ovector[30];
	int i = 0;
	pair<int, int> pr;
	rc = pcre_exec(re, NULL, src, strlen(src), i, 0, ovector, 30);
	for (; rc > 0;)
	{
		i = ovector[1];
		pr.first = ovector[2];
		pr.second = ovector[3];
		vc.push_back(pr);
		rc = pcre_exec(re, NULL, src, strlen(src), i, 0, ovector, 30);
	}
}
```
vector中是全文匹配后的索引对，只是简单地用下。