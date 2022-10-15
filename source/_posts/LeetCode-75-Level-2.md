---
title: LeetCode 75 Level 2
author: Farry
cover: true
tags: []
categories: []
reprintPolicy: cc_by
date: 2022-10-15 20:24:34
img:
top:
---
## 


### 202. Happy Number
A happy number is a number defined by the following process:

Starting with any positive integer, replace the number by the sum of the squares of its digits.
Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
Those numbers for which this process ends in 1 are happy.

#### Solution
n%10 get last number , n/10 let n smaller , map[100] , beacause all of the number will get smaller than 100 if the number is repeat , that mean's we fund a loop .
``` bash
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

### 


#### 

### 


#### 

### 


#### 

### 


#### 

### 


#### 
