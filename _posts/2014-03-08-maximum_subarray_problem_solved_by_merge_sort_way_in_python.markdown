---
layout: post
author: Jason Feng
title: Maximum-subarray problem, solved by Merge Sort way, in Python
date: '2014-03-08 08:05:00'
---

The macinum-subarrray problem is the task of finding the contiguous subarray within a one-dimensional array of numbers (containing at least one positive number) which has the largest sum. For example, for array -3, 2, -5, 10, -2, 8, -8, 1, 4, the contiguous subarray with the largest sum is 10, -2, 8, with sum 16. 

The code below use the methodology of divide-and conquer. Take the origin input and divide into two small arrays and recursively check on half of the subarray. 

So, for each array, there are three possible combinations for the maximum subarray exists in: 
- this maximum subarray fully exist in the left half of the array 
- this maximum subarray fully exist in the right half of the array 
- this maximum subarray exist across the left half and the right half 

Now, the problem is more clear, as in case 1(fully in left half) and case 2(fully in right half), those two cases can be handle by recursively divide. The only problem left is to find out the case 3(across left and right half). 

![](/content/images/2016/03/Screen-Shot-2014-03-08-at-6-54-22-pm.png)

Here is the code to find the maximum crossing subarray for array 

```
def find_max_crossing_subarray(array, low, mid, high):
    left_sum = None
    sum1 = 0
    max_left = 0
    for i in range(mid, low - 1, -1):
        sum1 = sum1 + array[i]
        if None == left_sum:
            left_sum = sum1
            max_left = i
        elif sum1 > left_sum:
            left_sum = sum1
            max_left = i

    right_sum = None
    sum2 = 0
    max_right = 0
    for j in range(mid + 1, high + 1):
        sum2 = sum2 + array[j]
        if None == right_sum:
            right_sum = sum2
            max_right = j
        elif sum2 > right_sum:
            right_sum = sum2
            max_right = j

    return (max_left, max_right, left_sum + right_sum)
```
Then, all we need is to perform this recursively on the input. The full code as below 

```

__author__ = 'jasonfungsing'


def find_max_crossing_subarray(array, low, mid, high):
    left_sum = None
    sum1 = 0
    max_left = 0
    for i in range(mid, low - 1, -1):
        sum1 = sum1 + array[i]
        if None == left_sum:
            left_sum = sum1
            max_left = i
        elif sum1 > left_sum:
            left_sum = sum1
            max_left = i

    right_sum = None
    sum2 = 0
    max_right = 0
    for j in range(mid + 1, high + 1):
        sum2 = sum2 + array[j]
        if None == right_sum:
            right_sum = sum2
            max_right = j
        elif sum2 > right_sum:
            right_sum = sum2
            max_right = j

    return (max_left, max_right, left_sum + right_sum)


def find_max_subarray(array, low, high):
    mid = (low + high) / 2
    if high == low:
        return (low, high, array[low])
    else:
        (left_low, left_high, left_sum) = find_max_subarray(array, low, mid)
        (right_low, right_high, right_sum) = find_max_subarray(array, mid + 1, high)
        (cross_low, cross_high, cross_sum) = find_max_crossing_subarray(array, low, mid, high)

    if left_sum >= right_sum and left_sum >= cross_sum:
        return (left_low, left_high, left_sum)
    elif right_sum >= left_sum and right_sum >= cross_sum:
        return (right_low, right_high, right_sum)
    else:
        return (cross_low, cross_high, cross_sum)


array = [13, -3, -25, 20, -3, -16, -23, 18, 20, -7, 12, -5, -22, 15, -4, 7]
# array = [-3, 2, -5, 10, -2, 8, -8, 1, 4]
print str(find_max_subarray(array, 0, len(array)-1))
```