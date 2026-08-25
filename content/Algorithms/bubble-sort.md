---
Title: Bubble sort
---

> [!note]
> **Bubble  sort** is fairly **easy**  sorting algorithm,
> Bubble Sort is called "bubble" because larger elements tend to "bubble up"
> to the top of the list as they are swapped. This process is repeated until no further swaps are needed, indicating that the list is sorted.

> [!info]
> It works by repeatedly comparing each pair of adjacent items
> and swapping them if they are in the wrong order. By consistently
> applying this process in one direction, you can sort items in ascending
> or descending order, depending on whether you choose to place the smaller
> or larger item on the left in each comparison.

<iframe src="https://fit-s-u-m.github.io/Algorithms-visualized/" width="100%" height="700px"></iframe>

> [!tip]
> ==decrease the speed== to 1 and see how the sorting works slowly

As you can see when it first come since it checks all adjacent items
and move the largest of the two to the right this make it seem like
we are  pushing the largest(max) item to the right and in the next
round it does the same but this time it pushes the 2nd largest item
to the right and so on this is exactly why it is called bubble sort
because of the way elements "bubble up" the largest item to one side at a time

But as you can see you can easily change for choosing the largest and
putting it to the right to make it choose the smallest and put it on
the left.This is left as an exercise for the reader

So starting at index 0 you check the first item with the second
if the first number is larger than the second you change the order of the two

| ![bubble sort step 1](/images/bubble_sort_step1.png)| ![bubble sort step 2](/images/bubble_sort_step2.png) |
| --- | --- |
|![bubble sort step 3](/images/bubble_sort_step3.png) | ![bubble sort step 4](/images/bubble_sort_step4.png)|

you repeat this until in the whole loop have no swap

## Let's code bubble sort

I choose typescript  because I'm the most familiar with it but you can
easily choose any language and the idea is the same

```typescript
function bubbleSort(arr:number[]):number[]{
     // Loop for every round
    for(let i=0;i<arr.length;i++){
        // Loop through the items
        for (let j = 0; j < arr.length - 1; j++) { // because we go up to j+1
            if (arr[j] > arr[j + 1]) {
                swap(arr, j, j + 1)
            }
        }
    }
}
function swap(arr, i, j) {
    let temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}

```

In the above code for every round it checks if arr[j] is greater than arr[j+1]
in that case it swap the items if not skip

But there is a big downside to the way we wrote the code above

> [!question]
> what if it is almost sorted or fully sorted? Think what would it do ?

The problem  with the previous code is even if it is sorted it tries to sort
it by going and checking every loop but ideally we if it is already sorted it
should detect it in the first round when it check the whole item

If it doesn't swap any item in the first round this means all
items are sorted because every item is in the right order to be swapped.

To account for the above fact we can have a variable called swapped at every
round it becomes false and if it becomes true when we swap item.

```typescript
function bubbleSort  (arr:number[]):number[]{
    let swaped = false
    do {
        swaped = false
        for (let j = 0; j < arr.length - 1; j++) { // because we go up to j+1
            if (arr[j] > arr[j + 1]) {
                swap(arr, j, j + 1)
                swaped = true
            }
        }
    } while (swaped)
    return arr
}

```

This code make that it have different stopping  criteria for sorted
and unsorted array

The other thing we could improve is **side effects**
we are given an array and manipulate that same array and give it back. But
what we are really doing is removing previous value of the array and
writing the new sorted date there. What  we actually want to do is take
an array and return a brand new array with out manipulating the previous one.
Like array.map does in js for example.

