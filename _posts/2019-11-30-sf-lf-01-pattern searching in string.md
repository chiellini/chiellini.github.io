---
title: "Survey of pattern search"
subtitle: "Some algorithms for pattern searching"
layout: post
author: "chiellini(lizelin)"
header-style: text
catalog: true
tags:
  - 软件基础
  - Data Structure
  - 笔记

---

# Some traditional algorithms and innovative methods for pattern searching

```
Input:  txt[] = "THIS IS A TEST TEXT"
        pat[] = "TEST"
Output: Pattern found at index 10

Input:  txt[] =  "AABAACAADAABAABA"
        pat[] =  "AABA"
Output: Pattern found at index 0
        Pattern found at index 9
        Pattern found at index 12

The length of txt is N, the length of pat is N.
```

## Naive Algorithm

Just search from head to tail. And here is some situations:

- If there is no match pattern substring in string

```
txt[] = "AABCCAADDEE"; 
pat[] = "FAA";
```

in this situation, the number of comparisons in best case is O(N)

- Other situation(normal situation)

```
1) When all characters of the text and pattern are same.
  
  filter_none
  brightness_4
  txt[] = "AAAAAAAAAAAAAAAAAA"; 
  pat[] = "AAAAA";
2) Worst case also occurs when only the last character is different.
  
  filter_none
  brightness_4
  txt[] = "AAAAAAAAAAAAAAAAAB"; 
  pat[] = "AAAAB";
```

The number of comparisons in worst case if O(M*(N-M+1))

### KMP Algorithm(Knuth-Morris-Pratt) -- Partial Match Table

lps= longest prefix and suffix

- Pre-processing

  An important question arises from the match of only part of the pattern, how to know how many characters to be skipped. To know this, we pre-process pattern and prepare an integer array lps[] that tells us the count of characters to be skipped. 

  Pre-process the pattern is one of the most important part of KMP.

- Unlike Naive algorithm, where we slide the pattern by one and compare all characters at each shift, we use a value from lps[] to decide the next characters to be matched. The idea is to not match a character that we know will anyway match. That why time complexity of KMP can reach O(n) in the worst case.

#### Detailed processes

- We start comparison of pat[j] with j=0 with characters of current window of text
- We keep matching characters txt[i] and pat[j] and keep incrementing i and j while pat[j] keep matching.
- When we see a mismatch：
  - We know that characters pat[0...j-1] match with txt [i-j...i-1] (Note that j starts with 0 and increment it only there is a match)
  - We also know (from above definition) that lps[j-1] is count of characters of pat[0...j-1] that are both proper prefix and suffix
  - From above two points, we can conclude that we do not need to match these lps[j-1] characters with txt[i-j...i-1] because we know that these characters will anyway match.

simple example

```
txt[] = "AAAAABAAABA" 
pat[] = "AAAA"
lps[] = {0, 1, 2, 3} 

i = 0, j = 0
txt[] = "AAAAABAAABA" 
pat[] = "AAAA"
txt[i] and pat[j] match, do i++, j++

i = 1, j = 1
txt[] = "AAAAABAAABA" 
pat[] = "AAAA"
txt[i] and pat[j] match, do i++, j++

i = 2, j = 2
txt[] = "AAAAABAAABA" 
pat[] = "AAAA"
pat[i] and pat[j] match, do i++, j++

i = 3, j = 3
txt[] = "AAAAABAAABA" 
pat[] = "AAAA"
txt[i] and pat[j] match, do i++, j++

i = 4, j = 4
Since j == M, print pattern found and reset j,
j = lps[j-1] = lps[3] = 3

/*Here unlike Naive algorithm, we do not match first three 
characters of this window. Value of lps[j-1] (in above 
step) gave us index of next character to match.*/

i = 4, j = 3
txt[] = "AAAAABAAABA" 
pat[] =  "AAAA"
txt[i] and pat[j] match, do i++, j++

i = 5, j = 4
Since j == M, print pattern found and reset j,
j = lps[j-1] = lps[3] = 3

/*Again unlike Naive algorithm, we do not match first three 
characters of this window. Value of lps[j-1] (in above 
step) gave us index of next character to match.*/

i = 5, j = 3
txt[] = "AAAAABAAABA" 
pat[] =   "AAAA"
txt[i] and pat[j] do NOT match and j > 0, change only j
j = lps[j-1] = lps[2] = 2

=============core part==========>>>>>>>>>>>>>>>>>>>>>>>>
i = 5, j = 2
txt[] = "AAAAABAAABA" 
pat[] =    "AAAA"
txt[i] and pat[j] do NOT match and j > 0, change only j
j = lps[j-1] = lps[1] = 1 

i = 5, j = 1
txt[] = "AAAAABAAABA" 
pat[] =     "AAAA"
txt[i] and pat[j] do NOT match and j > 0, change only j
j = lps[j-1] = lps[0] = 0

i = 5, j = 0
txt[] = "AAAAABAAABA" 
pat[] =      "AAAA"
txt[i] and pat[j] do NOT match and j is 0, we do i++.
=============core part=======>>>>>>>>>>>>>>>>>>>>>

i = 6, j = 0
txt[] = "AAAAABAAABA" 
pat[] =       "AAAA"
txt[i] and pat[j] match, do i++ and j++

i = 7, j = 1
txt[] = "AAAAABAAABA" 
pat[] =        "AAAA"
txt[i] and pat[j] match, do i++ and j++

We continue this way...
```

