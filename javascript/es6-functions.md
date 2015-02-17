## ECMAScript 6 Functions

In this TIL, we will look at three features in ES6 regarding functions:
* Default Values
* Block level functions
* Arrow functions

#### Default Values

JavaScript functions allow any number of parameters to be passed regardless of
the number of declared parameters. To have certain values in the parameters
represent defaults, you would need to do this:

```javascript
function doRequest(url, timeout, callback) {
  var timeout = timeout || 2000;
  var callback = callback || function() {
    // callback code
  };

  // rest of code
}
```
If `timeout` is not passed as an argument, then it would be set to 2000. Likewise
for `callback`. With ES6, we can now set default arguments.

```javascript
function doRequest(url, timeout = 2000, callback) {
  // rest of code
}
```

The default value for timeout will only be used when there is no second argument
present. For the last argument, we can also define a default function for it.

```javascript
function someCallback() {
  return function() {
    // some code
  }
}

function doRequest(url, timeout = 2000, callback = someCallback()) {
  // rest of code
}
```


#### Block Level Functions


In ES5 strict mode, a function declaration made within a block would throw an
error:

```javascript
"use strict";

if (true) {
  // throws a syntax error
  function someThing() {
    // some code
  }
}
```

In ES6, you can declare a function within a block and it will only be accessible
within that block:

```javascript
"use strict";

if (true) {
  console.log(typeof someThing()); // "function"

  function someThing() {
    // some code
  }

  someThing();
}

console.log(typeof someThing()); // "undefined"
```

Once the `if` block is finished executing, `someThing()` no longer exists. This
works in "use strict" mode, and if you were to not do "use strict", then
`someThing()` would be available outside the `if` block:

```javascript
if (true) {
  console.log(typeof someThing()); // "function"

  function someThing() {
    // some code
  }

  someThing();
}

console.log(typeof someThing()); // "function"
```

`someThing()` is hoisted in outside the `if` block.

#### Arrow Functions

This is one of the coolest parts of ES6 and probably will be most used. The
defining feature of arrow functions is the lexical binding of `this`. The value
of `this` is defined by where the arrow function is defined, not where it is
used. Essentially, `this` does not change.

###### Syntax
Arrow functions also provide a cleaner syntax. Here are a few examples:

```javascript
var double = num => num * 2;

//equivalent to

var double = function(num) {
  return num * 2;
}
```

You will notice the `double()` function did not have parenthesis around `num`.
You do not need to include parenthesis around a single parameter. 

If you want a function to have multiple parameters, you put them in parenthesis
before the arrow:

```javascript
var multiplyBoth = (num1, num2) => num1 * num2;

//equivalent to

var multiplyBoth = function(num1, num2) {
  return num1 * num2;
}
```

If there are no arguments, then you **must** include an empty parenthesis:

```javascript
var name = () => "Omar";

// equivalent to

var name = function() {
  return "Omar";
}
```

######Lexical this Binding

`this` causes a lot of errors in JavaScript because the value of `this` changes
depending on the context of which the function is called. Take this example:

```javascript
var WelcomeUser = {
  name: "Omar",

  init: function() {
    document.ready(function() {
      this.sayHello(); // this will error
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
      this.sayHello();
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
