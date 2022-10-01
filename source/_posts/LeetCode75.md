---
title: LeetCode75
author: Farry
img: 
cover: true
tags: [c++,syntactic sugar]
categories: [Algorithms]
reprintPolicy: cc_by
date: 2022-09-30 15:30:06
top: 
---
## Introduction
This study plan is for those who want to prepare for technical interviews but are uncertain which problems they should focus on. 、

### 1480.Running Sum of 1d Array
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
n[i+1] = n[i]+n[i+1]

### Solution
``` bash
vector<int> runningSum(vector<int>& n) {
        for(int i=0 ; i<n.size()-1 ; i++){
            n[i+1] = n[i]+n[i+1];
        }
        return n;
    }
```

### 724. Find Pivot Index
The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.

### Solution
``` bash
// int pivotIndex(vector<int>& nums) {
//         int n = nums.size();
//         int left , right , mid;
//         left = right = mid = 0;
//         while(mid <= n-1){ //n - 1
//             if(mid == 0){
//                 left = 0 ;
//             }else{
//                 for(int i = 0 ; i < mid ; i++){
//                     left += nums[i];
//                 }
//             }
//             if(mid == n - 1){
//                 right = 0 ;
//             }else{
//                 for(int i = n-1 ; i > mid ; i--){
//                     right += nums[i];
//                 }
//             }
//             //if is equal
//             if(left == right){
//                 break;
//             }
//             mid ++;
//             left = right = 0;
//         }
//         if(mid == n){
//             return -1;
//         }
//         return mid; // time limit O(n^2)
        
//     }
```
``` bash
int pivotIndex(vector<int>& nums) {
        int n = nums.size();
        int left , right , mid;
        left = right = mid = 0;
        for(int i = 1 ; i < n ; i++){
            right += nums[i];
        }
        while(mid < n){
            if(left == right){
                break;
            }
            left += nums[mid];
            if(mid+1 < n){
                right -= nums[mid+1];
            }
            mid ++;
            // left += nums[mid-1];
            // right -= nums[mid];
        }
        if(mid == n){
            return -1;
        }
        return mid;
    }
```
LeetCode Solution
``` bash
class Solution {
    public int pivotIndex(int[] nums) {
        int sum = 0, leftsum = 0;
        for (int x: nums) sum += x;
        for (int i = 0; i < nums.length; ++i) {
            if (leftsum == sum - leftsum - nums[i]) return i;
            leftsum += nums[i];
        }
        return -1;
    }
}
```
### 205. Isomorphic Strings
Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

### Solution
```
//     bool isIsomorphic(string s, string t) {
//         int i_s, i_t;
//         i_s = 0;
//         i_t = 0;
//         if(s.size() == 1 && t.size() == 1){
//             return true;
//         }
//         for(int i = 1; s[i] != '\0' && t[i] != '\0'; i++){
//             if(s[i] == s[i-1]){
//                 i_s = 0;
//             }else{
//                 i_s = 1;
//             }
            
//             if(t[i] == t[i-1]){
//                 i_t = 0;
//             }else{
//                 i_t = 1;
//             }
//             // i_s = s[i] - s[i-1];
//             // i_t = t[i] - t[i-1];
            
//             if(i_s != i_t /**or s[i] != t[i]*/){
//                 return false;
//             }
//         }
//         return true;
//     }
```
``` bash
bool isIsomorphic(string s, string t) {
        int map_s[128] = {0};
        for (int i = 0; s[i] != '\0'; i++) {
            if (map_s[s[i]] == 0) {
                // map_t[t[i]] = s[i];
                for(auto t_ : map_s) {
                    if (t_ == t[i]) return false;
                }
                map_s[s[i]] = t[i];
            } else {
                if (map_s[s[i]] != t[i]) return false;
            }
        }
        return true;
    }
```
6 lines solution : grandyang
``` bash
bool isIsomorphic(string s, string t) {
        int m1[256] = {0}, m2[256] = {0}, n = s.size();
        for (int i = 0; i < n; ++i) {
            if (m1[s[i]] != m2[t[i]]) return false;
            m1[s[i]] = i + 1;
            m2[t[i]] = i + 1;
        }
        return true;
    }
```

### 392. Is Subsequence
A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).

### Solution
``` bash
bool isSubsequence(string s, string t) {
      int i_t = 0;
      int i_s = 0;
      if(s[i_s] == '\0') return true;
      while(t[i_t + 1]){
        if(s[i_s] == t[i_t]){
          i_s ++;
          if(s[i_s] == '\0' && t[i_t] != '\0') return true;
        }
        i_t ++;
      }
      //if(s[i_s]) return false;
      // if(t[i_t] == '\0'){
      //   if(s[i_s] == t[i_t - 1]) return true;
      // }
      if(s[i_s] == t[i_t] && s[i_s + 1] == '\0') return true;
      
      return false;
    }
```
0ms 8.7mb : abhimanyuahuja
``` bash
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int n = s.length(),m=t.length();
        int j = 0; 
    // For index of s (or subsequence
 
    // Traverse s and t, and
    // compare current character
    // of s with first unmatched char
    // of t, if matched
    // then move ahead in s
    for (int i = 0; i < m and j < n; i++)
        if (s[j] == t[i])
            j++;
 
    // If all characters of s were found in t
    return (j == n);
    }
};
```

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###

###