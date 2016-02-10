title: Reverse Integer
date: 2015-03-13 17:22:20
categories: leetcode
tags: [leetcode, c++]
---
### [Reverse Integer](https://leetcode.com/problems/reverse-integer/)
#### Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

<!--more-->
#### spoilers

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

---
### code
``` C++
class Solution {
public:
    int reverse(int x) {

        int max = 1 << 31 - 1;
        int ret = 0;
        max = (max - 1) * 2 + 1;
        int min = 1 << 31;
        if(x < 0)
            while(x != 0){
                if(ret < (min - x % 10) / 10)
                    return 0;
                ret = ret * 10 + x % 10;
                x = x / 10;
            }
        else
            while(x != 0){
               if(ret > (max -x % 10) / 10)
                    return 0;
                ret = ret * 10 + x % 10;
                x = x / 10;
            }
        return ret;
    }
};
```
