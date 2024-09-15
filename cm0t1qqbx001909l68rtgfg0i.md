---
title: "Understanding JavaScript Classes: Beyond the Basics"
seoTitle: "JavaScript Classes: Advanced Concepts Explained"
seoDescription: "Learn JavaScript classes: syntax, differences from functions, and key features enhancing object-oriented programming in modern JavaScript"
datePublished: Sun Sep 08 2024 04:00:56 GMT+0000 (Coordinated Universal Time)
cuid: cm0t1qqbx001909l68rtgfg0i
slug: understanding-javascript-classes-beyond-the-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726377064292/cc3a1b6a-8a2d-4d05-bd25-f3f93a8d31b1.png
tags: interview, javascript, classes, oops

---

### What are Classes in JavaScript?

* Often, when working on real-world applications, we need to create many objects of the same kind, like users, products, or other entities.
    
* In modern JavaScript (ES6+), we use the `class` construct to create these objects more efficiently, offering features tailored to object-oriented programming (OOP).
    
* **Classes** are essentially special functions that help define blueprints for creating objects.
    
* Just like we can define functions in JavaScript using **function declarations** or **function expressions**, classes can also be defined similarly.
    
* By default, JavaScript **classes** are executed in **strict mode**, which helps catch potential errors and makes the code cleaner and more secure.
    

### JavaScript Class Syntax

* **Classes** can be defined using either a **class declaration** or a **class expression**.
    

#### Class Declaration

* To define a class, we use the `class` keyword followed by the class name.
    
    * According to JavaScript naming conventions, class names should start with an **uppercase letter** (e.g., `User`, `Product`).
        
* Unlike **function declarations**, class declarations are **not hoisted**. This means you must define the class **before using it** in your code.
    
* A class can only be declared **once**. If you try to declare the same class more than once, JavaScript will throw an **error**.
    

Here is the basic **syntax** for a class declaration:

```javascript
class ClassName {
  constructor(parameters) {
    // Initialize object properties
  }

  methodName() {
    // Define methods for class
  }
}
```

#### Class Expression

* Another way to define a class is by using a **class expression**.
    
* Unlike a class declaration, it's **not mandatory** to give a name to the class in a class expression. You can define it as an **anonymous class** or assign it to a variable.
    
* Class expressions allow us to **fetch the class name** from inside the class itself, which is not possible with a class declaration.
    
* **Cannot be re-declared**: Similar to class declarations, you cannot declare a class with the same name more than once within the same scope.
    
* **Can be reassigned**: You can reassign a variable to a new class expression within the same scope. This does not constitute re-declaration but rather a reassignment of the variable to a new class definition.
    

Here’s the **syntax** for a class expression:

```javascript
// Named class expression
let MyClass = class ClassName {
  constructor(parameters) {
    // Initialize object properties
  }

  methodName() {
    // Define methods for the class
  }
};
```

```javascript
// Anonymous class expression
let MyClass = class {
  constructor(parameters) {
    // Initialize object properties
  }

  methodName() {
    // Define methods for the class
  }
};
```

To provide a clearer understanding of the differences between class declarations and class expressions, here is a quick comparison:

| Feature | Class Declaration | Class Expression |
| --- | --- | --- |
| **Syntax** | `class ClassName { ... }` | `let ClassName = class { ... }` |
| **Naming** | Must have a name | Optional name (can be anonymous) |
| **Hoisting** | Not hoisted | Not hoisted |
| **Re-declaration** | Cannot be re-declared | Cannot be re-declared in the same scope, but can be reassigned to a new class expression in the same scope |

### JavaScript Classes: The Function Behind the Syntax

In JavaScript, a class is essentially a special type of function. To illustrate this:

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(this.name);
  }
}

