---
Title: Insertion sort
---

> [!note]
> **Insertion  sort** is very **natural** to think about.
> If I give you a bunch of cards to sort you are probably using Insertion sort
> You start by having one card on you left hard when you encounter a new card
> depending if it is greater of less than the card you have on your left hand
> you put it left of it or right of it. Every time you draw a card you **insert**
> it to the right place on your left hand.

<iframe src="https://fit-s-u-m.github.io/Algorithms-visualized/?algorithm=Insertion+Sort" width="100%" height="700px"></iframe>

It’s inspired by the way we often sort cards in our hands:
you take one card at a time and insert it into its correct
position among the cards you’ve already sorted.

1. **Start from the First Element**

    Treat the first element as a "sorted" section
    (since a single element is trivially sorted).
    Now, move to the next element.

2. **Insert Each New Element into Its Correct Position**

    For each new element (let’s call it the "key"), compare it to the elements in
    the "sorted" section (elements to its left).Shift all elements that are greater
    than the key one position to the right, making space for the key.
    Insert the key into its correct position in the sorted section.

3. **Repeat for All Elements**

    Move to the next element and repeat the insertion process until all
    elements are sorted.

In this example the card I have on my left hand are **sorted**
when we draw the next card we ask our self which is the right place for it
and put it there

| ![Insertion sort step 1](/images/insertion_sort_step1.svg) | ![Insertion sort step 2](/images/insertion_sort_step2.svg) | ![Insertion sort step 3](/images/insertion_sort_step3.svg) |
| --- | --- | --- |
| ![Insertion sort step 4](/images/insertion_sort_step4.svg) | ![Insertion sort step 5](/images/insertion_sort_step5.svg) | ![Insertion sort step 6](/images/insertion_sort_step6.svg) |
| ![Insertion sort step 7](/images/insertion_sort_step7.svg) | ![Insertion sort step 8](/images/insertion_sort_step8.svg) | |

You repeat this until there are no card unsorted card on the right

## Lets see how Insertion sort is done in code

```typescript
function insertionSort(arr:number[]):number[]{
     // For every item you draw
    for(let i=1;i<arr.length;i++){ // we start from 2nd element
        // Loop through the items and find it's place
        const currentCard = arr[i]
        let currentIndex = i
        for (let j = i - 1; j >= 0; j--) { // check sorted
            if (arr[j] > currentCard) {
              this.swap(arr, j, currentIndex)
              currentIndex = j  // it swaped with j
            }
        }
    }
    return arr
}
function swap(arr: number[], i: number, j: number): void {
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

Another  thing I want to talk about in insertion sort is ==direction==

## does sorting direction matter?

The sort answer is yes. Lets say you are assigned to sort the ==buying power of
Ethiopian birr in the last decade.==
We can know that it's mostly declining.In this case I can argue that choosing
insertion sort is better and faster.The data you have been give is predictable and
going in one direction.But don't rush and just use the previous formula we talked
about because as we talked you are getting mostly low value and low value are found
on the left hand side not on the right hand side. So maneuvering the card to the
right place takes time.

- let me show you pictorially

<image src="/videos/insertion_sort_wrong_way.gif" width=200>

| ![Step 1](/images/insertion_sort_wrong_way01.svg) | ![Step 2](/images/insertion_sort_wrong_way02.svg) | ![Step 3](/images/insertion_sort_wrong_way03.svg) | ![Step 4](/images/insertion_sort_wrong_way04.svg) |
| --- | --- | --- | --- |
| ![Step 5](/images/insertion_sort_wrong_way05.svg) | ![Step 6](/images/insertion_sort_wrong_way06.svg) | ![Step 7](/images/insertion_sort_wrong_way07.svg) | ![Step 8](/images/insertion_sort_wrong_way08.svg) |
| ![Step 9](/images/insertion_sort_wrong_way09.svg) | ![Step 10](/images/insertion_sort_wrong_way010.svg) |   |   |

But if you know it's mostly low values you can just reverse the direction you
are sorting to check from the left side to right.If we have checked from starting
5 we would have got the right place for 4 easily.

Using generator function I have talked about it in [[bubble-sort]] and [[FuncitonalProgamming/generatorFunction]]

Here is the end code for it.Implementing this by changing direction for sorting
is left as an exercise for the reader.

```typescript
interface returnType {
    arr: number[]
    swapped: boolean
    highlightIndex: { i: number, j: number }
}
function insertionSort(arr: number[]): Iterator<returnType> {
    if (arr.length < 2) // already sorted case
      return { arr, highlightIndex: {i:-1,j:-1}, swaped: false }
    for (let i = 1; i < arr.length; i++) {
      const currentCard = arr[i]
      let currentIndex = i
      for (let j = i - 1; j >= 0; j--) { // check sorted cards
        const currentSortCard = arr[j]
        if (currentSortCard > currentCard) {
          this.swap(arr, j, currentIndex)
          currentIndex = j  // it swapped with j
         yield { arr, highlightIndex: {i,j}, swaped: true }
        }
        else { // it is in the right spot 
          yield { arr, highlightIndex: {i,j}, swaped: false }
          break
        }
      }
    }
    yield { arr, highlightIndex: {i:-1,j:-1}, swaped: false }
}

function swap(arr: number[], i: number, j: number) {
    let temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
}
```
