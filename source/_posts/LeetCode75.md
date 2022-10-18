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

#### Solution
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

#### Solution
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

#### Solution
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

#### Solution
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
2022.10.1
### 21. Merge Two Sorted Lists(need reviwe)
Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

#### Solution
``` bash
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
      if(l1 == NULL) return l2;
      if(l2 == NULL) return l1;
      if(l1->val <= l2->val) {l1->next = mergeTwoLists(l1->next, l2); return l1;}
      else {l2->next = mergeTwoLists(l1,l2->next); return l2;}
    }
};//wiht help and finish this 
```
 C++ || Easy To Understand || 2 Approaches || Recursive || Iterative 
 [KnockCat](https://leetcode.com/problems/merge-two-sorted-lists/discuss/1826666/)

### 206. Reverse Linked List(need reviwe)

#### Solution
restore preview node and the next node 
change current node let first node->next => pre node 
then let pre node as current node
next node store current node -> next
so let current node => next node
judgy current node if Null;
``` bash
ListNode* reverseList(ListNode* h) {
      ListNode *pre_h , *next_h;
      pre_h = NULL;
      //next_h = h;
      while(h !=NULL){
        next_h = h->next;
        h->next = pre_h;
        pre_h = h;
        h = next_h;
      }
      return pre_h;
    }
```
[C++] Iterative vs. Recursive Solutions Compared and Explained, ~99% Time, ~85% Space 
Ajna

### 876. Middle of the Linked List
If there are two middle nodes, return the second middle node.
#### Solution
count list num , *h copy a head , mid find the node;
``` bash
ListNode* middleNode(ListNode* head) {
      int count = 0;
      ListNode *mid , *h;
      h = head;
      while(head){
        head = head->next;
        count ++;
      }
      count = count / 2 + 1;
      while(count--){
        mid = h;
        h = h->next;
      }
      return mid;
    }
```
better solution
``` bash
ListNode* middleNode(ListNode* head) {
        ListNode *slow = head, *fast = head;
        while (fast && fast->next)
            slow = slow->next, fast = fast->next->next;
        return slow;
    }
```
Each time, slow go 1 steps while fast go 2 steps.
When fast arrives at the end, slow will arrive right in the middle.
lee215

### 142. Linked List Cycle II
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

#### Solution
O(n^2) not a good solution maybe easy to understand.
detectCycle checkout the pre node and a copy of head node.
``` bash
ListNode *detectCycle(ListNode *head) {
      ListNode *pre , *copy;
      pre = copy = head ;
      if(head == NULL || head->next == NULL)
        return NULL;
      
      while(copy){
        if(copy == copy->next) return copy;
        copy = copy->next;
        if(copy->next == NULL) return NULL;
        while(pre != copy){
          //cout<<pre->val<<"!="<<copy->val<<" ";
          if(pre == copy->next) return pre;
          pre = pre->next;
        }
        
        pre = head;
        //return detectCycle(head->next);
      }
      return NULL;
    }
``` 
O(n) solution
``` bash 
ListNode *detectCycle(ListNode *head) {
    if (head == NULL || head->next == NULL)
        return NULL;
    
    ListNode *slow  = head;
    ListNode *fast  = head;
    ListNode *entry = head;
    
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) {                      // there is a cycle
            while(slow != entry) {               // found the entry location
                slow  = slow->next;
                entry = entry->next;
            }
            return entry;
        }
    }
    return NULL;                                 // there has no cycle
}
```
Concise O(n) solution by using C++ with Detailed Alogrithm Description
ngcl

### 121. Best Time to Buy and Sell Stock
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

#### Solution
time limit
``` bash
/*
[7,1,5,3,6,4]
[0]
[9,0]
[7,6,4,3,1]
[1101,1102,1111]
int maxProfit(vector<int>& prices) {
      int n = prices.size();
      int profit = 0 , max , min ;
      max = min = prices[0];
      //int index = 0;
      if(n<=1) return 0;
      for(int i = 0; i < n - 1 ; i ++){
        for(int j = i + 1; j < n ; j ++){
          if(profit < prices[j] - prices[i]){
            profit = prices[j] - prices[i];
          }
        }
      }
      return profit;
    }
*/
```
let min is the smalliest numbers ,then checkout max prices after min
every time we will choose the smalliest and the  after min's bigest number
``` bash
int maxProfit(vector<int>& prices) {
      int n = prices.size();
      int profit = 0 , max , min ;
      min = prices[0];
      max = prices[1];
      
      if(n<=1) return 0;
      
      for(int i = 1; i < n; i ++){
        if(min > prices[i]){
          min = prices[i];
        }
        else if(max < prices[i]) max = prices[i];
        //cout<<(max - min)<<endl;
        if(profit < (max - min)){
            profit = max - min;
        }
        if(i + 1 < n) max = prices[i+1];
        //cout<<" min "<<min<<" max "<<max<<" profit "<<profit<<endl;
      }
      return profit;
    }
```

``` bash
{
    int lsf = Integer.MAX_VALUE; // least so far
    int op = 0; // overall profit
    int pist = 0; // profit if sold today
        
    for(int i = 0; i < prices.length; i++){
        if(prices[i] < lsf){ // if we found new buy value which is more smaller then previous one
            lsf = prices[i]; // update our least so far
        }
        pist = prices[i] - lsf; // calculating profit if sold today by, Buy - sell
        if(op < pist){ // if pist is more then our previous overall profit
            op = pist; // update overall profit
        }
    }
        return op; // return op 
}
```

### 409. Longest Palindrome
longest palindrome

#### Solution
map[256]
as a math problems count a-z A-Z while the count > 2 palindrome length + 2 after we count , we need calculat if is have a single number ,if we have one , len should + 1 as middle char
``` bash
int longestPalindrome(string s) {
      int len = 0;
      int map[256] = { 0 };
      for(int i = 0; i < s.length(); i++){
        //cout<<" s[i] "<<s[i]<<" map[s[i]] "<<map[s[i]]<<endl;
        map[s[i]] += 1;
        //cout<<" s[i] "<<s[i]<<" map[s[i]] "<<map[s[i]]<<endl;
        if(map[s[i]] % 2 == 0) len += 2;
      }

      for(int i = 0; i < 256 ; i ++)
        if(map[i] % 2) return len + 1;
      
      return len;
    }

      // for(int i = 0; i < 256 && map[i] > 1 ; i ++){
      //   len += map[i] / 2 * 2;
      //   cout<<" map[s[i]] "<<map[s[i]]<<endl;
      // }
```

### 589. N-ary Tree Preorder Traversal
Nary-Tree input serialization is represented in their level order traversal. Each group of children is separated by the null value.

#### Solution
``` bash
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<int> preorder(Node* root) {
      vector<int> result;
      if(root == nullptr) return result;
      stack<Node *> s;
      s.push(root);
      Node * cur;
      while(!s.empty()){
        cur = s.top();
        result.push_back(cur->val);
        s.pop();
        for(int i = cur->children.size() - 1 ; i >= 0 ; i --){
          if(cur->children[i] != nullptr ) {
            s.push(cur->children[i]);
          }
        }
      }
      return result;
    }
};
```
stack function , using vector , 
MrQuin : 
From the code we use a stack to simulate the process:
we push 1 to the stack.
we pop 1 out, add 1 into result; Add the children of 1 into stack. The value in the stack will be 3, 2 and 2 at the top position;
we pop 2 out and add it to result; Then we add children of 2 into stack. So the stack will be like 3, 5, 4 and with 4 at the top.
we pop 4 and 5 out of stack since they are leaf node. Currently result will be like 1, 2, 4, 5.
we pop 3 out and add its children into stack. The stack is like 7, 6 with 6 at the top.
we pop 6 and 7 out and the stack becomes empty.
So the final result will be 1, 2, 4, 5, 3, 6, 7

### 102. Binary Tree Level Order Traversal
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

#### Solution
``` bash
vector<vector<int>> levelOrder(TreeNode *root) {
  vector<vector<int>> result;
  if(root == nullptr) return result;
  
  TreeNode *cur;
  queue<TreeNode *> que;
  que.push(root);
  while(!que.empty()){
    vector<int> value;
    
    for(int i = que.size() - 1; i >= 0 ; i --){
      cur = que.front();
      que.pop();
      if(cur->left) que.push(cur->left);
      if(cur->right) que.push(cur->right);
      value.push_back(cur->val);
    }
    result.push_back(value);
  }
  return result;
}
```
checkout 
``` bash
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>>arr;
        if(root==nullptr)return arr;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            vector<int>ans;
            int n=q.size();
            
            for(int i=0;i<n;i++){
                
                TreeNode*cur=q.front();
                q.pop();
                if(cur->left)q.push(cur->left);
                
                if(cur->right)q.push(cur->right);
                
                ans.push_back(cur->val);
            }
            arr.push_back(ans);
        }
        return arr;
    }
};
```
leetcode discuss Conquistador17

### 704. Binary Search
O(log n) runtime complexity.

#### Solution
``` bash
int search(vector<int>& nums, int target) {
      //int n =  = nums.size() / 2;
      int left, mid, right;
      left = 0 ;
      mid = nums.size() / 2;
      right = nums.size();
      while(mid > left && mid < right){
       //cout<<"\ntarget:"<<target<<" left:"<<left<<" mid:"<<mid<<" right:"<<right;
       if(target == nums[mid]) return mid;
       if(target > nums[mid]){
         left = mid;
         mid = left + (right - left) / 2;
       }
       if(target < nums[mid]){
         right = mid;
         mid = left + (right - left) / 2;
       }
      }
      if(target == nums[left]) return left;
      return -1;
    }
```
better solution
``` bash
lone_02wolf
110
Last Edit: September 18, 2021 8:03 PM

11.8K VIEWS

Upvote to motivate

int search(vector<int>& nums, int target) {
        int n = nums.size()-1;
        int low = 0, high = n;
        while( low <= high){
            int mid = low + (high-low)/2;
            if (nums[mid] == target) return mid;
            else if (nums[mid] > target) high = mid -1;
            else low = mid + 1;
        }
        return -1;
  }
```

### 278. First Bad Version
Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.
You are given an API bool isBadVersion(version) which returns whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

#### Solution
``` bash
int firstBadVersion(int n) {
      int left = 0, right = 2147483648 - 1; // 2^32 - 1
      while(1){
        if(isBadVersion(n)){
          right = n - 1;
          if(isBadVersion(right) == false) return right + 1;
        }
        else{
          left = n + 1;
          if(isBadVersion(left)) return left;
        }
        n = left + (right - left) / 2;
      }  
    }
```
better solution:
``` bash
int firstBadVersion(int n) {
        int lower = 1, upper = n, mid;
        while(lower < upper) {
            mid = lower + (upper - lower) / 2;
            if(!isBadVersion(mid)) lower = mid + 1;   /* Only one call to API */
            else upper = mid;
        }
        return lower;   /* Because there will alway be a bad version, return lower here */
    }
```

whaleking1990
70
September 7, 2015 9:21 PM

21.7K VIEWS

### Not Finished