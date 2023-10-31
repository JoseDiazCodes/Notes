# CRUD Operations

CRUD stands for Create, Read, Update, and Delete. These are the four basic operations that can be performed on data in a database.

## Create

To add new data. Example in SQL:

```sql
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
```

## Read

To retrieve data. Example in SQL:

```sql
SELECT * FROM table_name WHERE condition;
```

## Update

To modify existing data. Example in SQL:

```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```

## Delete

To remove data. Example in SQL:

```sql
DELETE FROM table_name WHERE condition;
```

# Call Stack and Global Execution Context in JavaScript

## Global Execution Context

When a JavaScript program starts, it enters the Global Execution Context by default. Any code that is not inside a function is executed in the global context.

Example:

```javascript
let a = "Hello, World!";
console.log(a); // This will run in the global execution context
```

## Call Stack

The call stack is a data structure that keeps track of function calls in your program. When a function is called, it is added to the stack. When the function finishes executing, it is removed from the stack. The JavaScript engine always executes the function that is on the top of the stack.

Example:

```javascript
function firstFunction() {
	console.log("First function");
}

function secondFunction() {
	firstFunction();
	console.log("Second function");
}

secondFunction();
```

In this example, the call stack would look like this:

1. `secondFunction` is called and added to the call stack.
2. Inside `secondFunction`, `firstFunction` is called and added to the top of the call stack.
3. `firstFunction` logs 'First function' and is removed from the call stack.
4. Execution returns to `secondFunction`, which then logs 'Second function' and is removed from the call stack.

Remember, the call stack works in a Last In, First Out (LIFO) manner.

# Execution Stack

The execution stack, also known as the call stack, is a stack data structure that stores information about the active functions/subroutines of a computer program. It keeps track of the function calls in the program, so that when a function returns, execution can pick up where it left off in the calling function.

# Event Loop

JavaScript has a single-threaded non-blocking asynchronous concurrent programming model, which is implemented through the event loop. The event loop continuously checks the message queue for messages. If it finds one, it adds the message's callback function to the call stack for execution. If the call stack is not empty, the event loop waits until it is.

Example:

```javascript
console.log("First");

setTimeout(function () {
	console.log("Second");
}, 0);

console.log("Third");
```

Even though the `setTimeout` function has a delay of 0 milliseconds, 'Third' will be logged before 'Second'. This is because `setTimeout` puts its callback function into the message queue, and it has to wait until the call stack is empty before it gets executed.

# Image Example

You can add images using the following Markdown syntax:

```markdown
![Alt text](URL_TO_YOUR_IMAGE)
```

Replace `Alt text` with the alternative text for the image, and `URL_TO_YOUR_IMAGE` with the URL of your image.

Example:

```markdown
![Example GIF](https://example.com/path/to/your/image.gif)
```

That’s it! You can use this explanation in your README.md file for a clear and concise explanation of CRUD operations, the call stack, global execution context, the execution stack, the event loop in JavaScript, along with an example image.
