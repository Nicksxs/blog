title: Number of 1 Bits
date: 2015-03-11 17:02:58
categories: leetcode
tags: [leetcode, c++]
---
### [Number of 1 Bits ](https://leetcode.com/problems/number-of-1-bits/)
#### Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight). For example, the 32-bit integer '11' has binary representation  ``00000000000000000000000000001011``, so the function should return 3.
<!--more-->

### 分析
从1位到2位到4位逐步的交换

---
### code
``` C++
int hammingWeight(uint32_t n) {
        const uint32_t m1  = 0x55555555; //binary: 0101...  
        const uint32_t m2  = 0x33333333; //binary: 00110011..  
        const uint32_t m4  = 0x0f0f0f0f; //binary:  4 zeros,  4 ones ...  
        const uint32_t m8  = 0x00ff00ff; //binary:  8 zeros,  8 ones ...  
        const uint32_t m16 = 0x0000ffff; //binary: 16 zeros, 16 ones ...  
        
        n = (n & m1 ) + ((n >>  1) & m1 ); //put count of each  2 bits into those  2 bits   
        n = (n & m2 ) + ((n >>  2) & m2 ); //put count of each  4 bits into those  4 bits   
        n = (n & m4 ) + ((n >>  4) & m4 ); //put count of each  8 bits into those  8 bits   
        n = (n & m8 ) + ((n >>  8) & m8 ); //put count of each 16 bits into those 16 bits   
        n = (n & m16) + ((n >> 16) & m16); //put count of each 32 bits into those 32 bits   
        return n; 

}
```