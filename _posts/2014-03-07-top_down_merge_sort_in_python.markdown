---
layout: post
author: Jason Feng
title: Top Down Merge Sort in Python
date: '2014-03-07 10:49:00'
---

Merge Sort is one of the classic divide and conquer algorithm. 

Top-down mergesort uses between 1/2NlgN and NlgN compares to sort any array of length N. 
Top-down mergesort used at most 6NlgN array accesses to sort an array of length N. 

Following is sample code for top down mergesort 

```
 private ArrayList<integer> mergeSort(ArrayList<integer> inputArray) {
        int size = inputArray.size();
        if (size <= 1) {
            return inputArray;
        } else {
            int mid = size / 2;
            ArrayList<integer> left = new ArrayList<integer>();
            ArrayList<integer> right = new ArrayList<integer>();
            for (int i = 0; i < mid; i++) {
                left.add(inputArray.get(i));
            }
            for (int i = mid; i < size; i++) {
                right.add(inputArray.get(i));
            }
            left = mergeSort(left);
            right = mergeSort(right);
            return merge(left, right);
        }
    }

    private ArrayList<Integer> merge(ArrayList<integer> left,
                                     ArrayList<integer> right) {
        ArrayList<integer> result = new ArrayList<integer>();
        while (left.size() > 0 || right.size() > 0) {
            if (left.size() > 0 && right.size() > 0) {
                if (left.get(0) <= right.get(0)) {
                    result.add(left.get(0));
                    left.remove(0);
                } else {
                    result.add(right.get(0));
                    right.remove(0);
                    total = total + left.size();//this line is to get the total inversion
                }
            } else if (left.size() > 0) {
                result.add(left.get(0));
                left.remove(0);
            } else if (right.size() > 0) {
                result.add(right.get(0));
                right.remove(0);
            }
        }
        return result;
    }
```