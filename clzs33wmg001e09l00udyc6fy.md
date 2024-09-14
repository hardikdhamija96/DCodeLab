---
title: "DeCoding Closures: Exploring JavaScript with Fun Examples"
seoTitle: "JavaScript Closures Explained with Fun Examples"
seoDescription: "Explore JavaScript closures and lexical scoping with fun, practical examples to understand powerful coding concepts"
datePublished: Sun Sep 01 2024 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clzs33wmg001e09l00udyc6fy
slug: decoding-closures-exploring-javascript-with-fun-examples
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726309557041/f11c62dc-aef2-4e3b-861d-b09b37211afc.png
tags: interview, closure, javascript, web-development, webdev

---

## Introduction

JavaScript is primarily a function-oriented language, offering developers a great deal of flexibility. You can create functions on the fly, pass them as arguments, and even call them from completely different parts of your code. This makes JavaScript highly dynamic and powerful.

One of the unique features that makes JavaScript stand out is **Closures**. Unlike many other languages, JavaScript allows functions to "remember" the variables from their outer scope, even after that scope has finished executing.

**But what do we mean by that?**

To fully understand closures, we need to explore two important concepts: **scope** and **lexical environment**. These lay the foundation for understanding how and why closures work.

In this blog, we’ll break down these basics before diving into the concept of closures itself. Once we’ve covered that, we’ll explore some practical examples to see how closures are used in real-world applications. By the end of this post, you’ll not only understand closures but also feel confident using them in your own projects.

### Understanding Scope in JavaScript

When you declare a variable in JavaScript, such as:

```javascript
let name = "Hardik";
console.log(name); //Output:Hardik 

//name is accessible within this file
```

> * you can use this variable throughout the file where it’s declared.
>     
> * This is because of its **scope**.
>     
> * **Scope:** determines where a variable can be accessed in your code.
>     

In this case, `name` has **global scope** within the file, meaning it is accessible from anywhere in that file.

What if we write same code in same file, with in curly braces ?

```javascript
{
  let name = "Hardik";
  console.log(name); // Output: Hardik
}

console.log(name); // Error! name is not defined
```

But Why ?

> * Here, the variable `name` is declared inside a code block `{...}`.
>     
> * **Code blocks** are sections of code enclosed in curly braces `{...}`.
>     
> * In this example, `name` is only accessible within that block.
>     
> * Trying to access `name` outside the block results in an error.
>     
> * This is because of **block scope**.
>     
> 
> **Block scope** means that variables declared inside a code block are confined to that block and cannot be accessed outside of it, even if it’s within the same file.

A similar behavior can be seen with functions as well.

```javascript
function nameScope() {
  let name = "Hardik";
  console.log(name); // Output: Hardik
}

nameScope();

console.log(name); // Error! name is not defined
```

> * `name` is declared inside the function `nameScope`.
>     
> * This is an example of **local scope**.
>     
> * Variables declared within a function are only accessible within that function.
>     

Scope Summary:

| Scope Type | Accessibility |
| --- | --- |
| Global Scope | Accessible from any part of the file. |
| Block Scope | Accessible only within the code block `{...}`. |
| Local Scope | Accessible only inside the function. |

### What is Lexical Scoping ?

* Lexical scope means that the scope of a variable is based on where it is defined in the code.
    
* It remains accessible only within that block of code.
    

```javascript
function outerFunction() {
  let outerVariable = 'I am outside!';
  
  function innerFunction() {
    let innerVariable = 'I am inside!';
    console.log(outerVariable); // Can access outerVariable
    console.log(innerVariable); // Can access innerVariable
  }
  
  innerFunction();
  console.log(outerVariable); // Can access outerVariable
  console.log(innerVariable); // Cannot access innerVariable (causes an error)
}

outerFunction();
```

* **Lexical Scope** refers to the way the scope of a variable is determined by its location in the code. In above example:
    
* `outerVariable` is declared within `outerFunction`, so it is accessible within `outerFunction` and any functions nested inside it (like `innerFunction`).
    
* `innerVariable` is declared within `innerFunction`, so it is accessible only within `innerFunction`.
    

### What is Closure ?

* **Closure** is a concept where a function retains access to variables from its outer (enclosing) scope even after that function has finished executing. In your code:
    
* `innerFunction` is a closure because it has access to `outerVariable` even though `outerVariable` is defined in the outer function (`outerFunction`).
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725278285707/57bd1d26-4099-4a75-a00d-529bcf2b26e6.png align="right")

