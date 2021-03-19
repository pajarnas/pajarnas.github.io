---
title: Dynamic Programming Leetcode
date: 03/19/2021
updated: 
tags: 
  - notes
  - leetcode
  - interview
  - dynamic programming
  - medium
categories: 
  - interview
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

# **Dynamic Programming**: Number of Longest Increasing Subsequence

# Description

Given an integer array `nums`, return *the number of longest increasing subsequences.*

**Notice** that the sequence has to be **strictly** increasing.

 

## **Example 1:**

```
Input: nums = [1,3,5,4,7]
Output: 2
Explanation: The two longest increasing subsequences are [1, 3, 4, 7] and [1, 3, 5, 7].
```

## **Example 2:**

```
Input: nums = [2,2,2,2,2]
Output: 5
Explanation: The length of longest continuous increasing subsequence is 1, and there are 5 subsequences' length is 1, so output 5.
```

 

## **Constraints:**

- `1 <= nums.length <= 2000`
- `-106 <= nums[i] <= 106`

# Thought and Notes

Given A[j] and A[j-1], for A[j] you can just borrow the the longest number of A[j-1] and then if A[j] > A[j-1], the length of A[j] = LIS(A[j-1]) + 1. There is one special condition: if LIS(A[j])  was already = LIS(A[j-1]) + 1, then counts = counts[j-1] + counts . if LIS[A[j-1] != or < , then it means this is the first time to get such length, so counts = counts[j-1].

# Solution

## Approach 1: Dynamic Programming

### **Intuition and Algorithm**

Suppose for sequences ending at `nums[i]`, we knew the length `length[i]` of the longest sequence, and the number `count[i]` of such sequences with that length.

For every `i < j` with `A[i] < A[j]`, we might append `A[j]` to a longest subsequence ending at `A[i]`. It means that we have demonstrated `count[i]` subsequences of length `length[i] + 1`.

Now, if those sequences are longer than `length[j]`, then we know we have `count[i]` sequences of this length. If these sequences are equal in length to `length[j]`, then we know that there are now `count[i]` additional sequences to be counted of that length (ie. `count[j] += count[i]`).

```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        int N = nums.length;
        if(nums.length <= 1) return 1;
        int[] lengths = new int[N];
        int[] counts = new int[N];
        Arrays.fill(counts,1);
        
        for(int j = 0; j < N; j++){
            for(int i = 0; i < j; i++){
                if(nums[i] < nums[j]){
                    if(lengths[j]<=lengths[i]){
                        lengths[j] = lengths[i] + 1;
                        counts[j] = counts[i];
                    }else if(lengths[i] + 1 == lengths[j]){
                        counts[j] += counts[i];
                    }
                }
            }
        }
        
        int longest = 0, ans = 0;
        for (int length: lengths) {
            longest = Math.max(longest, length);
        }
        for (int i = 0; i < N; ++i) {
            if (lengths[i] == longest) {
                ans += counts[i];
            }
        }
        return ans;
    }
}
```

### **Complexity Analysis**

- Time Complexity: O(N^2)*O*(*N*2) where N*N* is the length of `nums`. There are two for-loops and the work inside is O(1)*O*(1).
- Space Complexity: O(N)*O*(*N*), the space used by `lengths` and `counts`.

# Performance

Runtime: 18 ms, faster than 87.80% of Java online submissions for Number of Longest Increasing Subsequence.

Memory Usage: 38.5 MB, less than 73.33% of Java online submissions for Number of Longest Increasing Subsequence.