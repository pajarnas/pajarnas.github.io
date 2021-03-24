---
title: Stack Leetcode
date: 03/19/2021
updated: 
tags: 
  - notes
  - leetcode
  - interview
  - stack
  - medium
categories: 
  - leetcode
keywords: 
  - java
  - solution
description: 
top_img: 
comments: 
cover: 
toc: 
toc_number: 
copyright:
copyright_author: Shiqi Zhang
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# Stack : Next Greater Element I

# Description

- You are given two integer arrays `nums1` and `nums2` both of **unique** elements, where `nums1` is a subset of `nums2`.

  Find all the next greater numbers for `nums1`'s elements in the corresponding places of `nums2`.

  The Next Greater Number of a number `x` in `nums1` is the first greater number to its right in `nums2`. If it does not exist, return `-1` for this number.

   

  **Example 1:**

  ```
  Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
  Output: [-1,3,-1]
  Explanation:
  For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
  For number 1 in the first array, the next greater number for it in the second array is 3.
  For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
  ```

  **Example 2:**

  ```
  Input: nums1 = [2,4], nums2 = [1,2,3,4]
  Output: [3,-1]
  Explanation:
  For number 2 in the first array, the next greater number for it in the second array is 3.
  For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
  ```

   

  **Constraints:**

  - `1 <= nums1.length <= nums2.length <= 1000`
  - `0 <= nums1[i], nums2[i] <= 104`
  - All integers in `nums1` and `nums2` are **unique**.
  - All the integers of `nums1` also appear in `nums2`.

# Thought and Notes

Simply find the pairs in nums2, then travels the nums1. 

# Solution

## Approach 1: Stack

https://leetcode.com/problems/next-greater-element-i/solution/

```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Stack < Integer > stack = new Stack < > ();
        HashMap < Integer, Integer > map = new HashMap < > ();
        int[] res = new int[findNums.length];
        for (int i = 0; i < nums.length; i++) {
            while (!stack.empty() && nums[i] > stack.peek())
                map.put(stack.pop(), nums[i]);
            stack.push(nums[i]);
        }
        while (!stack.empty())
            map.put(stack.pop(), -1);
        for (int i = 0; i < findNums.length; i++) {
            res[i] = map.get(findNums[i]);
        }
        return res;
    }
}
```

### **Complexity Analysis**

- Time complexity : O(m+n)*O*(*m*+*n*). The entire nums*n**u**m**s* array(of size n*n*) is scanned only once. The stack's n*n* elements are popped only once. The findNums*f**i**n**d**N**u**m**s* array is also scanned only once.
- Space complexity : O(m+n)*O*(*m*+*n*). stack*s**t**a**c**k* and map*m**a**p* of size n*n* is used. res*r**e**s* array of size m*m* is used, where n*n* refers to the length of the nums*n**u**m**s* array and m*m* refers to the length of the findNums*f**i**n**d**N**u**m**s* array.



