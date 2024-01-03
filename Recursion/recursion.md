# Recursion Explanation and Example

Recursion is a programming technique where a function calls itself to solve a problem. A recursive function typically has two cases: the base case and the recursive case.

## The Recursive Process

- The **base case** is the simplest instance of the problem, which can be solved directly without recursion.
- The **recursive case** breaks the problem down into smaller instances of the same problem, calling itself with different arguments.

## Factorial Function

Here's a simple JavaScript implementation of the factorial function using recursion:

```javascript
function factorial(n) {
	// base case
	if (n === 0) {
		return 1
	}
	// recursive case
	return n * factorial(n - 1)
}
```

## How Recursion Works

Let's go through how `factorial(5)` would be processed:

1. **Initial Call** - `factorial(5)`

   - Waits for `factorial(4)`

2. **Recursive Call 1** - `factorial(4)`

   - Waits for `factorial(3)`

3. **Recursive Call 2** - `factorial(3)`

   - Waits for `factorial(2)`

4. **Recursive Call 3** - `factorial(2)`

   - Waits for `factorial(1)`

5. **Recursive Call 4** - `factorial(1)`

   - Waits for `factorial(0)`

6. **Base Case Reached** - `factorial(0)`

   - Returns `1` directly

7. **Unwinding the Stack**
   - `factorial(1)` gets the result from `factorial(0)` and returns `1 * 1`
   - `factorial(2)` gets the result from `factorial(1)` and returns `2 * 1`
   - `factorial(3)` gets the result from `factorial(2)` and returns `3 * 2`
   - `factorial(4)` gets the result from `factorial(3)` and returns `4 * 6`
   - `factorial(5)` gets the result from `factorial(4)` and returns `5 * 24`

At each step, each function call waits for the result from its recursive call before it can return its value.

## Call Stack Visualization

Here is a visualization of the call stack at each step for `factorial(5)`:

```
factorial(5)
  5 * factorial(4)
    4 * factorial(3)
      3 * factorial(2)
        2 * factorial(1)
          1 * factorial(0)
            return 1
          return 1
        return 2
      return 6
    return 24
  return 120
```

When `factorial(5)` is called, it ends up performing `5 * 4 * 3 * 2 * 1` through the series of recursive calls and returns `120`.

## Conclusion

Recursion allows us to write cleaner and more concise code for problems that can be broken down into smaller, similar subproblems. It's essential, however, to have a base case to prevent infinite recursion and eventual stack overflow.

#### Codewars

```tx
In mathematics, the factorial of a non-negative integer n, denoted by n!, is the product of all positive integers less than or equal to n. For example: 5! = 5 * 4 * 3 * 2 * 1 = 120. By convention the value of 0! is 1.

Write a function to calculate factorial for a given input. If input is below 0 or above 12 throw an exception of type ArgumentOutOfRangeException (C#) or IllegalArgumentException (Java) or RangeException (PHP) or throw a RangeError (JavaScript) or ValueError (Python) or return -1 (C).

More details about factorial can be found here.
```

```js
function factorial(n) {
	// 5
	// base cases

	if (n < 0 || n > 12) {
		throw new RangeError("Invalid value for n")
	}

	if (n === 0) {
		return 1
	}

	return n * factorial(n - 1)

	// factorial(5) * factorial(4)...

	// facotrial(4) * factorial(3)

	// factorial(3) * factorial(2)

	// factorial(2) * factorial(1)

	// factorial(1) * factorial(0)

	// factorial(0) return 1

	// n! === n * (n-1)
}

// factoral
// recurison due to the subproblem nature of the problem where I have to use the product of one answer to get another.
```

> Recursion inherently uses the Last In, First Out (LIFO) principle because of the way function calls are managed in the call stack.

> When a recursive function is called, each call to the function is added to the call stack, and each of these calls waits for the next one to complete. As each call completes, it gets removed from the stack in the reverse order that they were put in—meaning the last function call to be added to the stack is the first one to be completed and removed. This mirrors the behavior of a stack data structure, which operates strictly on LIFO principles.

> Here's a simple step-by-step illustration of how LIFO works with a recursive function:

> The initial call to the recursive function is made.
> If the base case is not met, the function calls itself with new arguments, and this call is placed on top of the call stack.
> Step 2 repeats, stacking calls until the base case is met.
> Once the base case is reached, it returns a value, which then allows the next call on the stack (the one that was waiting for this result) to complete.
> This process continues, with each call completing and being popped off the stack in the reverse order that they were added, until we get back to the initial call.
> This LIFO property ensures that recursion can manage the dependencies between the nested calls correctly, resolving them from the inside out.
