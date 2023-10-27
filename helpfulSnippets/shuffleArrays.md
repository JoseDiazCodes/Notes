# Simplified Array Shuffling in JavaScript

This document provides a guide on how to shuffle an array in JavaScript using a simplified method, utilizing the `sort()` function with a random comparison function.

## Overview

The method revolves around the use of the `sort()` function in combination with a comparison function that returns a random value, effectively shuffling the array.

### The `Math.random()` Function

`Math.random()` generates a random decimal number between 0 (inclusive) and 1 (exclusive). Every call to this function returns a new random number.

### Shuffling Logic

The expression `0.5 - Math.random()` plays a crucial role in shuffling the array:

- **Positive Result:** If `Math.random()` returns a number less than 0.5, the result is positive.
- **Zero:** If `Math.random()` returns exactly 0.5 (which is extremely rare), the result is zero.
- **Negative Result:** If `Math.random()` returns a number greater than 0.5, the result is negative.

### How It Affects Sorting

- **Negative Number:** Tells the `sort()` function to place the first element before the second.
- **Zero:** Indicates that the two elements are equal, and no sorting is necessary.
- **Positive Number:** Instructs the `sort()` function to place the second element before the first.

### Code Example

```javascript
const cards = ["A", "A", "B", "B", "C", "C", "D", "D", "E", "E"];

function shuffle(array) {
	return array.sort(() => 0.5 - Math.random());
}

let shuffledCards = shuffle(cards);
console.log("Shuffled cards:", shuffledCards);
```

# Conclusion

> While this shuffling method is simple and concise, it's important to note that it doesn’t provide a uniform distribution, and certain sequences may be more likely to occur than others. This is usually fine for small arrays or less critical applications, but for situations where the quality of the shuffle is important (such as in cryptographic or gaming applications), a more robust algorithm like the Fisher-Yates (or Knuth) shuffle is recommended.
>
> This method provides a quick way to shuffle an array, making it a good option for rapid prototyping, learning exercises, or other non-critical use cases.
