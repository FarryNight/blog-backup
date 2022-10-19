---
title: LeetCodeDay2
author: Farry
img: 
top: 
cover: true
reprintPolicy: cc_by
date: 2022-09-29 22:25:14
tags: [c++,syntactic sugar]
categories: [Algorithms]
---
## Question

### Number of 1 Bits
uint32_t: unsigned int
<!-- more -->
https://en.wikipedia.org/wiki/Hamming_weight

need use operator & ^ ( or not ? )

1001
1000

1000

0111

0000

### Solution
``` bash
int hammingWeight(uint32_t n) {
        //uint32_t s = 0xffffffff ; //( n & s ) + ( n >> s ) 
        int count = 0 ;
        while ( n ){
            n &= ( n - 1 ) ;
            count++ ;
        }
        return count ;
        //return n ? 1 + hammingWeight(n & (n - 1)) : 0;
    }

//n &= ( n - 1 )
```
O(1)
n & (n - 1) drops the lowest set bit. It’s a neat little bit trick.

Let’s use n = 00101100 as an example. This binary representation has three 1s.

If n = 00101100, then n - 1 = 00101011, so n & (n - 1) = 00101100 & 00101011 = 00101000. Count = 1.

If n = 00101000, then n - 1 = 00100111, so n & (n - 1) = 00101000 & 00100111 = 00100000. Count = 2.

If n = 00100000, then n - 1 = 00011111, so n & (n - 1) = 00100000 & 00011111 = 00000000. Count = 3.

n is now zero, so the while loop ends, and the final count (the numbers of set bits) is returned.

from(https://leetcode.com/problems/number-of-1-bits/discuss/55255/C%2B%2B-Solution%3A-n-and-(n-1))
### Subtract the Product and Sum of Digits of an Integer
% can get value(last)
/ can get value(first)

### Solution
``` bash
int subtractProductAndSum(int n) {
        int sum , prod ;
        sum = n % 10 ;
        prod = n % 10 ;
        n /= 10 ;
        while ( n > 0 ){
            sum += n % 10 ;
            prod *= n % 10 ;
            n /= 10 ;
        }
        return prod - sum ;
    }
```