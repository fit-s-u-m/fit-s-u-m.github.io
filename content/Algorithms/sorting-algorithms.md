---
title: Algorithms
---


An **algorithm** is a ==step by step== set of instructions or
a process used to solve a problem or perform a task.
</br>
just like a **cooking book**

When you learn about algorithms the first thing that comes to mind is
**sorting**.

Sorting is the process of arranging items in a specific order.

The ability to sort help in many ways:

> [!example] for e.g
> + **Searching**
> + **Remove duplication**
> + **Scheduling**

But most of the time when we learn **data-structures and algorithms**
we just visualize the algorithms in our mind
this is what makes the course a little bit harder then it should be.
Types of Sorting Algorithms

There are many sorting algorithms, each with different characteristics
in terms of speed and efficiency. The most common ones include:

1. **Bubble Sort** [[bubble-sort]]
    + **Description**: Bubble sort repeatedly steps through the list,
    compares adjacent elements, and swaps them if they are in the wrong order.
    This process is repeated until the list is sorted.
    + **Time Complexity**: $$O(n^2)$$ for average and worst cases, where n is
    the number of elements.
    + **Use Case**: Simple to understand but inefficient for large datasets.
    Mostly used for educational purposes.

2. **Insertion Sort** [[insertion-sort]]
    + **Description**: Insertion sort builds the sorted list one element at a
    time by repeatedly picking the next element and inserting it into its correct
    position within the sorted part.
    + **Time Complexity**: $$O(n^2)$$.
    + **Use Case**: Good for small datasets or datasets that are almost sorted.
    Simple to implement.

3. **Selection Sort** [[selection-sort]]
    + **Description**: Selection sort finds the smallest element in the list
    and swaps it with the first element.This process is repeated for each
    subsequent element until the entire list is sorted.
    + **Time Complexity**: $$O(n^2)$$.
    + **Use Case**: Easy to implement but not suitable for large datasets due to
    its inefficiency.
4. **Merge Sort**
    + **Description**: Merge sort is a divide-and-conquer algorithm.
    It divides the array into two halves, recursively sorts them,
    and then merges the sorted halves back together.
    + **Time Complexity**: $$O(n log n)$$ for both average and worst cases.
    + **Use Case**: Efficient for large datasets and maintains stable sorting
    (preserves the order of equal elements).

5. **Quick Sort**
    + **Description**: Quick sort also uses divide-and-conquer but
    selects a pivot element and partitions the dataset such that elements
    smaller than the pivot are moved to the left, and elements larger are moved to
    the right. The process is then repeated for the left and right sub-arrays.
    + **Time Complexity**: $$O(n log n)$$ on average but $$O(n^2)$$
    in the worst case.
    + **Use Case**: Often faster than merge sort for large datasets but has
    poor performance in its worst case.

6. **Heap Sort**
   + **Description**: Heap sort first turns the list into a binary heap
   (a complete binary tree where the parent node is greater than or
   equal to the child nodes).It then repeatedly removes the largest element
   from the heap and rebuilds the heap until all elements are sorted.
   + **Time Complexity**: $$O(n log n)$$.
   + **Use Case**: Suitable for large datasets and guarantees $$O(n log n)$$ performance,
   but it is not stable.

7. **Radix Sort**
    + **Description**: Radix sort processes integers by sorting digits starting
    from the least significant digit to the most significant one. It is a
    non-comparative sorting algorithm that uses another sorting algorithm
    (like counting sort) as a subroutine.
    + **Time Complexity**: $$O(nk)$$, where n is the number of elements and
    k is the number of digits.
    + **Use Case**: Efficient for sorting large numbers of integers with the same
    number of digits.

> [!info]
> [This](https://fit-s-u-m.github.io/Algorithms-visualized/)
> is my way of trying to visualize some of the sorting algorithms i have learned.

+ [Algorithms-visualized](https://fit-s-u-m.github.io/Algorithms-visualized/)
