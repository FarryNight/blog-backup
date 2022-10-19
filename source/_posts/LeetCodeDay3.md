---
title: LeetCodeDay3
author: Farry
img: 
top: 
cover: true
reprintPolicy: cc_by
date: 2022-09-29 22:25:19
tags: [c++,syntactic sugar]
categories: [Algorithms]
---
## Question

### Largest Perimeter Triangle
store the 1st largest number
<!-- more -->
store the 2st largest number
store the 3st largest number
how to ?

wrong thinking , need take care of all the numbers ! not only the largest three numbers !
so , sort them and start from end

Try to get a triangle with 3 biggest numbers.
If A[n-1] < A[n-2] + A[n-3], we get a triangle.
If A[n-1] >= A[n-2] + A[n-3] >= A[i] + A[j], we cannot get any triangle with A[n-1]
repeat step2 and step3 with the left numbers.

check if it is a triangle : a >= b >= c, a,b,c can form a triangle if a < b + c. (math)

return

### Soloution
``` bash
int largestPerimeter(vector<int>& n) {
        sort( n.begin() , n.end() ) ;
        for ( int i = n.size() - 1 ; i > 1 ; i-- ){// i > 1 because n[i-2] 3 number
            if ( n[i] < n [i-1] + n[i-2] )
                return n[i] + n [i-1] + n[i-2] ;
        }
        return 0 ;
    }
```

### Find Nearest Point That Has the Same X or Y Coordinate
Return the index (0-indexed) of the valid point with the smallest Manhattan distance from your current location. If there are multiple, return the valid point with the smallest index. If there are no valid points, return -1.

The Manhattan distance between two points (x1, y1) and (x2, y2) is abs(x1 - x2) + abs(y1 - y2).
``` bash
int nearestValidPoint(int x, int y, vector<vector<int>>& p) {
    int min = -1 , index = -1 ;
    for ( int i = 0 ; i < p.size()-1 ; i += 2 ){
        if ( p[i][0] == x || p[i][1] == x ||
             p[i][0] == y || p[i][1] == y 
           ){
            if(min == -1 ){
                min = abs(x - p[i][0]) + abs( y - p[i][1] ); \
                index = i ;
                continue ;
            }
            if( min > abs(x - p[i][0]) + abs( y - p[i][1] ) ){
                //min = abs(x - p[i][0]) + abs( y - p[i][1] ) ;
                index = i ;
            }
        }
    }
    return index ;
}
```
3
4
[[1,2],[3,1],[2,4],[2,3],[4,4]]

3
4
[[2,3]]

can’t sove this example
need cosider the case : Same X or Y Coordinate

### Solution
``` bash
class Solution {
public:
    int nearestValidPoint(int x, int y, vector<vector<int>>& p) {
        int min = -1 , index = -1 ;
        for ( int i = 0 ; i < p.size() ; i ++ ){
            if ( p[i][0] == x || p[i][1] == y){
                if(min == -1 ){
                    min = abs(x - p[i][0]) + abs( y - p[i][1] ); \
                    index = i ;
                    continue ;
                }
                if( min > abs(x - p[i][0]) + abs( y - p[i][1] ) ){
                    min = abs(x - p[i][0]) + abs( y - p[i][1] ) ;
                    index = i ;
                }
            }
        }
        return index ;
    }
};
```
