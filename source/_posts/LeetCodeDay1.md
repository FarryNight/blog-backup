---
title: LeetCodeDay1
author: Farry
img: 
top: true
cover: true
reprintPolicy: cc_by
date: 2022-09-29 22:25:10
tags: [c++,syntactic sugar]
categories: [Algorithms]
---
## Question

### Count Odd Numbers in an Interval Range
odd even | odd odd | even even | even Odd
<!-- more -->

### Solution
``` bash
int countOdds(int low, int high) {
        int i = 0 ;
        while ( low <= high ) {
            if( low % 2 == 1 && low != 2 ){
                i++;
                low+=2;
            }
            else{
                low+=1;
            }
        }
        return i; // Time Limit Exceeded
    }
```
Changes:
``` bash
int countOdds(int low, int high) {
        if( low % 2 == 1 && low != 2 ){
            low -= 1 ;
        }
        if( high % 2 == 1 && high != 2 ){
            high += 1 ;
        }
        return ( high - low ) / 2 ;
    }//Accepted
```
best answer:
``` bash
int countOdds(int low, int high) {
    return (high + 1) / 2 - low / 2;
}
```

### Average Salary Excluding the Minimum and Maximum Salary
salary.size();

### Solution
``` bash
class Solution {
public:
    double average(vector<int>& salary) {
        int max , min ;
        double sum = 0 ;
        max = min = salary[0];
        for( int i = 0 ; i < salary.size() ; i++ ) {
            if (max < salary[i] ){
                max = salary[i];
            }
            if ( min > salary[i] ){
                min = salary[i];
            }
            sum += salary[i] ;
        }
        return ( sum - max - min ) / (salary.size() - 2) ;
    }
};
```