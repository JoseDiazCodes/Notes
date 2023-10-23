# Modern JavaScript Explained for Dinosaurs

### Link to Article:

`https://medium.com/the-node-js-collection/modern-javascript-explained-for-dinosaurs-f695e9747b70`

## The Birth of JavaScript

JavaScript was created to make web pages interactive. It started out simple but quickly evolved.

### Example: Early JavaScript Alert

```javascript
alert("Hello, World!");
```

## The jQuery Era

jQuery made it easier to handle events, create animations, and update the DOM.

### Example: DOM Manipulation with jQuery

```javascript
$("#button").click(function () {
	$(this).toggleClass("expanded").next(".content").slideToggle();
});
```

### Example: AJAX with jQuery

```javascript
$.get("/my/url", function (data) {
	// Do something with data
});
```

## Introduction of JavaScript Frameworks

Modern frameworks allow for the creation of reusable UI components.

### Example: A Basic Backbone.js View

```javascript
var TodoView = Backbone.View.extend({
	tagName: "li",
	render: function () {
		this.$el.html(this.model.get("text"));
		return this;
	},
});
```

## Enter Node.js

Node.js made it possible for JavaScript to be run on the server, making JS a full-stack language.

### Example: Simple Node.js Server

```javascript
var http = require("http");
http
	.createServer(function (req, res) {
		res.writeHead(200, { "Content-Type": "text/plain" });
		res.end("Hello World\n");
	})
	.listen(1337, "127.0.0.1");
console.log("Server running at http://127.0.0.1:1337/");
```

## The New Build Tools

Tools like Grunt, Gulp, and Webpack allow for optimization of assets.

### Example: Concatenate & Minify JS with Gulp

```javascript
var gulp = require("gulp");
var uglify = require("gulp-uglify");
var concat = require("gulp-concat");

gulp.task("scripts", function () {
	return gulp
		.src("src/js/**/*.js")
		.pipe(concat("all.js"))
		.pipe(uglify())
		.pipe(gulp.dest("dist/js"));
});
```

## ES6, Babel, and Transpiling

ES6 brought new syntax and capabilities. Babel lets us use ES6 features while maintaining compatibility.

### Example: ES6 Arrow Function

```javascript
[1, 2, 3].map((n) => n + 1);
```

## Package Managers

NPM became the largest software registry in the world, allowing easy management of JS libraries.

### Example: Installing a Package with NPM

```bash
npm install lodash
```

## Conclusion & Key Takeaways

- **The JavaScript Landscape Has Evolved**: The journey from simple scripts to full-blown frameworks has transformed web development.
- **Tools Streamline and Enhance Development**: With build tools and transpilers, developers can optimize for performance and use the latest language features.
- **Node.js Unified the JavaScript Ecosystem**: By extending JavaScript to the server, Node cemented JS's role in the full web development stack.
- **The Importance of Staying Updated**: While the evolution of tools and practices might seem overwhelming, it's vital for developers to stay informed to build efficient and modern web applications.
