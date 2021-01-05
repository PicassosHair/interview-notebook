# Single Number

## Question List
136\. Single Number I \
137\. Single Number II \
260\. Single Number III


## Map Solution 
We can use `map (dictionary)` to solve **Single Number** issues. The `map` stores keys for numbers and values for the frequency. In the end, literal `map` to find the answer. 

**Leetcode 260**
```Python
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        
        dic = {}
        for num in nums:
            if num in dic:
                dic[num] += 1
            else:
                dic[num] = 1
        
        res = []
        for k,v in dic.items():
            if v == 1:
                res.append(k)
        
        return res
```

## Bitwise Solution

### Bitwise Operation 

#### x << y
Returns x with the bits shifted to the left by y places (and new bits on the right-hand-side are zeros). This is the same as multiplying x by 2**y.
#### x >> y
Returns x with the bits shifted to the right by y places. This is the same as //'ing x by 2**y.
#### x & y
Does a "bitwise and". Each bit of the output is 1 if the corresponding bit of x AND of y is 1, otherwise it's 0.
#### x | y
Does a "bitwise or". Each bit of the output is 0 if the corresponding bit of x AND of y is 0, otherwise it's 1.
#### ~ x
Returns the complement of x - the number you get by switching each 1 for a 0 and each 0 for a 1. This is the same as -x - 1.
#### x ^ y
Does a "bitwise exclusive or". Each bit of the output is the same as the corresponding bit in x if that bit in y is 0, and it's the complement of the bit in x if that bit in y is 1.

### Boolean algebra
- x | (x & y) = x
- x & (x | y) = x
- ~(x | y) = ~x & ~y
- ~(x & y) = ~x | ~y
- x | (y & z) = (x | y) & (x | z)
- x & (y | z) = (x & y) | (x & z)
- x & (y ^ z) = (x & y) ^ (x & z)
- x + y = (x ^ y) + ((x & y) << 1)
- x - y = ~(~x + y)

### Laws of Boolean Algebra Example 
```
Using the above laws, simplify the following expression:  (A + B)(A + C)

Q =	(A + B).(A + C)	 
 	A.A + A.C + A.B + B.C	 – Distributive law
 	A + A.C + A.B + B.C	     – Idempotent AND law (A.A = A)
 	A(1 + C) + A.B + B.C	 – Distributive law
 	A.1 + A.B + B.C	         – Identity OR law (1 + C = 1)
 	A(1 + B) + B.C	         – Distributive law
 	A.1 + B.C	             – Identity OR law (1 + B = 1)
Q =	A + (B.C)	             – Identity AND law (A.1 = A)
```

<br>

## Leetcode Problem
### Leetcode 136 <br>
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return reduce(lambda x, y: x^y, nums, 0)
```

### Leetcode 137 <br>
Given a non-empty array of integers, every element appears three times except for one, which appears exactly once. Find that single one.

#### Algorithm
a is the high bit. b is the low bit. c is the data. a' is the a's result. b' is the b's result.
|a|b|c|a'|b'|
|-|-|-|-|-|
|0|0|0|0|0|
|0|1|0|0|1|
|1|0|0|1|0|

|a|b|c|a'|b'|
|-|-|-|-|-|
|0|0|1|0|1|
|0|1|1|1|0|
|1|0|1|0|0|

b' = 1: `(a==0 && b==1 && c==0) || (a==0 && b==0 && c==1)` <br>
=> `b' = (~a & b & ~c) + (~a & ~b & c) = ~a & (b & ~c + ~b & c) = ~a & (b ^ c)` <br><br>
a' = 1: `(a==1 && b==0 && c==0) || (a==0 && b==1 && c==1)` <br>
=> `a' = (a & ~b & ~c) + (~a & b & c)` <br>
=> `a' = (~a & ~b' & c) + (a & ~b' & ~c) = ~b' & (~a & c + a & ~c) = ~b' & (a ^ c)`

#### Code
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        a, b = 0, 0
        for c in nums:
            b = (b ^ c) & ~a
            a = (a ^ c) & ~b
        return b
```

#### Reference
https://blog.csdn.net/qq_17550379/article/details/83926804
https://blog.csdn.net/jiangxiewei/article/details/82227451


### Leetcode 260
#### Code
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        
        diff = reduce((lambda x, y: x ^ y), nums)
        diff &= -diff

        first, second = 0, 0
        for num in nums:
            if diff & num:
                first ^= num
            else:
                second ^= num

        return [first, second]
```


#### Reference
https://leetcode.com/problems/single-number-iii/discuss/68901/Sharing-explanation-of-the-solution

