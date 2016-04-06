---
layout: post
author: Jason Feng
title: Simple Insertion Sort in Python
date: '2014-03-06 22:51:00'
---

Insertion sort is one of the basic sorting algorithm. It is much less efficient on large input compare to quicksort, merge sort. However, it also has several advantages: 

- Simple implementation (as show in code below) 
- Efficient for small input 
- Efficient than other quadratic algorithms, such as selection sort. 
- In place (only requires a constant amount of additional memory space) 

Here is the simple code of it: 

```
__author__ = 'jasonfungsing'


def insertionSort(input):
    print "Input: " + str(input)
    counter = 0
    size = len(input)
    for i in range(1, size):
        counter += 1
        key = input[i]

        j = i - 1
        while j >= 0 and input[j] > key:
            input[j + 1] = input[j]
            j -= 1
        input[j + 1] = key
        print str(counter) + " #: " + str(input)

    print "Output: " + str(input)
    return input


input = [5, 2, 4, 6, 1, 3]
insertionSort(input)
```