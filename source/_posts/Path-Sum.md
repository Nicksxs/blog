title: Path Sum
date: 2015-01-04 15:44:10
categories: leetcode
tags: [leetcode, c++]
---
### problem
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

<!--more-->
For example:
Given the below binary tree and sum = 22,
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
```
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

### Analysis
using simple deep first search


### code

``` C++
/*
  Definition for binary tree
  struct TreeNode {
      int val;
      TreeNode *left;
      TreeNode *right;
      TreeNode(int x) : val(x), left(NULL), right(NULL)}
  };
 */
class Solution {
public:
    bool deep_first_search(TreeNode *node, int sum, int curSum)
    {
        if (node == NULL)
            return false;
        
        if (node->left == NULL && node->right == NULL)
            return curSum + node->val == sum;
               
        return deep_first_search(node->left, sum, curSum + node->val) || deep_first_search(node->right, sum, curSum + node->val);
    }
    
    bool hasPathSum(TreeNode *root, int sum) {
        // Start typing your C/C++ solution below
        // DO NOT write int main() function
        return deep_first_search(root, sum, 0);
    }
};
```
