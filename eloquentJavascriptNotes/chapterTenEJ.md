# Chapter Ten Eloquent JS: Modules

## Overview

- **Modules** help manage and organize code, especially in larger programs.
- With ES6, JavaScript introduced its own system for modules.

## Use of Modules

- Modules prevent polluting the global namespace.
- They allow for better code structure and organization.

### Example:

Module for math operations:

```javascript
// mathOperations.js
export function add(a, b) {
	return a + b;
}

export function subtract(a, b) {
	return a - b;
}
```

## Importing and Exporting

Modules communicate via `import` and `export`.

### Examples:

1. Basic Import and Export:

```javascript
// utils.js
export function log(message) {
	console.log(message);
}

// main.js
import { log } from "./utils.js";
log("This is a log message from utils.");
```

2. Renaming during import:

```javascript
// utils.js
export function log(message) {
	console.log(message);
}

// main.js
import { log as displayLog } from "./utils.js";
displayLog("Displaying a log message from utils.");
```

## Building and Bundling

- Browsers now support modules via the `type="module"` attribute.
- Tools like **Rollup**, **Parcel**, and **Webpack** bundle multiple modules.

### Example:

Using **Webpack**:

```javascript
// webpack.config.js
module.exports = {
	entry: "./app/index.js",
	output: {
		filename: "bundle.js",
		path: __dirname + "/dist",
	},
};
```

## NPM (Node Package Manager)

- A repository for JavaScript packages.
- Utilizes `package.json` to manage dependencies.

### NPM Workings:

1. **Initialization**: Sets up a new project or existing one.

```bash
npm init
```

2. **Installing Packages**: Downloads packages and adds them to `node_modules` and `package.json`.

```bash
npm install lodash
```

3. **Using Packages**: After installation, you can utilize them in your project.

```javascript
import _ from "lodash";
let array = _.uniq([1, 2, 2, 3, 3, 3]);
console.log(array); // Outputs: [1, 2, 3]
```

4. **Package Versions**: Can specify version ranges for dependencies, ensuring compatibility.

5. **Scripts**: NPM can run scripts defined in `package.json`, aiding in tasks like testing or building.

## CommonJS

- Used before ES6 modules, especially in Node.js.
- Uses `require` for importing and `module.exports` for exporting.

### Example:

```javascript
// math.js
exports.add = function (a, b) {
	return a + b;
};

// main.js
const math = require("./math.js");
console.log(math.add(5, 3)); // Outputs: 8
```

## Designing a Module

1. Keep the interface minimal.
2. Reduce dependencies.
3. Focus on high-level functionalities.

## ECMAScript Modules (ESM)

- The standard module system for modern JavaScript.
- Static structure and asynchronous design.

### Example:

Dynamic imports:

```javascript
// On a button click, we might want to load a module conditionally.
button.addEventListener("click", async () => {
	const heavyModule = await import("./heavyModule.js");
	heavyModule.performTask();
});
```

## Key Takeaways

- Modules enhance code structure and organization.
- ES6 introduced a standardized module system.
- NPM, Webpack, and other tools aid in module management.
