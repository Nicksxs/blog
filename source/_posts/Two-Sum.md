title: two sum
date: 2015-01-14 15:39:31
categories: leetcode
tags: [leetcode, c++]
---
### problem
Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

<!--more-->
You may assume that each input would have exactly one solution.

**Input**: numbers={2, 7, 11, 15}, target=9
**Output**: index1=1, index2=2

### code
``` c++
struct Node
{
    int num, pos;
};
bool cmp(Node a, Node b)
{
    return a.num < b.num;
}
class Solution {
public:
    vector<int> twoSum(vector<int> &numbers, int target) {
        // Start typing your C/C++ solution below
        // DO NOT write int main() function
        vector<int> result;
        vector<Node> array;
        for (int i = 0; i < numbers.size(); i++)
        {
            Node temp;
            temp.num = numbers[i];
            temp.pos = i;
            array.push_back(temp);
        }

        sort(array.begin(), array.end(), cmp);
        for (int i = 0, j = array.size() - 1; i != j;)
        {
            int sum = array[i].num + array[j].num;
            if (sum == target)
            {
                if (array[i].pos < array[j].pos)
                {
                    result.push_back(array[i].pos + 1);
                    result.push_back(array[j].pos + 1);
                } else
                {
                    result.push_back(array[j].pos + 1);
                    result.push_back(array[i].pos + 1);
                }
                break;
            } else if (sum < target)
            {
                i++;
            } else if (sum > target)
            {
                j--;
            }
        }
        return result;
    }
};
```

### Analysis
sort the array, then test from head and end, until catch the right answer