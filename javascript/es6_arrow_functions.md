## ECMAScript 6 Arrow Functions

ES6 gives a new flavor of JavaScript. I think one of the coolest part about are the
arrow functions.

### Syntax
Arrow functions provide a cleaner syntax. Here are a few examples:

```javascript
var multiplyBoth = (num1, num2) => num1 * num2;
// equivalent to
var multiplyBoth = function(num1, num2) {
  return num1 * num2;
}

var name = () => "Omar"; // must include () if no arguments
// equivalent to
var name = function() {
  return "Omar";
}
```

###Lexical this Binding

`this` causes a lot of errors in JavaScript because the value of `this` changes
depending on the context of which the function is called. Take this example:

```javascript
var WelcomeUser = {
  name: "Omar",

  init: function() {
    document.ready(function() {
      this.sayHello(); // will cause an error
    });
  },

  sayHello: function() {
    alert("Hello " + this.name + ", it is a pleasure to have you.");
  }
}
```

In this example, the function `this` inside the `init()` function is actually a
reference to `document`. Let's see how the arrow function can change that.

```javascript
var WelcomeUser = {
  name: "Omar",

  init: function() {
    document.ready(() => { // arrow function here
      this.sayHello(); // will trigger the sayHello() function below
    });
  },

  sayHello: function() {
    alert("Hello " + this.name + ", it is a pleasure to have you.");
  }
}
```

Arrow functions implicitly bind `this`. This means that the value of `this`
inside the `document.ready` function call will be the same value of `this` in
which the arrow function was defined. Meaning it will be able to successfully
call the `sayHello()` function.


-----

Functions haven't gone through huge changes, just changes that make them easier
to work with.
