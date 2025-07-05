# Performance Comparison of Array Filtering Methods

This document compares the performance of various methods used to filter arrays in JavaScript. The measurements were taken on an array of 10,000 integers and report the observed execution times in milliseconds.

## Device specification:

Processor: 11th Gen Intel(R) Core(TM) i7-11370H @ 3.30GHz 3.30 GHz <br>
RAM: 16.0 GB <br>
System type: 64-bit operating system, x64-based processor <br>

```javascript
const even = arr.filter((num) => num % 2 === 0); // 1.4 - 2 ms

const even = arr.reduce((acc, num) => {
    // 1.0 - 1.5 ms
    if (num % 2 === 0) acc.push(num);
    return acc;
}, []);

const numbers = []; // 0.2 - 1 ms
arr.forEach((num) => {
    if (num % 2 === 0) numbers.push(num);
});

const numbers = []; // 1.5 - 3 ms
for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) numbers.push(arr[i]);
}

const evens = arr.flatMap((n) => (n % 2 === 0 ? [n] : [])); // 1.3 - 2.5 ms

function* genFilter(arr, pred) {
    // 1.7 - 3.5 ms
    for (const x of arr) {
        if (pred(x)) yield x;
    }
}
const evens = Array.from(genFilter(arr, (n) => n % 2 === 0));
```

# Summary of Performance

| Method                     | Observed Time (ms) |
| -------------------------- | ------------------ |
| **forEach + push**         | 0.2 – 1.0          |
| **`filter()`**             | 1.4 – 2.0          |
| **Array.prototype.reduce** | 1.0 – 1.5          |
| **for loop + push**        | 1.5 – 3.0          |
| **`flatMap()`**            | 1.3 – 2.5          |
| **Generator + Array.from** | 1.7 – 3.5          |

Note: Results may vary based on environment and JS engine optimizations.
