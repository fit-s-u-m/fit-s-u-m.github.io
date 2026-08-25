---
Title: Generator-Function
---
## What is Generator function ?

A Generator function is a function that allows you to get intermediate value
from the function before the function end's doing it's job
To put it more correctly it returns an Iterator that you can iterate over to get
it values underneath.

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

So the yield keyword pauses the execution and gives you the value at that
execution period.

> [!tip]
> By the way ,if you think about,
> programmers are often told that infinity is "bad"—but in this case,
> generator functions let us work with something close to infinity.
> Here is what i mean. In functional programming there is something called
> [[lazy evaluation]]  means the evaluation of expressions is delayed until their
> results are actually needed
> if you define infinite list it don't mind because he doesn't have to calculate
> it right away
> For example in the programming language **Haskell** you
> can define infinite list by `[1..]` (meaning 1 to infinity) then you could
> print out the first 10 by `[1...].take(10)` in this example yea you defined
> infinite list. This works because Haskell doesn't compute the entire list
> right away; it only evaluates up to the 10th element.
> You can do the same thing using generator functions.==Like defining infinite loops.==
> Believe me you need it.

Here's an example of a simple generator function that counts numbers starting
from 0:

```javascript
function* numberGenerator() {
    let count = 0;
    // this works because it doesn't compute the whole sequence at once
    while (true) {  // infinite loops
        yield count;
        count++;
    }
}

const myGenerator = numberGenerator();
console.log(myGenerator.next().value); // Output: 0
console.log(myGenerator.next().value); // Output: 1
console.log(myGenerator.next().value); // Output: 3
```

In this example, `numberGenerator()` is a generator function that generates numbers
starting from 0 and continues indefinitely as long as we call the `next()` method
on its returned iterator object, `myGenerator`.This is called lazy evaluation
it evaluate the computation only when asked to compute(when needed).

```javascript
function* numberGenerator() {
    let count = 1; // starting value
    while (true) {
        yield count;
        count++;
    }
}

function take(n){
    const myGenerator = numberGenerator();
    for(let i =0; i < n; i++){
        const { value } = myGenerator.next(); // Destructure to get the yielded value
        console.log(value); // Print the yielded value
    }
}
take(5) // prints 1 to 5
take(500) // prints 1 to 500
// like we saw before in the haskell programming language
```

Here we saw simple thing counting but the generator function can be Fibonacci sequence

```javascript
function* fibonacciGenerator() {
    let a = 0, b = 1; // Starting values for the Fibonacci sequence
    while (true) {
        yield a; // Yield the current Fibonacci number
        [a, b] = [b, a + b]; // Update a and b for the next Fibonacci number
    }
}

function take(n) {
    const fibGen = fibonacciGenerator();
    for (let i = 0; i < n; i++) {
        console.log(fibGen.next().value); // Print the next Fibonacci number
    }
}

// prints the first 10 Fibonacci numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34
take(10); 
```
