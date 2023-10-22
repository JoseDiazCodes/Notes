# Chapter Eleven Eloquent JS: Asynchronous Programming

## Overview

- **Asynchronous Programming** is a means to handle operations that don't need to block the subsequent code from running.
- It provides a way to maintain performance, especially on tasks that might have waiting times, like reading from a file or making a network request.

## Callbacks

- A fundamental way to handle async operations. A function that gets called once an operation completes.

### Example:

File reading with a callback:

```javascript
const fs = require("fs");

fs.readFile("myfile.txt", "utf8", (err, data) => {
	if (err) throw err;
	console.log(data);
});
```

## Promises

- A promise represents a future value.
- Provides methods (`then`, `catch`, `finally`) to handle the eventual result.

### Example:

Creating and using a Promise:

```javascript
let myPromise = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve("Promise resolved");
	}, 2000);
});

myPromise
	.then((response) => console.log(response))
	.catch((error) => console.log(error))
	.finally(() => console.log("Promise completed"));
```

## async/await

- Elegant way to work with promises.
- Makes your asynchronous code look and behave a little more like synchronous code.

### Example:

Using async/await for file reading:

```javascript
const fs = require("fs").promises;

async function readMyFile() {
	try {
		const data = await fs.readFile("myfile.txt", "utf8");
		console.log(data);
	} catch (error) {
		console.error(`Got an error trying to read the file: ${error.message}`);
	}
}
readMyFile();
```

## Event Loop

- The secret behind JavaScript's asynchronous capabilities.
- Checks if the call stack is empty, then takes the first thing from the message queue and runs it.

### Example:

Understanding the order of execution:

```javascript
console.log("Start");
setTimeout(() => {
	console.log("Timeout callback");
}, 0);
console.log("End");
// Outputs: Start, End, Timeout callback
```

## Network Requests

- Making requests to fetch or send data to a server.

### Example:

Fetching data from a JSON API:

```javascript
fetch("https://api.example.com/data")
	.then((response) => response.json())
	.then((data) => console.log(data))
	.catch((error) => console.error("Error fetching data:", error));
```

## Error Handling

- Asynchronous operations are prone to errors, hence handling them is crucial.

### Example:

Handling errors in async/await:

```javascript
async function fetchData() {
	try {
		let response = await fetch("https://api.example.com/data");
		if (!response.ok) throw new Error(`HTTP error! Status: ${response.status}`);
		let data = await response.json();
		console.log(data);
	} catch (error) {
		console.error("Error fetching data:", error.message);
	}
}
fetchData();
```

## Concurrency

- Performing multiple asynchronous operations at the same time.

### Example:

Using `Promise.all`:

```javascript
let request1 = fetch("https://api.example.com/data1");
let request2 = fetch("https://api.example.com/data2");

Promise.all([request1, request2])
	.then((responses) => Promise.all(responses.map((r) => r.json())))
	.then((datasets) => console.log(datasets));
```

## Microtasks

- Tasks that are scheduled to run immediately after the currently running script.

### Example:

Using `Promise.resolve`:

```javascript
console.log("Start");
Promise.resolve().then(() => console.log("Microtask 1"));
console.log("End");
// Outputs: Start, End, Microtask 1
```

## Key Takeaways

- Asynchronous Programming is a powerful feature in JavaScript allowing non-blocking code execution.
- Understanding promises, callbacks, and async/await is essential for managing async operations.
- The event loop and message queue play a crucial role in executing asynchronous code.
- Proper error handling in async operations ensures robust applications.