```typescript
function bubbleSort(arr: number[]): number[] {
    // Create a copy of the input array to avoid modifying the original
    let sortedArray = [...arr];
    let swapped: boolean;

    do {
        swapped = false;
        for (let j = 0; j < sortedArray.length - 1; j++) { 
            if (sortedArray[j] > sortedArray[j + 1]) {
                swap(sortedArray, j, j + 1);
                swapped = true;
            }
        }
    } while (swapped);

    return sortedArray; // Return the sorted copy
}

function swap(arr: number[], i: number, j: number) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

One final improvement we can do is since we sort one item per round we don't
have to check for swap until the left corner we can stop the swap much sooner
by every round check for sorting one less then before

in the **first** round we check every item in the array until `arr.length`

in the **second** round we check until `arr.length -1`
// since the last item is already sorted

in the **third** round we check until `arr.length -2`
// since the last two item is already sorted

in the **nth** round we check until `arr.length - (n-1)`
and so on

```typescript
function bubbleSort(arr: number[]): number[] {
    // Create a copy of the input array to avoid modifying the original
    let sortedArray = [...arr];
    let swapped: boolean;
    let round = 0

    do {
        swapped = false;
        // sortedArray.length - 1 -(round -1) == sortedArray.length - 1 - round +1
        for (let j = 0; j < sortedArray.length -round; j++) { 
            if (sortedArray[j] > sortedArray[j + 1]) {
                swap(sortedArray, j, j + 1);
                swapped = true;
            }
        }
        round ++
    } while (swapped);

    return sortedArray; // Return the sorted copy
}

function swap(arr: number[], i: number, j: number) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

==One last optimization== you can do is each time we perform a full pass through the array,
the *last position we swapped is actually the boundary of our unsorted section*.
**This allows us to skip comparing any elements beyond this** index in subsequent passes.
By tracking the last swapped position, we can avoid comparisons for elements
that are already sorted.

```typescript
function bubbleSort(arr: number[]): number[] {
    let sortedArray = [...arr];
    let n = sortedArray.length;

    while (n > 1) {
        let lastSwappedIndex = 0;
        for (let j = 0; j < n - 1; j++) {
            if (sortedArray[j] > sortedArray[j + 1]) {
                swap(sortedArray, j, j + 1);
                lastSwappedIndex = j + 1;
            }
        }
        n = lastSwappedIndex;
    }

    return sortedArray;
}

function swap(arr: number[], i: number, j: number) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

```

This is all if you want to get only the last return result
correct but **what I did for the illustration above is not this** what
I actually need is to to yield the results in the middle like when it swap.
And you don't want to write the visualization in the sorting algorithm
it self.

## Why the need to separate visualizing and implementing sorting Algorithm ?

There are **two** reasons for it

- To use the visualization again and again (for different sorting algorithms)
  - ![duplicate code step 1](/images/duplicate-code-01.png)
  - ![duplicate code step 2](/images/duplicate-code-02.png)
  - ![duplicate code step 3](/images/duplicate-code-03.png)

- For **testing** the sorting Algorithm
  - To separate bugs occurring in visualization process and sorting algorithms

In JavaScript their is interesting function called  **Generator function**.

## What is Generator function ?

![[FuncitonalProgamming/generatorFunction]]

>[!question]
> How does Generator function solve our problem ?

Instead of returning at the end you yield values while computing other iteration.

```typescript

interface returnType {
    arr: number[]
    swapped: boolean
    highlightIndex: { i: number, j: number }
}

// watch for the asterisk here
function* bubbleSort(arr: number[]): Iterator<returnType> {
    // Create a copy of the input array to avoid modifying the original
    let sortedArray = [...arr];
    let swapped: boolean = false;
    let round = 0

    do {
        // sortedArray.length - 1 -(round -1) == sortedArray.length - 1 - round +1
        for (let j = 0; j < sortedArray.length - round; j++) {
            if (sortedArray[j] > sortedArray[j + 1]) {
                swap(sortedArray, j, j + 1);
                swapped = true;
            }
        yield {
            arr: sortedArray, swapped, highlightIndex: { i: j, j: j + 1 }
             }
        }
        round++
        swapped = false;
    } while (swapped);
}

function swap(arr: number[], i: number, j: number) {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

Instead of returning the last value you can return the intermediate value
then using that we can visualize it.
