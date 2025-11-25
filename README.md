# Modern JavaScript (ES6+) Features

A comprehensive guide to modern JavaScript syntax and features with practical examples.

## 📚 Table of Contents

- [Overview](#overview)
- [Arrow Functions](#arrow-functions)
- [Template Literals](#template-literals)
- [Destructuring](#destructuring)
  - [Array Destructuring](#array-destructuring)
  - [Object Destructuring](#object-destructuring)
- [Spread Operator](#spread-operator)
- [Rest Parameters](#rest-parameters)
- [For...of Loop](#forof-loop)
- [Classes and Objects](#classes-and-objects)
  - [Class Syntax](#class-syntax)
  - [Static Methods](#static-methods)
  - [Inheritance](#inheritance)
  - [Mixins](#mixins)
- [Prototypes](#prototypes)
- [Constructors](#constructors)

---

## Overview

This repository contains examples demonstrating modern JavaScript (ES6+) features. ES6 (ECMAScript 2015) introduced significant improvements to JavaScript, making code more readable, maintainable, and powerful.

**Files in this repository:**
- `es6.js` - Covers classes, inheritance, mixins, and arrow functions
- `modern.js` - Covers rest/spread operators, destructuring, template literals, prototypes, and constructors

---

## Arrow Functions

Arrow functions provide a concise syntax for writing function expressions. They also lexically bind the `this` value.

### Syntax

```javascript
// Traditional function
function sum(a, b) {
  return a + b;
}

// Arrow function
const sum = (a, b) => a + b;

// Single parameter (parentheses optional)
const namePrint = name => console.log(name);

// Multiple statements (requires curly braces and return)
const calculate = (a, b) => {
  const result = a + b;
  return result;
};
```

### Example from Code

```javascript
const sum = (a, b) => a + b;
console.log(sum(5, 6)); // Output: 11

const namePrint = (name) => console.log(name);
namePrint("Rider"); // Output: Rider
```

### Key Benefits
- Shorter syntax
- Implicit return for single expressions
- Lexical `this` binding (inherits `this` from surrounding scope)

---

## Template Literals

Template literals allow embedded expressions and multi-line strings using backticks (`` ` ``).

### Syntax

```javascript
const number = 5;
let str = `he
it's
ur
boy
!  his no is ${number}`;
console.log(str);
```

### Features
- **Multi-line strings**: No need for `\n` or string concatenation
- **String interpolation**: Embed expressions using `${expression}`
- **Tagged templates**: Advanced feature for custom string processing

---

## Destructuring

Destructuring allows unpacking values from arrays or properties from objects into distinct variables.

### Array Destructuring

```javascript
let book = ["universe", 55, 69];

// Traditional approach
console.log(book[0]); // universe

// Destructuring
let [title, page, price] = book;
console.log(title); // universe
console.log(page);  // 55
console.log(price); // 69
```

### Object Destructuring

```javascript
let book = {
  name: "Window",
  page: 69,
  price: 599
};

// Destructuring with renaming and default values
let {
  name: title,      // Rename 'name' to 'title'
  page,
  price = 669       // Default value if undefined
} = book;

console.log(title); // Window
console.log(price); // 599
```

### Key Features
- **Renaming**: Use `originalName: newName` syntax
- **Default values**: Provide fallback values with `= defaultValue`
- **Nested destructuring**: Access nested object/array properties

---

## Spread Operator

The spread operator (`...`) expands an iterable (array, string, etc.) into individual elements.

### Syntax

```javascript
let array = [1, 2, 3];
let anotherArray = [5, 4, 6];

// Combine arrays
let spreadArray = [...array, ...anotherArray];
console.log(spreadArray); // [1, 2, 3, 5, 4, 6]

// Copy array
let copyArray = [...array];

// Spread in function calls
console.log(Math.max(...array)); // 3
```

### Use Cases
- Combining arrays
- Copying arrays (shallow copy)
- Converting iterables to arrays
- Spreading elements as function arguments

---

## Rest Parameters

Rest parameters allow functions to accept an indefinite number of arguments as an array.

### Syntax

```javascript
function sum(...args) {
  let result = 0;
  for (let i = 0; i < args.length; i++) {
    result += args[i];
  }
  console.log(result);
}

sum(2, 5, 6, 8); // Output: 21
```

### Key Points
- Must be the last parameter in function definition
- Collects remaining arguments into an array
- Replaces the old `arguments` object with a true array

---

## For...of Loop

The `for...of` loop iterates over iterable objects (arrays, strings, maps, sets, etc.).

### Syntax

```javascript
let scores = [80, 39, 69, 96, 55];

for (const x of scores) {
  console.log(x);
}
// Output: 80, 39, 69, 96, 55
```

### Comparison with For...in
- `for...of`: Iterates over **values**
- `for...in`: Iterates over **keys/indices**

---

## Classes and Objects

ES6 introduced a cleaner syntax for creating objects and implementing inheritance.

### Class Syntax

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayHi() {
    console.log(`Hi ${this.name}`);
  }
}

let person1 = new Person("Spider", 21);
console.log(person1.name); // Spider
person1.sayHi();           // Hi Spider
```

### Static Methods

Static methods belong to the class itself, not instances.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  static hello() {
    console.log("Hey...");
  }
}

Person.hello();  // Works - called on class
// person1.hello(); // Error - not available on instances
```

### Inheritance

Use `extends` to create a subclass and `super` to call parent methods.

```javascript
class Employee {
  constructor(name) {
    this.name = name;
  }

  msg() {
    console.log("Hey it's from Employee...");
  }
}

class Manager extends Employee {
  constructor(name, department) {
    super(name);  // Call parent constructor
    this.department = department;
  }

  msg() {
    console.log("Hey it's from Manager...");
  }

  info() {
    this.msg();       // Calls Manager's msg
    super.msg();      // Calls Employee's msg
    console.log(`${this.name} is manager of department ${this.department}`);
  }
}

let manager1 = new Manager("Spider", "Web");
manager1.info();
```

### Mixins

Mixins allow adding functionality to classes without inheritance.

```javascript
let usefulMethods = {
  sayHi() {
    console.log("Hi...");
  },
  sayBye() {
    console.log("Bye...");
  }
};

class User {
  constructor() {
    this.name = "Uniq";
  }
}

// Add mixin methods to prototype
Object.assign(User.prototype, usefulMethods);

let user1 = new User();
user1.sayHi();  // Hi...
user1.sayBye(); // Bye...
```

---

## Prototypes

Prototypes are the mechanism by which JavaScript objects inherit features from one another.

### Prototype Chain

```javascript
function Creature(lifeSpan) {
  this.lifeSpan = lifeSpan;
}

Creature.prototype.breath = function() {
  console.log('breathing...');
};

function Person(first, last, age) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
}

Person.prototype.fullName = function() {
  console.log(`Hey ${this.firstName} ${this.lastName}`);
};

// Set up inheritance
Person.prototype.__proto__ = Object.create(Creature.prototype);

let person1 = new Person("Uniq", "Boy", 21);
person1.breath();  // breathing... (inherited from Creature)
person1.fullName(); // Hey Uniq Boy
```

### Key Concepts
- Every JavaScript object has a prototype
- Properties/methods are looked up through the prototype chain
- `Object.create()` creates objects with specified prototype
- `Object.assign()` copies properties between objects

---

## Constructors

Constructors are functions used to create and initialize objects.

### Traditional Constructor Function

```javascript
function Person(first, last, age) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;

  this.sayHi = function() {
    console.log(`Hi ${this.firstName} ${this.lastName}!`);
  };

  this.changeAge = function(newAge) {
    this.age = newAge;
  };
}

let person1 = new Person("Spy", "Boy", 21);
person1.changeAge(55);
console.log(person1.age); // 55
person1.sayHi();          // Hi Spy Boy!
```

### Object Literal vs Constructor

```javascript
// Object literal (single object)
let person1 = {
  firstName: "Uniq",
  lastName: "Boy",
  age: 21,
  'id proof': "Pan",

  fullName: function() {
    console.log(`${this.firstName} ${this.lastName}`);
  }
};

// Constructor (reusable template)
function Person(first, last) {
  this.firstName = first;
  this.lastName = last;
}

let person2 = new Person("Lost", "Boy");
```

---

## 🚀 Running the Examples

To run the examples:

```bash
# Run ES6 examples
node es6.js

# Run Modern JS examples
node modern.js
```

---

## 📖 Additional Resources

- [MDN Web Docs - JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [ECMAScript 6 Features](https://es6-features.org/)
- [JavaScript.info](https://javascript.info/)

---

## 📝 License

This project is open source and available for learning purposes.
