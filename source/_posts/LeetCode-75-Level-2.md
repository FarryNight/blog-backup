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

### 1706. Where Will the Ball Fall


#### Solution
you need to know the ball's  moving action search from 0 to cloumn lenght , search every cloumn if it will fall , the count will equal row lenght
``` c++
class Solution {
public:
    vector<int> findBall(vector<vector<int>>& grid) {
      int m = grid.size() , n = grid[0].size() - 1;
      int il = 0 , ir = n , step = 0 , count = 0 ;
      vector<int> res;
      while( n + 1 ){
        //cout<<"\n il "<< il ;
        //cout<<"\n i il count ";
        for( int i = 0 ; i < m ; ++i){
          //cout<<"\n grid[i][il]:"<< grid[i][il] <<" ";
          if(grid[i][il] == 1 && il + 1 <= ir && grid[i][il] == grid[i][il + 1]){
            //cout<<"\n "<< i <<" "<< il << " " << count;
            ++il;
            ++count;
            continue;
          }
          if(grid[i][il] == -1 && il - 1 >= 0 && grid[i][il] == grid[i][il - 1]){
            //cout<<"\n "<< i <<" "<< il << " " << count;
            --il;
            ++count;
            continue;
          }
          //else break;
        }
        if(count >= m) res.push_back(il);
        else res.push_back(-1);
        il = ++step;
        --n;
        count = 0;
      }
      return res;
    }
};

/*
[[1,1,1,-1,-1],[1,1,1,-1,-1],[-1,-1,-1,1,1],[1,1,1,1,-1],[-1,-1,-1,-1,-1]]
[[-1]]
[[1,1,1,1,1,1],[-1,-1,-1,-1,-1,-1],[1,1,1,1,1,1],[-1,-1,-1,-1,-1,-1]]
*/
```
lee215
167146
December 27, 2020 3:04 PM

14.2K VIEWS
[Java/C++/Python] Solution with Explanation
``` c++
vector<int> findBall(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<int> res;
        for (int i = 0; i < n; ++i) {
            int i1 = i, i2;
            for (int j = 0; j < m; ++j) {
                i2 = i1 + grid[j][i1];
                if (i2 < 0 || i2 >= n || grid[j][i2] != grid[j][i1]) {
                    i1 = -1;
                    break;
                }
                i1 = i2;
            }
            res.push_back(i1);
        }
        return res;
    }
```
great solution

### 14. Longest Common Prefix
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

#### solution
compaire every string of index if not equal return res ;
``` c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
      int map[128] = { 0 };
      int n = strs.size() , i = 0 , len = strs[i].size() ;
      string res;
      //cout<<n<<endl;
      if( n == 1){
        for(int i = 0 ; i < len ; ++i) res.push_back(strs[0][i]);
        return res;
      }
      int nextlen = strs[i + 1].size();
      for(int j = 0 ; j < len && j < nextlen; ++j){
        for(i = 0 ; i < n - 1 ; ++i){
          nextlen = strs[i + 1].size();
          if(strs[i][j] == strs[i+1][j]){
            map[ strs[i][j] ] ++;
          }
          else return res;
          if(map[ strs[i][j] ] != 0 && map[ strs[i][j] ] % (n - 1) == 0 ){
            res.push_back(strs[i][j]);
          }
        }
      }
      return res;
    }
};
/*
["flower","flow","flight"]
["ab","ba","ca","da"]
["a"]
["dog","racecar","car"]
[""]
["aabbbaaaaaabbbaaaa","aabbbaaaaaabbbaaaa","aabbbaaaaaabbbaaaa","aabbbaaaaaabbbaaaa","aabbbaaaaaabbbaaaa","aabbbaaaaaabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa"]
["a","ba"]
["cir","car"]
["aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa","aabbbaaaa"]

*/
```
more simple way 
``` c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& str) {
        int n = str.size();
        if(n==0) return "";
        
        string ans  = "";
        sort(begin(str), end(str));
        string a = str[0];
        string b = str[n-1];
        
        for(int i=0; i<a.size(); i++){
            if(a[i]==b[i]){
                ans = ans + a[i];
            }
            else{
                break;
            }
        }
        
        return ans;
        
    }
};
```

### 


#### solution
``` c++
```

### 


#### solution
``` c++
```

### 


#### solution
``` c++
```

### 


#### solution
``` c++
```

### 


#### solution
``` c++
```
