title: Reverse Bits
date: 2015-03-11 17:35:20
categories: leetcode
tags: [leetcode, c++]
---
###[Reverse Bits ](https://leetcode.com/problems/reverse-bits/)
####Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).
<!--more-->
Follow up:
If this function is called many times, how would you optimize it?

---
###code
``` C++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        n = ((n >> 1) & 0x55555555) | ((n & 0x55555555) << 1);
        n = ((n >> 2) & 0x33333333) | ((n & 0x33333333) << 2);
        n = ((n >> 4) & 0x0f0f0f0f) | ((n & 0x0f0f0f0f) << 4);
        n = ((n >> 8) & 0x00ff00ff) | ((n & 0x00ff00ff) << 8);
        n = ((n >> 16) & 0x0000ffff) | ((n & 0x0000ffff) << 16);
        return n;
    }
};
```
