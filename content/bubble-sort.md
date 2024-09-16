---
Title: Bubble sort
---

> [!note]
> **Bubble  sort** is fairly easy  sorting algorithm it sorts by checking every
> adjacent item if one is bigger than the other and changing either way
> consistently throughout
> this means you can sort item ascending or descending by choosing which
> item(small, large) you want to put on the left

> [!WARNING]
> if this visualization doesn't show properly in you device please write an issue
> in GitHub until  i fix it don't try it with Mobile phones

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
> what if it is almost sorted or fully sorted? Think what would it do?

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
