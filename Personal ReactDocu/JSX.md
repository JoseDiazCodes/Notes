# JSX

    Created by React Devs and it's considered to be a flavor of JavaScript that looks a lot like HTML

### What does it allow us to do?

```js
ReactDOM.render(<h1>This is JSX</h1>, document.getElementById("root"));
```

- Allows us to write code this ^ opposed to this:

```js
const h1 = document.createElement("h1");
h1.textContent = "Hello world";
h1.className = "header";
console.log(h1);
```

### Classes

- Classes are written like `className=""` opposed to `class=""` which is seen in ordinary HTML

---

### Object Nature of React Elements

**This:**

```js
const element = <h1 className="header">This is JSX</h1>;
console.log(element);
```

**Is essentially this:**

```js
/*
{
    type: "h1", 
    key: null, 
    ref: null, 
    props: {className: "header", children: "This is JSX"}, 
    _owner: null, 
    _store: {}
}
 */
```

- It returns an **OBJECT** _mind blown_

### It's just another Object

```js
const page = (
	<div>
		<h1 className="header">This is JSX</h1>
		<p>This is a paragraph</p>
	</div>
);

ReactDOM.render(page, document.getElementById("root"));
```

- The reason we can save the JSX into a variable and pass it through the `ReactDOM.render` as a parameter is because what we are getting back when we write and render JSX is just a Javascript.... **OBJECT!**

### Challenge:

- [x] Create a navbar in JSX:
  - Use the semantic `nav` element as the parent wrapper
  - Have an h1 element with the brand name of your "website"
  - Insert an unordered list for the other nav elements
    - Inside the `ul`, have three `li`s for "Pricing",
      "About", and "Contact"
  - Don't worry about styling yet - it'll just be plain-looking HTML for now

---

    My solution:

```js
let root = document.getElementById("root");

function Navbar() {
	return (
		<nav>
			<h1>Avenoir</h1>
			<ul>
				<li>Pricing</li>
				<li>About</li>
				<li>Contact</li>
			</ul>
		</nav>
	);
}

ReactDOM.render(<Navbar />, root);
```

---

    Actual solution from creator:

```js
const navbar = (
	<nav>
		<h1>Bob's Bistro</h1>
		<ul>
			<li>Menu</li>
			<li>About</li>
			<li>Contact</li>
		</ul>
	</nav>
);

ReactDOM.render(navbar, document.getElementById("root"));
```
