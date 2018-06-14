---
title: Fenwick Tree
---

## Fenwick Tree

This article assumes that you have a basic knowledge of algorithm time complexity analysis, Javascript programming and the binary number system.

The Fenwick Tree, also known as a Binary Indexed Tree, is an efficent data structure that speeds up specific operations - primarily range sum queries and point updates. Fear not if you do not understand what are these operations and what they do! They will be explained succintly in the next section. 

Before we see an implementation of the Fenwick Tree, let us understand why us programmers would want to use a Fenwick Tree in the first place. We can construct a simple problem (usually faced by some programmers in some context) to understand why Fenwick Trees are so important.

## Problem Statement
Write a data structure to efficently support two operations, each with a time complexity of O(log n).

1) The sum from index i to index j
2) Adding a value v to index i.

The former operation is called range sum queries (RSQ) because we are trying to get a sum over a range while the latter is called point update (PU) as we are only updating an element at one point.

### Example

![diasbd](https://user-images.githubusercontent.com/19306879/41423751-c08291de-702e-11e8-979e-647992ad3aba.PNG)

Suppose you have an array (0-indexed) as such above, and now this sequence of operations follows:

1) RSQ from index 0 to index 5: 60
2) RSQ from index 1 to index 3: 15
3) RSQ from index 4 to index 5: 33
4) (PU) Add a value of 6 to index 1

![isbidasd](https://user-images.githubusercontent.com/19306879/41423988-58470eb4-702f-11e8-9dcc-3b058dad80b6.PNG)

5) RSQ from index 0 to index 5: 66
6) (PU) Add a value of 4 to index 2
6) RSQ from index 1 to index 3: 23
7) RSQ from index 4 to index 5: 33

I hope you understand RSQ and PU operations now. Now imagine if you have a large amount of data and have to perform these operations a lot of times. The PU operation will take O(1) constant time as the PU operation only consists of accessing and updating a single element, hence is efficent enough. However, the problem lies in the RSQ operation. By iterating through a range, the RSQ operation has an average time complexity of O(n), which may not be efficent enough. 

This is where the Fenwick Tree comes in, where both the PU and RSQ operations take O(log n) each. Though the PU operation becomes a bit less efficent, the difference in efficency will become negligible as the input size gets larger. One can easily observe this in a logarithmic graph, where the y-value grows slower and slower as the x-value increases. Furthermore, the best part is that the RSQ takes O(log n) as well, which is a good thing!

## How Fenwick Tree Works

The basic building block of a Fenwick Tree is the *least significant one-bit* operation. Let's explain what that operation is first before moving on.

### Quick Excercise

```javascript
00000001011
```

Q: How many zeroes are there to the rightmost one-bit?

A: 0. This is because the rightmost one-bit is all the way at the end and hence there are no zeroes after the rightmost one-bit.

```javascript
00001010000
00000001100
```

For the above two binary numbers, the answer is 4 and 2.

This is basically the essence of the *least significant one-bit* operation. And turns out that is there is a nifty way of getting the least significant one-bit of any number. 

```javascript
var x = 10;

// bit stores the least significant bit of the integer x.
var bit = x & (-x);
```

We will define the least significant one-bit of every integer x as LS(x);

Now we can construct a modified prefix sum array, where at every index i of the fenwick tree, we store the sum from the index i-{2^[LS(i)]}+1 to the index i of the array. 

![meme](https://user-images.githubusercontent.com/19306879/41426265-af34b82e-7035-11e8-99fe-9b49eb673a1c.jpg)

We shall use diagrams to simplify things. Meanwhile, I recommend taking a break; we're about halfway done!





### Sources / Credits

1. [Fenwick, Peter. "A New Data Structure for Cumulative Frequency Tables" June 7, 1993. Accessed: June 14, 2018](https://pdfs.semanticscholar.org/769f/b8055fbe0997ef8d9dab6c9abf37489c6575.pdf)
2. [What does that mean?! Meme](https://vignette.wikia.nocookie.net/animal-jam-clans-1/images/2/2f/1a4e5b80c15cc5da929dee6ccad878c1_meme-means-what-what-does-memes-mean_460-300.jpeg/revision/latest?cb=2017041503505)

