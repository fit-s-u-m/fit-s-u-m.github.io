---
Title: Bubble sort
---

> [!note]
> **Bubble  sort** is fairly easy  sorting algorithm it sorts by checking every
> adjacent item if one is bigger than the other and changing either way
> consistently throughout
> this means you can sort item ascending or descending by choosing which
> item(small, large) you want to put on the left

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

Lets see how bubble sort is done in code
I choose type script  because I'm the most familiar with it but you can
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
it by going and checking every loop buy ideally we if it is already sorted it
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

This is all if you want to get only the last return result correct
but what I did for the illustration above is not this
what I actually need is to to yield the results in the middle like
when it swap.And if you don't want to write the visualization in the
sorting algorithm it self. Because the visualization have many sorting
algorithms implemented. I have to separate this.

In JavaScript their is interesting function called  **Generator function**.

>[!question]
> What is Generator function ?

A Generator function is a function that yields an iterator(which we gen each
value iteratively not getting when whole thing as one we get each yield at a time)
instead of a concrete result.

An Iterator is something that we can iterate over by calling the
next function.To think about it you can think it as a black box with cards inside
which have a single hole which you can insert you hand and take one card at a time.

> [!note]
> A Generator Function in JavaScript is a special type of function that is used
> to control the execution flow and produce values sequentially, instead of executing
> all code at once like a regular function.

A Generator function is a function  which allows pausing and resuming its execution
during runtime.Unlike regular function, which run to completion

A Generator function is identified by the presence of the `function*` syntax
and the use of the `yield` keyword, which acts as a pause point during
iteration. When a generator function is called, it does not execute immediately
like a regular function but returns an iterator object instead. The iterator object
has a method, such as `next()`, that can be called to continue the execution of the
generator function from where it left off, and optionally return a value.

So the yield keyword pauses the execution and gives you the value at that execution period.

Here's an example of a simple generator function that counts numbers starting
from 0:

```javascript
function* numberGenerator() {
    let count = 0;
    while (true) {
        yield count;
        count++;
    }
}

const myGenerator = numberGenerator();
console.log(myGenerator.next().value); // Output: 0
console.log(myGenerator.next().value); // Output: 1
```

In this example, `numberGenerator()` is a generator function that generates numbers
starting from 0 and continues indefinitely as long as we call the `next()` method
on its returned iterator object, `myGenerator`.This is called lazy evaluation
it evaluate the computation only when asked to compute(when needed).

>[!question]
> How does Generator function solve our problem ?

Instead of returning at the end you can yield when for every loop

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