// type of User is a function
console.log(typeof User); // function
```

In this example, `User` is a class, and when we check its type, we see that it's a function. This is because, in JavaScript, **classes are syntactic sugar** over the existing prototype-based inheritance and function constructs.However, there are important differences that distinguish class functions from regular functions. We will explore these differences in the upcoming sections.

#### What the `class` Construct Does ?

When you use the `class User { ... }` construct, the following happens:

1. **Creates a Function**:
    
    * A function named `User` is created. This function represents the class and is the result of the class declaration.
        
    * The function is created from the code inside the `constructor` method (if provided). If no `constructor` method is defined, an empty constructor is used.
        
    
    ```javascript
    // This is a simplified version of what happens
    function User(name) {
      this.name = name;
    }
    ```
    
2. **Stores Methods in** `User.prototype`:
    
    * Methods defined inside the class (like `greet`) are stored on `User.prototype`. This means all instances of `User` will share the same methods through the prototype chain.
        
    
    ```javascript
    User.prototype.greet = function() {
      console.log(this.name);
    };
    ```
    

To confirm these points, consider the following code:

```javascript
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(this.name);
  }
}

// Check if User is a function
console.log(typeof User); // function

// Verify that User is equal to User.prototype.constructor
console.log(User === User.prototype.constructor); // true

// Display the greet method from User.prototype
console.log(User.prototype.greet); // function greet() { ... }

// Show the methods present in User.prototype
console.log(Object.getOwnPropertyNames(User.prototype)); 
// ["constructor", "greet"]
```

So, JavaScript classes are syntactic sugar over functions. Right?  
Wrong!

Often described as syntactic sugar over traditional function and prototype constructs, JavaScript classes offer additional features and distinctions. Let's explore why classes are more than just syntactic sugar.

### Beyond Syntactic Sugar: Key Differences of JavaScript Classes

Let’s explore these key differences one by one.

1. **Internal Properties**
    
    Classes have a special internal property, `[[IsClassConstructor]]: true`, which distinguishes them from regular functions. This property ensures that the function created by the class is recognized as a class constructor by the JavaScript engine.
    
2. **String Representation**
    
    The string representation of a class constructor includes the `class` keyword, making it clear that it was defined using the class syntax. In contrast, a function constructor simply starts with the `function` keyword.
    
    **Class Constructor**:
    
    ```javascript
    class User {}
    console.log(User.toString()); // "class User {}"
    ```
    
    **Regular Function**:
    
    ```javascript
    function User() {}
    console.log(User.toString()); // "function User() {}"
    ```
    
3. **Non-enumerable Methods**
    
    Methods defined within a class are non-enumerable, meaning they don’t appear in `for...in` loops or `Object.keys()`. This helps in hiding internal methods from enumeration, which aligns with typical usage patterns and encapsulation practices.
    
    **Class Methods**:
    
    ```javascript
    class User {
      greet() {}
    }
    console.log(Object.getOwnPropertyNames(User.prototype)); // ["constructor", "greet"]
    ```
    
    **Regular Function Methods**:
    
    ```javascript
    function User() {}
    User.prototype.greet = function() {};
    console.log(Object.getOwnPropertyNames(User.prototype)); // ["constructor", "greet"]
    ```
    
4. **Strict Mode**
    
    All code inside a class is automatically executed in strict mode. This ensures safer coding practices by enforcing stricter parsing and error handling, which is not always the case with functions that are not explicitly marked as strict.
    
    **Inside Class**:
    
    ```javascript
    class User {
      constructor(name) {
        this.name = name;
      }
      greet() {
        // Strict mode is automatically applied here
        console.log(this.name);
      }
    }
    ```
    
    **Regular Function**:
    
    ```javascript
    function User(name) {
      this.name = name;
    }
    User.prototype.greet = function() {
      "use strict";
      console.log(this.name);
    };
    ```
    

These features illustrate that JavaScript classes are more than just a syntactic convenience—they introduce distinct characteristics that enhance their functionality and integration with modern JavaScript practices.

### Summary

JavaScript classes are more than just a syntactic enhancement; they are specialized functions that serve as blueprints for creating objects, embracing object-oriented programming principles. Defined through class declarations or class expressions, these classes are neither hoisted nor re-declarable. Beyond their syntactic benefits, classes introduce unique features such as the `[[IsClassConstructor]]` internal property, non-enumerable methods, and automatic strict mode execution. These characteristics enhance their functionality and align them with modern JavaScript practices, making them a powerful tool in your development toolkit.