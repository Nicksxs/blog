title: add-two-number
date: 2015-04-14 17:40:10
categories: leetcode
tags: [leetcode, c++]
---
###problem
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input**:`(2 -> 4 -> 3) + (5 -> 6 -> 4)`
**Output**: `7 -> 0 -> 8`

**分析（不用英文装逼了）**
这个代码是抄来的，[链接](https://github.com/haoel/leetcode)原作是这位大大。
<!--more-->
一开始没看懂题，后来发现是要进位的，自己写的时候想把长短不同时长的串接到结果
串的后面，试了下因为进位会有些问题比较难搞定，这样的话就是在其中一个为空的
时候还是会循环操作，在链表太大的时候可能会有问题，就这样（逃
原来是有个小错误没发现，改进后的代码也AC了，棒棒哒！

###正确代码
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        ListNode dummy(0);
        ListNode* p = &dummy;

        int cn = 0;
        while(l1 || l2){
            int val = cn + (l1 ? l1->val : 0) + (l2 ? l2->val : 0);
            cn = val / 10;
            val = val % 10;
            p->next = new ListNode(val);
            p = p->next;
            if(l1){
                l1 = l1->next;
            }
            if(l2){
                l2 = l2->next;
            }
        }
        if(cn != 0){
            p->next = new ListNode(cn);
            p = p->next;
        }
        return dummy.next;
    }
};
```

###失败的代码
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        ListNode dummy(0);
        ListNode* p = &dummy;

        int cn = 0;
        int flag = 0;
        while(l1 || l2){
            int val = cn + (l1 ? l1->val : 0) + (l2 ? l2->val : 0);
            cn = val / 10;
            val = val % 10;
            p->next = new ListNode(val);
            p = p->next;
            if(!l1 && cn == 0){
                flag = 1;
                break;
            }
            if(!l2 && cn == 0){
                flag = 1;
                break;
            }
            if(l1){
                l1 = l1->next;
            }
            if(l2){
                l2 = l2->next;
            }
        }
        if(!l1 && cn == 0 && flag == 1){
            p->next = l2->next;
        }
        if(!l2 && cn == 0 && flag == 1){
            p->next = l1->next;
        }
        if(cn != 0){
            p->next = new ListNode(cn);
            p = p->next;
        }
        return dummy.next;
    }
};
```
