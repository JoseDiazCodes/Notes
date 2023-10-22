# Node.js Deep Dive

## Overview

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It is designed for building scalable network applications and can execute JavaScript code server-side. This has paved the way for creating web servers and networking tools using JavaScript and a collection of "modules" that handle various core functionalities.

## Features of Node.js

- Asynchronous and Event Driven: All APIs of Node.js are asynchronous, meaning they are non-blocking.
- Single-threaded but Scalable: Uses a single-threaded model with event looping, making it lightweight and efficient.
- No Buffering: Node.js cuts down the processing time while uploading audio and video files. It outputs the data in chunks.

## Understanding NPM (Node Package Manager)

NPM is the default package manager for Node.js. It lets developers install and manage application dependencies.

### Example:

#### Installing a package:

```bash
npm install express
```

#### Listing installed packages:

```bash
npm list --depth=0
```

#### Removing a package:

```bash
npm uninstall express
```

## Core Modules and File System

Node.js provides a set of built-in modules without having to install them using npm.

### Examples:

#### Reading a file:

```javascript
const fs = require("fs");
fs.readFile("example.txt", "utf8", (err, data) => {
	if (err) throw err;
	console.log(data);
});
```

#### Writing to a file:

```javascript
const fs = require("fs");
fs.writeFile("example.txt", "Hello, World!", (err) => {
	if (err) throw err;
	console.log("File has been saved!");
});
```

#### Appending to a file:

```javascript
const fs = require("fs");
fs.appendFile("example.txt", "\nAppended Text.", (err) => {
	if (err) throw err;
	console.log('The "Appended Text." was appended to file!');
});
```

## Event Loop and Concurrency Model

Node.js uses a single-threaded event loop model. The event mechanism helps the server to get a response from the non-blocking operation.

...

## Creating a Simple Server

To demonstrate Node's capabilities, creating a basic server is often a beginner's first step.

### Example:

```javascript
const http = require("http");
const server = http.createServer((req, res) => {
	res.writeHead(200, { "Content-Type": "text/plain" });
	res.end("Hello World\n");
});

server.listen(3000, "127.0.0.1", () => {
	console.log("Node server running on port 3000");
});
```

## Building a Simple Express Application

Express is a minimal and flexible Node.js web application framework.

### Example:

#### Setting up an Express server:

```javascript
const express = require("express");
const app = express();
const PORT = 3000;

app.get("/", (req, res) => {
	res.send("Hello, Express!");
});

app.listen(PORT, () => {
	console.log(`Server is running on http://localhost:${PORT}`);
});
```

#### Routing in Express:

```javascript
app.get("/about", (req, res) => {
	res.send("About Page");
});

app.post("/login", (req, res) => {
	res.send("Login successful!");
});
```

#### Middleware in Express:

Middleware functions have access to the request and response objects.

```javascript
app.use((req, res, next) => {
	console.log(`${req.method} ${req.originalUrl}`);
	next();
});
```

## Real-time Applications

Node.js is well-suited for real-time applications: chat applications, online gaming, etc.

...

## Key Takeaways

Node.js has revolutionized the way we think about web servers, making it possible to build fast, scalable, and efficient applications in JavaScript.
