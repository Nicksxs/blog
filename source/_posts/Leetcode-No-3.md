title: leetcode no.3
date: 2015-04-15 13:49:00
categories: leetcode
tags: [leetcode, c++]
---
**Longest Substring Without Repeating Characters **

<!-- more -->
###description
Given a string, find the length of the longest substring without repeating characters.   
For example, the longest substring without repeating letters for "abcabcbb" is "abc",   
which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.  
###分析
[源码](http://www.cnblogs.com/dollarzhaole/p/3155712.html)这次是参考了这个代码，  
tail 表示的当前子串的起始点位置，tail从-1开始就包括的串的长度是1的边界。其实我  
也是猜的（逃
```C++
int ct[256];
    memset(ct, -1, sizeof(ct));
	int tail = -1;
	int max = 0;
	for (int i = 0; i < s.size(); i++){
		if (ct[s[i]] > tail)
			tail = ct[s[i]];
		if (i - tail > max)
			max = i - tail;
		ct[s[i]] = i;
	}
	return max;
```
