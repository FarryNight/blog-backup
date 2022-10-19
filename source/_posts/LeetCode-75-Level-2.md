---
title: LeetCode 75 Level 2
author: Farry
cover: true
tags: [c++,syntactic sugar]
categories: [Algorithms]
reprintPolicy: cc_by
date: 2022-10-15 20:24:34
img:
top:
---
## LeetCode75-v2
leetcode
<!-- more -->

### 202. Happy Number
A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.

#### Solution
n%10 get last number , n/10 let n smaller , map[100] , beacause all of the number will get smaller than 100 if the number is repeat , that mean's we fund a loop .
``` c++
bool isHappy(int n) {
  int sum = 0;
  int map[100] = {0};
  while (1){
    while(n > 0){
      sum += (n % 10) * (n % 10);
      //cout<<"\n sum:"<<sum;
      n /= 10;
    }
    n = sum;
    sum = 0;
    if(n < 100){
      if(map[n]) return false;
      else map[n] = 1;
    }
    //cout<<"\n n:"<<n;
    if(n == 1) return true;
  }
  return true;
}
```

### 54. Spiral Matrix
Given an m x n matrix, return all elements of the matrix in spiral order.

#### Solution
``` c++
vector<int> spiralOrder(vector<vector<int>>& m) {
  vector<int> result;
  int in = m.size() , jn = m[0].size();
  int left = 0 , down = 0 , right = jn - 1 , up = in - 1 , step = 1;
  while( left <= right && down <= up ){
    int i = left , j = left;
    if(step == 1){
      for( ; j <= right ; ++j ){
        result.push_back(m[i][j]);
      }
      down++;
      step++;
    }
    else if(step == 2){
      for( j = right , i = down ; i <= up ; ++i ){
        //cout<<m[i][j]<<" i , j "<<i<<" "<<j;
        result.push_back(m[i][j]);
      }
      right--;
      step++;
    }
    else if(step == 3){
      for( i = up , j = right ; j >= left ; --j ){
        result.push_back(m[i][j]);
      }
      up--;
      step++;
    }
    else if(step == 4){
      for( j = left , i = up ; i >= down ; --i ){
        result.push_back(m[i][j]);
      }
      left++;
      step = 1;
    }
  }
  return result;
}
```
discuss
``` c++
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    int n=matrix.size();
    int m=matrix[0].size();
    int left=0,right=m-1,bottom=n-1,top=0;
    int direction=1;
    vector<int> v;
    while(left<=right && top<=bottom)
    {
        if(direction==1)
        {
            for(int i=left;i<=right;i++) v.push_back(matrix[top][i]);
            direction=2;
            top++;
        }
        
        else if(direction==2)
        {
            for(int i=top;i<=bottom;i++) v.push_back(matrix[i][right]);
            direction=3;
            right--;
        }
        
        else if(direction==3)
        {
            for(int i=right;i>=left;i--) v.push_back(matrix[bottom][i]);
            direction=4;
            bottom--;
        }
        
        else if(direction==4)
        {
            for(int i=bottom;i>=top;i--) v.push_back(matrix[i][left]);
            direction=1;
            left++;
        }
    }
    return v; 
}
```
C++ | 0ms faster than 100% | Easy solution with proper explanation
rv237
368
Last Edit: December 20, 2020 4:52 PM

11.4K VIEWS

A concise C++ implementation based on Directions
stellari
5661
Last Edit: October 21, 2018 7:01 AM

50.6K VIEWS
``` c++
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<vector<int> > dirs{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    vector<int> res;
    int nr = matrix.size();     if (nr == 0) return res;
    int nc = matrix[0].size();  if (nc == 0) return res;
    
    vector<int> nSteps{nc, nr-1};
    
    int iDir = 0;   // index of direction.
    int ir = 0, ic = -1;    // initial position
    while (nSteps[iDir%2]) {
        for (int i = 0; i < nSteps[iDir%2]; ++i) {
            ir += dirs[iDir][0]; ic += dirs[iDir][1];
            res.push_back(matrix[ir][ic]);
        }
        nSteps[iDir%2]--;
        iDir = (iDir + 1) % 4;
    }
    return res;
}
```

### 


#### 

### 


#### 

### 


#### 

### 


#### 
