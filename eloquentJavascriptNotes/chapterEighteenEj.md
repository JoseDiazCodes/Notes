# Chapter Eighteen Eloquent JS: HTTP and Forms

## Overview

- The chapter delves into the world of the **HTTP protocol** and how it enables web pages to communicate with web servers.
- **Forms** provide a method for users to send data to the server.

## The Protocol

- **HTTP** stands for HyperText Transfer Protocol.
- It's a protocol that dictates how requests for web content and responses to those requests should be formatted and transmitted.

### Example:

An HTTP request might look like:

```
GET /path/file.html HTTP/1.0
```

An HTTP response might look like:

```
HTTP/1.1 200 OK
Date: Sun, 18 Oct 2009 08:56:53 GMT
Server: Apache/2.2.14 (Win32)
Content-Length: 88
Content-Type: text/html
Connection: Closed
```

## URLs

- Stands for **Uniform Resource Locators**.
- It provides a way to access the desired web page or resource.

### Example:

A typical URL:

```
https://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#somewhere
```

## Methods

- **HTTP methods** dictate the kind of request being made.
- Common methods: `GET`, `POST`, `DELETE`, `PUT`, and more.

### Example:

A `POST` request might be used when submitting form data:

```javascript
fetch("https://api.example.com/data", {
	method: "POST",
	body: JSON.stringify(data),
});
```

## Status Codes

- HTTP responses come with **status codes** that give information about the result of the request.
- Examples: `200 OK`, `404 Not Found`, `500 Internal Server Error`.

## Fetch

- The **fetch** function provides a promise-based way to make HTTP requests from JavaScript.

### Example:

Making a simple fetch request:

```javascript
fetch("https://api.example.com/data")
	.then((response) => response.json())
	.then((data) => console.log(data))
	.catch((error) => console.error("Error:", error));
```

## Forms

- HTML **forms** are a way to collect input from users.

### Example:

Basic HTML form:

```html
<form action="/submit-data" method="post">
	<label for="name">Name:</label>
	<input type="text" id="name" name="name" /><br /><br />
	<input type="submit" value="Submit" />
</form>
```

## Handling Forms in JavaScript

- JavaScript can be used to handle form submissions and process data.

### Example:

Listening to a form submission:

```javascript
document.querySelector("form").addEventListener("submit", (event) => {
	event.preventDefault();
	let formData = new FormData(event.target);
	// Process formData or send it to server
});
```

## XMLHttpRequest

- An older way to make HTTP requests in JavaScript.

### Example:

Making a request with **XMLHttpRequest**:

```javascript
let xhr = new XMLHttpRequest();
xhr.open("GET", "https://api.example.com/data", true);
xhr.onreadystatechange = function () {
	if (xhr.readyState == 4 && xhr.status == 200)
		console.log(JSON.parse(xhr.responseText));
};
xhr.send();
```

## Key Takeaways

- HTTP is the backbone protocol of the web, defining how data should be transferred.
- Forms provide a means to gather input and send it to servers.
- Fetch and XMLHttpRequest are ways to make HTTP requests in JavaScript.
- Understanding HTTP methods, status codes, and URLs is essential for web development.
