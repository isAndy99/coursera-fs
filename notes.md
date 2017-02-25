# Introduction to HTML5

## Lecture 5: HTML Content models

> **Block-Level elements:** (Roughly Flow Content)
> - render to begin on a new line
> - may contain inline or other block-level elements
> 
> **Inline elements:** (Roughly Phrase Content)
> - rendered on the same line (by default)
> - may only contain other inline elements

# Introduction to CSS3
## Lecture 14: Combining Selectors

Selector type | Syntax
---------|----------
 class selector | selector.class
 child (direct) selector | selector > selector
 descendent selector | selector selector
  | 
  adjacent selector | selector + selector
  general sibling selector | selector - selector


# Introduction to JavaScript

## Lecture 41, Part 1: Defining Variables, Function, and Scope
### Variables
- JS figures the type of the variable at runtime (dynamically typed)
- same variable cand hold different types during the life of the execution

### Functions

>```javascript
>function a () {...}
>```
>or
>```javascript
>var a = function () {...}
>```
> - no name defined
> - value of function assigned, **NOT the returned result**

### Scope
- Global
- Function (aka lexical)

### Scope chain
- Everything is executed in an *Execution Context*
- Function invocation creates a new *Execution Context*
- Each *Execution Context* has:
  * Its own *Variable Environment*
  * Special *'this'* object
  * Reference to its *Outer Environment*
- Global scope does not have an *Outer Environment* as it's the most outer there is

>Referenced (not defined) variable will be searched for in its current scope first. If not found, the *Outer Reference* will be searched. If not found, the *Outer Reference*'s *Outer Reference* will be searched, etc. This will keep going until the Global scope. If not found in Global scope, the variable is undefined.

- It does not matter where a particular function is executed **(resolving scope over variables)** ; what matters is **where the function is physically defined** 


## Lecture 42, Part 1: Javascript Types
### Object type
- **Object** is a collection of name/value pairs
- **Primitive type** represents a single, immutable value
  - **Boolean**
  - **Undefined** - no values have ever been set (lack of definition) - `undefined`
  - **Null** - lack of value - `null`
  - **Number** - double-precision 64-bit floating point (only numeric type in JS)
    * Integers are a subset of doubles, instead of a separate data type
  - **String** - sequence of characters used to represent Context
    * single or double quotes

  - Symbol - new to ES6


## Lecture 42, Part 2: Javascript Types

> **undefined** != **not defined**  
> **undefined** - has been declared, but it has not been set a value


## Lecture 43, Part 2: Common Language Constructs

### False
``` javascript
if (false || null || undefined || "" || 0 || NaN) {
  console.log("This line won't ever execute");
}
else {
  console.log("All false");
}
```

### True
``` javascript
if (true && "hello" && 1 && -1 && "false") {
  console.log("All true");
}
```

## Lecture 44: Handling Default Values

``` javascript
function orderChickenWith(sideDish) {
  sideDish = sideDish || "whatever!";
  console.log("Chicken with " + sideDish);
}

orderChickenWith("noodles");
orderChickenWith();
```
Result:  
`Chicken with noodles`  
`Chicken with whatever!`

## Lecture 46: Functions Explained
``` javascript
// Functions are First-Class Data Types
// Functions ARE objects
function multiply(x, y) {
  return x * y;
}
multiply.version = "v.1.0.0";
console.log(multiply.version);


// Function factory
function makeMultiplier(multiplier) {
  var myFunc = function (x) {
    return multiplier * x;
  };

  return myFunc;
}

var multiplyBy3 = makeMultiplier(3);
console.log(multiplyBy3(10));
var doubleAll = makeMultiplier(2);
console.log(doubleAll(100));



// Passing functions as arguments
function doOperationOn(x, operation) {
  return operation(x);
}

var result = doOperationOn(5, multiplyBy3);
console.log(result);
result = doOperationOn(100, doubleAll);
console.log(result);
```

## Lecture 47, Part 1: Passing Variables by Value vs. by Reference

> In JavaScript, **primitives** are passed by _value_, **objects** are passed by _reference_.
- "Under the hood", everything is actually passed by value


## Lecture 48: Function Constructors, prototype, and the 'this' Keyword

``` javascript
// Function constructors
function Circle (radius) {
  this.radius = radius;
}

Circle.prototype.getArea = // prototype, so it does not create a getArea method for each instance of Circle; only once
  function () {
    return Math.PI * Math.pow(this.radius, 2);
  };


var myCircle = new Circle(10);
console.log(myCircle.getArea());

var myOtherCircle = new Circle(20);
console.log(myOtherCircle);
```


## Lecture 49: Object Literals and the 'this' Keyword