The core process is build that lps array, and know why we can use this lps array to control the pattern index j. This is some regular expression like prefix and suffix.

#### Illustration of pre-processing

In the pre-processing part, we calculate values is lps[]. To do that, we keep track of **the length of the longest prefix and suffix**(we use len variable for this purpose) for the previous index. We initialize lps[0] and len as 0. If pat[len] and pat[i] match, we increment len by 1 and assign the incremented value to lps[i]. If pat[i] and pat[len] do not match and len is not 0, we update len to lps[len-1].

```
pat[]="AAACAAAA"

len=0,i=0.
lps[0] is always 0, we move to i=1

len=0, i=1.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] and do i++.
len =1, lps[1]=1, i=2

len=1, i=2.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] and do i++.
len =2, lps[2]=2, i=3

len=2, i=3.
Since pat[len] and pat[i] do not match, and len >0,
set len=lps[len-1]=lps[1]=1

len=1, i=3.
Since pat[len] and pat[i] do not match and len > 0,
set len=lps[len-1]=lps[0]=0

len=0,i=3.
Since pat[len] and pat [i] do not match and and len=0,
Set lps[3]=0 and i =4.
We know that characters pat

len=0,i=4.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] do i++.
len=1, lps[4]=1, i=5

len=1, i=5.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] and do i++.
len=2, lps[5]=2, i=6

len=2, i=6.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] and do i++.
len=3, lps[6]=3, i=7

len =3, i=7.
Since pat[len] and pat[i] do not match and len>0,
set len=lps[len-1]=lps[2]=2

len=2,i=7.
Since pat[len] and pat[i] match, do len++,
store it in lps[i] and do i++.
len=3, lps[7]=3, i=8

we stop and get the lps[]:
[0,1,2,0,1,2,3,2,3]
```



#### Understanding

**The lps[] demonstrate the inner relationship of pattern. You can imagine that if the pattern is "ABCD" OR "BLOCKCHAIN" such different string, you can easily recognize it and move the pattern window along the txt; we use lps[] as [0,0,0,0,0…]. But if there are lots of similar characters, we can't know whether current characters match before in this window. For an instance, pat[] is AAAC and txt[] is AAAAAAAAAC; if we start matching from first character of pat[], we can never get O(n) time comlexity to get correct result. **

**KMP is  a Dynamic Programming algorithm because of its lps[], a DP array. And KMP use lps[] array to avoid lots of useless computation in Naive Algorithm, which is an important feature of Dynamic Programming.**

**The most significant part of a successful Dynamic Programming is to find the State Transition Equation.**

**The lps[] is designed to support the state transition. **

#### Test your program

```
Examples of lps[] construction:
For the pattern “AAAA”, 
lps[] is [0, 1, 2, 3]

For the pattern “ABCDE”, 
lps[] is [0, 0, 0, 0, 0]

For the pattern “AABAACAABAA”, 
lps[] is [0, 1, 0, 1, 2, 0, 1, 2, 3, 4, 5]

For the pattern “AAACAAAAAC”, 
lps[] is [0, 1, 2, 0, 1, 2, 3, 3, 3, 4] 

For the pattern “AAABAAA”, 
lps[] is [0, 1, 2, 0, 1, 2, 3]
```

Reference link:

https://cloud.tencent.com/developer/article/1511699

https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/



### Rabin-Karp Algorithm

waiting to updates...