### Definition

A closure is a function that retains access to variables from its outer (enclosing) function even after the outer function has finished executing. Closures are a result of lexical scoping and allow functions to maintain a reference to their environment.

```javascript
function createCounter() {
  var count = 0;

  function incrementCounter() {
    count += 1;
    console.log(count);
  }

  return incrementCounter;
}

var counter = createCounter();
counter(); // Output: 1
counter(); // Output: 2
```

**Explanation:**

* `createCounter` defines a local variable `count` and an inner function `incrementCounter`.
    
* `incrementCounter` forms a closure over `count`, meaning it retains access to `count` even after `createCounter` has finished executing.
    
* Each time `counter()` is called, it updates and logs the value of `count` because the closure maintains a reference to the original `count` variable.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1725279813047/af74eb5a-f3d6-4fa9-9bff-5777048699f8.png align="center")

### Updating Outer Scope Variables

* **Retains Reference:** Closures retain a reference to the outer variables, not just a copy of their values.
    
* **Dynamic Updates:** If an outer variable is updated after the closure is created, the closure reflects these updates because it maintains a reference to the variable.
    

```javascript
function createCounter(initialValue) {
  var count = initialValue;

  function getCount() {
    console.log(count);
  }

  count = 100; // Modifying outer variable
  return getCount;
}

var counter = createCounter(10);
counter(); // Output: 100
```

**Explanation:**

* `createCounter` initializes `count` with `initialValue` and defines the `getCount` function.
    
* After defining `getCount`, the outer variable `count` is updated to **100**.
    
* The closure formed by `getCount` retains access to the updated value of `count`. As a result, when `counter()` is called, it reflects the modified value of `count`.
    

### Shadowing with Closures

* **Variable shadowing** happens when a nested function defines a variable with the same name as a variable in an outer scope.
    
* The inner variable shadows the outer one within its scope.
    

```javascript
function createCounter() {
  var count = 0;

  function increment() {
    var count = 10; // Shadowing outer `count`
    console.log(count); // Output: 10
  }

  increment();
  console.log(count); // Output: 0
}

createCounter();
```

Explanation:

* `createCounter` defines a variable `count` and an inner function `increment`.
    
* `increment` defines its own `count` which shadows the outer `count`.
    
* Within `increment`, the inner `count` is accessed, while outside it, the outer `count` is accessed.
    

## Practical Frontend Techniques

### [**Currying**](https://hardikdhamija.hashnode.dev/decoding-functional-currying)

* Currying is a functional programming technique where a function that takes multiple arguments is transformed into a series of functions that each take a single argument.
    
* Currying utilizes closures to retain the state of partially applied arguments. Each curried function call returns a new function that maintains access to the previously provided arguments, allowing for incremental function application.
    

Read more: [here](https://hardikdhamija.hashnode.dev/decoding-functional-currying)

```javascript
// Curried function to create a greeting message
function greet(formality) {
  return function(timeOfDay) {
    return function(name) {
      return `${formality} ${name}, good ${timeOfDay}!`;
    };
  };
}

// Usage
const formalGreeting = greet('Good evening'); // Curried function with formality
const eveningGreeting = formalGreeting('evening'); // Curried function with time of day
const message = eveningGreeting('Alice'); // Complete the greeting with the name
console.log(message); // Output: Good evening Alice, good evening!
```

### Debouncing

* Debouncing is a technique used to ensure that a function is only executed after a certain period of inactivity or delay. This is particularly useful for handling events that fire frequently, such as keystrokes or window resizing, to prevent excessive function calls and improve performance.
    
* Under the hood, debouncing often uses closures to maintain the state of the timer. The closure keeps a reference to the timeout function and manages its execution, ensuring that the function is called only after the specified delay has passed since the last event.
    

```javascript
function debounce(func, delay) {
  let timer; // Closure variable to keep track of the timer
  
  return function(...args) {
    clearTimeout(timer); // Clear previous timer
    timer = setTimeout(() => func(...args), delay); // Set a new timer
  };
}

// Usage
const debouncedFunction = debounce(() => console.log('Debounced!'), 300);
window.addEventListener('resize', debouncedFunction);
```

## Conclusion

Closures and lexical scoping in JavaScript are essential concepts that enhance coding flexibility and power. Lexical scoping determines a variable's scope based on its location in the code. Closures allow a function to retain access to variables from its outer scope even after the outer function has finished executing. Practical applications include currying and debouncing, which utilize closures to manage state and improve performance.