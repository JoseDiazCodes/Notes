# Chapter Six Eloquent JS Chapter 6

## Encapsulation

- Essentially is the bundling of data with the methods that operate on that data. This restricts direct access to some of an object's components and can prevent accidental modifications of data

### Examples

```js
let car = {
	make: "Toyota",
	model: "Camry",
	startEngine: function () {
		console.log("Engine started!");
	},
};
car.startEngine(); // Engine started!
```

```js
let bankAccount = {
	balance: 1000,
	deposit: function (amount) {
		this.balance += amount;
		console.log(`Deposited ${amount}. New balance: ${this.balance}`);
	},
};
bankAccount.deposit(200); // Deposited 200. New balance: 1200
```

## Methods

- Methods are functions that are stored as object properties

### Examples

```js
let dog = {
	name: "Buddy",
	bark: function () {
		console.log("Woof! Woof!");
	},
};
dog.bark(); // Woof! Woof!
```

- The bark property of the dog object has a method as the value.

```js
let calculator = {
	add: function (x, y) {
		return x + y;
	},
	subtract: function (x, y) {
		return x - y;
	},
};
console.log(calculator.add(5, 3)); // 8
console.log(calculator.subtract(5, 3)); // 2
```

- The calculator object has both add and subtract properties with functions corresponding to that operation as a method.

## Prototypes

- Prototypes are the mechanism by which JavaScript objects inherit features from one object to another.

### Examples

```js
let animal = {
	makesSound: true,
	sound: "Generic sound",
};
let cat = Object.create(animal);
cat.sound = "Meow";
console.log(cat.sound); // Meow
```

```js
function Dog(name) {
	this.name = name;
}
Dog.prototype.bark = function () {
	console.log(`${this.name} says woof`);
};
let dog1 = new Dog("Rex");
dog1.bark(); // Rex says woof
```

### Using Object.create();

- This piggy backs on Prototype Inheritance
- In JavaScript, the Object.create() method is used to create a new object and set its prototype to an existing object. This allows the new object to inherit all of the prototype properties and methods from the old object.

```js
const newObject = Object.create(oldObject);
```

### Example:

```js
// Define an object with a method
let person = {
	greet: function () {
		console.log("Hello!");
	},
};

// Create a new object that inherits from the person object
let student = Object.create(person);

// The student object can now use the greet method
student.greet(); // Outputs: "Hello!"
```

## Classes

- Classes are blueprints for creating objects shared properties and methods

```js
class MyObject {
	constructor(radius) {
		this.radius = radius;
	}
	area() {
		return Math.PI * this.radius * this.radius;
	}
}

let c = new Circle(5);
console.log(c.area());
```

```js
class Square {
	constructor(sideLength) {
		this.sideLength = sideLength;
	}
	area() {
		return this.sideLength * this.sideLength;
	}
}
let s = new Square(4);
console.log(s.area()); // 16
```

## Overriding Derived Properties

- properties in object can override the prototype properties within the prototype. properties can be inherited from the Objects prototype or it can have its own properties or methods.

### Examples

```js
function Bird(name) {
	this.name = name;
}
Bird.prototype.sound = "Tweet";
let parrot = new Bird("Polly");
parrot.sound = "Hello! Polly wants a cracker!";
console.log(parrot.sound); // Hello! Polly wants a cracker!
```

-- this essentially shows how you can override a Objects.prototype property if you reassign the same property with the same property name.

```js
// By default, JavaScript objects don't have a clear way to be represented as strings.
// The default `toString()` method for objects returns the generic "[object Object]".

let person = { firstName: "John", lastName: "Doe" };
console.log(person.toString()); // Output: [object Object]

// To provide a more meaningful string representation, we can override the `toString()` method.
// Here, we want the string representation of the `person` object to be the full name.

person.toString = function () {
	return this.firstName + " " + this.lastName;
};

console.log(person.toString()); // Output: John Doe
```

## Maps

- A **Map** holds key-value pairs. The keys can be any type of including functions and objects, and values can be any type

### Examples

```js
let map = new Map();
map.set("name", "Alice");
map.set("age", 25);
console.log(map.get("name")); // Alice
```

```js
let recipes = new Map([
	["pancake", ["flour", "milk", "egg"]],
	["omelette", ["egg", "milk", "salt"]],
]);
console.log(recipes.get("pancake")); // ["flour", "milk", "egg"]
```

## Polymorphism

- **Polymorphism** allows objects of different classes to be treated as instances of the same class through inheritance.

```js
class Shape {
	area() {
		return 0;
	}
}
class Rectangle extends Shape {
	constructor(width, height) {
		super();
		this.width = width;
		this.height = height;
	}
	area() {
		return this.width * this.height;
	}
}
class Circle extends Shape {
	constructor(radius) {
		super();
		this.radius = radius;
	}
	area() {
		return Math.PI * this.radius * this.radius;
	}
}
let shapes = [new Rectangle(10, 5), new Circle(5)];
for (let shape of shapes) {
	console.log(shape.area());
} // 50, 78.53981633974483
```

```js
class Animal {
	makeSound() {
		console.log("Some sound");
	}
}
class Dog extends Animal {
	makeSound() {
		console.log("Woof! Woof!");
	}
}
class Cat extends Animal {
	makeSound() {
		console.log("Meow");
	}
}
let pets = [new Dog(), new Cat()];
for (let pet of pets) {
	pet.makeSound();
} // Woof! Woof!, Meow
```

- Polymorph allows you to use methods from different classes in your code.
