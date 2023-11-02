# React

```js
let root = document.getElementById("root");
ReactDOM.render(<h1>Hi my name is Jose Diaz</h1>, root);
```

- `ReactDOM.render()` takes in two parameters, the **first** being what will be placed inside of the dom.

- The **second** parameter being where you would like to place the element (in this case its the **div** with the id of **root**) [its specifically called a Dom Node that you we are selecting using the `document.getElementById("root")`]

---

### Practice Goal

- [x] Try and figure out how to render an `<ul>` with 2+ `<li>s` **inside**

```js
ReactDOM.render(
	<ul>
		<li>Born: Boston</li>
		<li>Age: 26</li>
	</ul>,
	root
);
```

---

## Why React?

    React allows us to rewrite composable code... (What does this mean?)

- Code that can be broken down into pieces and becomes more maintainable like building a car out of legos.

### Challenge:

> Create your own custom React component!
> Call it "MainContent", and have it return a simple
> h1 element that says "I'm learning React!"
>
> Afterward, render it below the Navbar (which you can do inside the ReactDOM.render call below)

```js
function Navbar() {
	return (
		<nav className="navbar navbar-expand-lg navbar-light bg-light">
			<a className="navbar-brand" href="#">
				Navbar
			</a>
			<button
				className="navbar-toggler"
				type="button"
				data-toggle="collapse"
				data-target="#navbarSupportedContent"
				aria-controls="navbarSupportedContent"
				aria-expanded="false"
				aria-label="Toggle navigation"
			>
				<span className="navbar-toggler-icon"></span>
			</button>

			<div className="collapse navbar-collapse" id="navbarSupportedContent">
				<ul className="navbar-nav mr-auto">
					<li className="nav-item active">
						<a className="nav-link" href="#">
							Home <span className="sr-only">(current)</span>
						</a>
					</li>
					<li className="nav-item">
						<a className="nav-link" href="#">
							Link
						</a>
					</li>
					<li className="nav-item dropdown">
						<a
							className="nav-link dropdown-toggle"
							href="#"
							id="navbarDropdown"
							role="button"
							data-toggle="dropdown"
							aria-haspopup="true"
							aria-expanded="false"
						>
							Dropdown
						</a>
						<div className="dropdown-menu" aria-labelledby="navbarDropdown">
							<a className="dropdown-item" href="#">
								Action
							</a>
							<a className="dropdown-item" href="#">
								Another action
							</a>
							<div className="dropdown-divider"></div>
							<a className="dropdown-item" href="#">
								Something else here
							</a>
						</div>
					</li>
					<li className="nav-item">
						<a className="nav-link disabled" href="#">
							Disabled
						</a>
					</li>
				</ul>
				<form className="form-inline my-2 my-lg-0">
					<input
						className="form-control mr-sm-2"
						type="search"
						placeholder="Search"
						aria-label="Search"
					/>
					<button
						className="btn btn-outline-success my-2 my-sm-0"
						type="submit"
					>
						Search
					</button>
				</form>
			</div>
		</nav>
	);
}

function MainContent() {
	return (
		<div className="mainContent">
			<h1 className="main">I'm learning React!</h1>
		</div>
	);
}

// added this MainContentFunction.

// Challenge: Create your own custom React component!
// Call it "MainContent", and have it return a simple
// h1 element that says "I'm learning React!"

// Afterward, render it below the Navbar (which
// you can do inside the ReactDOM.render call below)

ReactDOM.render(
	<div>
		<Navbar />
		<MainContent /> // added this
	</div>,
	document.getElementById("root")
);
```

## Why do people love React?

#### It's Declarative

- "What should be done?" - The computer/program will just wants to know what to do and you wont have to worry how it gets it done.

#### && It's Imperative

- "How it should be done?" - The computer/program wants to know exactly how to get something done.
- "Describe to me every step on how to do something, and I'll do it"
- Vanilla JS is imperative.

### Ex:

```js
const h1 = document.createElement("h1");
h1.textContent = "This is an imperative way to program using vanilla JS";
h1.className = "header";
document.getElementById("root").append(h1);
```