``` javascript
// Object literals and "this"
var literalCircle = { // new Object() implied
  radius: 10,

  getArea: function () {
    var self = this;
    console.log(this);

    var increaseRadius = function () {
      self.radius = 20; //if 'this' is used here (function within a function), it will refer to Window (global scope)
    };
    increaseRadius();
    console.log(this.radius);

    return Math.PI * Math.pow(this.radius, 2);
  }
};

console.log(literalCircle.getArea());
```


## Lecture 50: Arrays
``` javascript
// Arrays
var array = new Array();
array[0] = "Yaakov";
array[1] = 2;
array[2] = function (name) {
  console.log("Hello " + name);
};
array[3] = {course: " HTML, CSS & JS"};

console.log(array);
array[2](array[0]);
console.log(array[3].course);


// Short hand array creation
var names = ["Yaakov", "John", "Joe"];
console.log(names);

for (var i = 0; i < names.length; i++) {
  console.log("Hello " + names[i]);
}

names[100] = "Jim";
for (var i = 0; i < names.length; i++) {
  console.log("Hello " + names[i]);
}

var names2 = ["Yaakov", "John", "Joe"];

var myObj = {
  name: "Yaakov",
  course: "HTML/CSS/JS",
  platform: "Courera"
};
for (var prop in myObj) {
  console.log(prop + ": " + myObj[prop]);
}

for (var name in names2) {
  console.log("Hello " + names2[name]);
}

names2.greeting = "Hi!";

for (var name in names2) {
  console.log("Hello " + names2[name]);
}
```


## Lecture 51: Closures
```javascript
// Closures
function makeMultiplier (multiplier) {
  // var multiplier = 2;
  function b() {
    console.log("Multiplier is: " + multiplier);
  }
  b();


  return (
      function (x) {
        return multiplier * x;
      }

    );
}

var doubleAll = makeMultiplier(2);
console.log(doubleAll(10)); // its own exec env
```

## Lecture 52: Fake Namespaces; Immediately Invoked Function Expressions (IIFEs)
_script1.js_
``` javascript
(function (window) {
  var yaakovGreeter = {};
  yaakovGreeter.name = "Yaakov";
  var greeting = "Hello ";
  yaakovGreeter.sayHello = function () {
    console.log(greeting + yaakovGreeter.name);
  }

  window.yaakovGreeter = yaakovGreeter;

})(window);
```
_script2.js_
``` javascript
(function (window) {
  var johnGreeter = {};
  johnGreeter.name = "John";
  var greeting = "Hi ";
  johnGreeter.sayHi = function () {
    console.log(greeting + johnGreeter.name);
  }

  window.johnGreeter = johnGreeter;

})(window);
```
_app.js_
``` javascript
yaakovGreeter.sayHello();
johnGreeter.sayHi();

// Immediately Invoked Function Expression
// IIFE
(function (name) {
  console.log("Hello " + name);
})("Coursera!");
```
_index.html_
``` html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <script src="js/script1.js"></script>
    <script src="js/script2.js"></script>
    <script src="js/app.js"></script>
  </head>
<body>
  <h1>Lecture 52</h1>
</body>
</html>
```

## Lecture 53: DOM Manipulation
``` javascript
// DOM manipulation
// console.log(document.getElementById("title"));
// console.log(document instanceof HTMLDocument);

function sayHello () {
  var name =
   document.getElementById("name").value;
   var message = "<h2>Hello " + name + "!</h2>";

  // document
  //   .getElementById("content")
  //   .textContent = message;

  document
    .getElementById("content")
    .innerHTML = message;

  if (name === "student") {
    var title = 
      document
        .querySelector("#title")
        .textContent;
    title += " & Lovin' it!";
    document
        .querySelector("h1") // returns the first found element; queryAllSelector for all
        .textContent = title;
  }
}
```

## Lecture 54: Handling Events & Lecture 55: The 'event' Argument

``` javascript
// Event handling
document.addEventListener("DOMContentLoaded",
  function (event) {
    
    function sayHello (event) {
      console.log(event);

      this.textContent = "Said it!";
      var name =
       document.getElementById("name").value;
       var message = "<h2>Hello " + name + "!</h2>";

      document
        .getElementById("content")
        .innerHTML = message;

      if (name === "student") {
        var title = 
          document
            .querySelector("#title")
            .textContent;
        title += " & Lovin' it!";
        document
            .querySelector("h1")
            .textContent = title;
      }
    }

    // Unobtrusive event binding
    document.querySelector("button")
      .addEventListener("click", sayHello);

    document.querySelector("body")
      .addEventListener("mousemove",
        function (event) {
          if (event.shiftKey === true) {
            console.log("x: " + event.clientX);
            console.log("y: " + event.clientY);
          }
        }
      );

  }
);

// document.querySelector("button")
//   .onclick = sayHello;
```



# Other
> ### BrowserSync
> ``` browser-sync start --server --directory --files "**/*" ```