---
title: "Decoding Functional Currying"
seoTitle: "Understanding Functional Currying"
seoDescription: "Learn how currying simplifies function calls, enhances reusability, and improves readability by transforming functions with multiple arguments"
datePublished: Mon Sep 02 2024 16:22:37 GMT+0000 (Coordinated Universal Time)
cuid: cm0l7lfm2000b09msg1wy79bs
slug: decoding-functional-currying
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1725294057010/ef3c704e-e659-4cc0-8f60-403d552ba414.png
tags: closure, javascript, currying, closures-in-javascript

---

### What is **Currying** ?

* Currying is a programming technique that transforms a function taking multiple arguments (e.g., `func(a, b, c, d)`) into a sequence of functions, each accepting one argument at a time. This allows you to call the function in a chain-like manner (e.g., `func(a)(b)(c)(d)`).
    

```javascript
// Original function taking multiple arguments
function multiply(a, b, c) {
  return a * b * c;
}

// Curried version
function curriedMultiply(a) {
  return function(b) {
    return function(c) {
      return a * b * c;
    };
  };
}

// Using the curried function
const result = curriedMultiply(2)(3)(4); // 2 * 3 * 4 = 24
console.log(result); // Outputs: 24
```

* Currying lets you call a function with one argument at a time. Each call returns a new function that takes the next argument, continuing until all arguments are used.
    

```javascript
// Curried function
function curriedMultiply(a) {
  return function(b) {
    return function(c) {
      return a * b * c;
    };
  };
}

// Call the function with one argument at a time
const step1 = curriedMultiply(2);  // Returns a function that takes `b`
const step2 = step1(3);            // Returns a function that takes `c`
const result = step2(4);           // Computes the result: 2 * 3 * 4

console.log(result); // Outputs: 24
```

### Why Learn Currying ?

1. ***Simplifies Function calls:*** Currying allows you to break down a function into simpler steps, making repeated use easier.
    

```javascript
// Using normal function
function multiply(a, b) {
  return a * b;
}
var result = multiply(2, 3);

// Curried function more simplified
function multiply(a) {
  return function(b) {
    return a * b;
  };
}
var multiplyBy2 = multiply(2);
var result = multiplyBy2(3);
```

2. ***Enhances Reusability:*** By currying, you can create specialized versions of functions for different scenarios without rewriting code.
    

```javascript
// Using normal function
function applyDiscount(discount, price) {
  return price - (price * discount);
}
var discountedPrice100 = applyDiscount(0.10, 100);
var discountedPrice200 = applyDiscount(0.10, 200);

// Curried function for different discounts
function applyDiscount(discount) {
  return function(price) {
    return price - (price * discount);
  };
}
var discount10 = applyDiscount(0.10);

var discountedPrice100 = discount10(100);
var discountedPrice200 = discount10(200);
```

3. ***Improves Readability:*** Currying breaks down complex functions into simpler, more understandable pieces.
    

```javascript
// Function that sets a user's name directly with both arguments provided

// Using normal function
function setUserName(user, name) {
  user.name = name; // Assign the name to the user object
  return user;      // Return the modified user object
}

// Call the function with the user object and name directly
var user = setUserName({}, 'Harry'); 
console.log(user); // Output: { name: 'Harry' }


// Curried function for setting names
function setUserName(name) {
  return function(user) {
    user.name = name; // Assign the name to the user object
    return user;     // Return the modified user object
  };
}

// Create a specific function for setting the name 'Harry'
var setNameForJohn = setUserName('Harry'); // Pre-configure the name 'Harry'

// Use the curried function with the user object
var user = setNameForJohn({}); // Pass an empty object to the pre-configured function
console.log(user); // Output: { name: 'Harry' }
```

### Theme Customization using Currying

Imagine you're building a web application that supports theme customization, allowing users to set different colors for various elements like the background and text. Currying can be used to create functions that customize the theme based on user preferences.

```javascript
// Currying function to customize the theme
function setTheme(backgroundColor) {
  return function(textColor) {
    return function(fontSize) {
      document.body.style.backgroundColor = backgroundColor;
      document.body.style.color = textColor;
      document.body.style.fontSize = fontSize;
    };
  };
}

// Create specialized theme functions
const setLightTheme = setTheme('white')('black'); //white background-black text
const setDarkTheme = setTheme('black')('white'); //black background-white text

// Apply the light theme
setLightTheme('16px'); // Set font size to 16px

// Apply the dark theme
setDarkTheme('18px'); // Set font size to 18px
```

### Conclusion

Currying transforms a function with multiple arguments into a sequence of functions, each taking one argument. It simplifies function calls, enhances reusability, and improves readability by breaking down complex functions into simpler steps.