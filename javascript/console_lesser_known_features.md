# `console` lesser known features.

We've all used the [`console`](https://developer.mozilla.org/en-US/docs/Tools/Web_Console "Console Tool on Firefox") tools
for age (Thank you Firebug) ; but most of use only use the basic features like `console.log()` or `console.error()`.

However, the `console` API is really powerful and offers a lot of very interesting features.

:warning: : Always keep in mind that the `console` API is not standard and is not going to be standardized.
There is absolutely no guarantee that these features will be available and *you should never use `console` on production*.

## String substitutions

`console.log()` and other printing message methods (info, warn and error) supports string substitution (like the C `printf` function).

You can so use :
```javascript
console.log('User %s has %d items', 'John', 5);
```
:arrow_double_down:
```
"User John has 5 items"
```

It's often useful for string concatenation, to avoid the `" + "` agony and prevent the quote/double-quotes errors.

```javascript
var example = " This -> ' and this -> '";
console.log('Here is my string "%s"', example);
```
:arrow_double_down:
```
"Here is my string " This -> ' and this -> '""
```

Currently, here are the supported identifiers :

Identifier  | Description | IE | Chrome | Firefox
:------------- | :------------- | :-------------: | :-------------: | :-------------:
%s | String | :white_check_mark: | :white_check_mark: | :white_check_mark:
%d | Integer | :white_check_mark: | :white_check_mark: | :white_check_mark:
%i | Integer | :white_check_mark: | :white_check_mark: | :white_check_mark:
%f | Floating point value | :white_check_mark: | :white_check_mark: | :white_check_mark:
%o | Javascript object<br>Object will be pretty-printed or a link to the inspector.<br>DOM Object are also handled. | :white_check_mark: | :white_check_mark: | :white_check_mark:
%c | Apply these CSS rules to the following text.<br>Exemple : ```console.log('There are now %c%d%c listeners', 'font-weight: bold;', 2, 'font-weight: normal;')``` =>  There are now **2** listeners  | :x: | :white_check_mark: | :white_check_mark:
%b | Value as binary | :white_check_mark: | :x: | :x:
%x | Value as hexa decimal | :white_check_mark: | :x: | :x:

## Grouping messages

Messages can be grouped with `console.group()` and `console.groupCollapsed()` and `console.groupEnd()`.

```javascript
console.group('First group');
console.log('a'); console.log('b'); console.log('c');
console.groupEnd();
console.group('Second group');
console.log('1'); console.log('2'); console.log('3');
console.group('Embeded subgroup');
console.log('α'); console.log('β'); console.log('γ');
console.groupEnd(); // For the "Embeded subgroup"
console.groupEnd(); // For the "Second group"
```

:arrow_double_down:

![Grouping in Firefox](javascript/console_lesser_known_features/group.png)

```javascript
console.groupCollapsed('Pre-collapsed to save your eyes');
console.log('Never Gonna %s', 'Give You Up');
console.log('Never Gonna %s', 'Get you down !');
console.info('This is a potato');
console.groupEnd();
```

:arrow_double_down:

![Grouping in Chrome](javascript/console_lesser_known_features/collapsed.gif)

## Measuring & profiling

`console.time()` and `console.timeEnd()` allows you to measure the time elapsed between their call.

They both takes a label as argument so you can start simultaneously several timers (docs says up to 10,000) and
know which one you want to stop.

```javascript
var slowInitializer = function() {
  var collection = [];

  for (var i = 20000000; i > 0 ; i--) {
    collection.push(i);
    if (i === 1000) {
      console.time('Last iterations');
    }
  }
  console.timeEnd('Last iterations');
};

console.time('Slow initializer');
slowInitializer();
console.timeEnd('Slow initializer');
```

:arrow_double_down:

```
Last iterations: 0.123ms
Slow initializer: 2778.002ms
```

`console.profile()` and `console.profileEnd()` allows you to profile a part of your code.

`console.profile()` takes a label as argument so you can start simultaneously several timers
(no infos on how many) ; `console.profileEnd()` will end the last started profiler.

The code profiling will be shown in the *profiles* or *profiler* (how any other related name)
on your brower ; with the memory/cpu/calls etc usages.

```javascript
var fibonateIt = function(n) {
  return ((n < 2) ? n : (fibonateIt(n-1) + fibonateIt(n-2)));
};

console.profile('Fibonnaci generation');
fibonateIt(32);
console.profileEnd();
```
:arrow_double_down:

![Fibonacci profiling on IE](javascript/console_lesser_known_features/fibonacci_ie.png)
*On IE*
![Fibonacci profiling on IE](javascript/console_lesser_known_features/fibonacci_chrome.png)
*On Chrome*

You may also use `console.count()` to count the times a label has been executed :


```javascript
$('#image').on('click', function() {
  console.count('Click on my image');
});
```
:arrow_double_down:
```
Click on my image : 1
Click on my image : 2
// [...]
Click on my image : 12
```

:warning: : Don't use `console.count()` on fast and numerous loops (like previous
  previous example on the fibonacci numbers. This will cause your console to print
  a **lot** of information and make your browser slow/unstable/angry.


## Make a conditional logging

`console.assert()` allows you to condition your debug by using a condition as its
first argument.

If your first argument is false (loose comparison aka == and not ===),
it will print out your message (or object), elsewhere it will be ignored.

For example, if you want to log every 100 iteration of a loop :

```javascript
for (var i = 0; i <= 10000; i++) {
  // Do something awesome.
  console.assert(i % 1000, 'Iteration #%d', i);
}
```
:arrow_double_down:
```
"Iteration #0"
"Iteration #1000"
"Iteration #2000"
"Iteration #3000"
"Iteration #4000"
"Iteration #5000"
"Iteration #6000"
"Iteration #7000"
"Iteration #8000"
"Iteration #9000"
"Iteration #10000"
```

**assert** may sound like unit test to you, and of course, you can use it also
to make some kind of unit testing, like :

```javascript
console.assert(
  (fibonateIt(-1) === -1),
  'Fibonacci for -1 should be -1'
);
console.assert(
  (fibonateIt(0) === 0),
  'Fibonacci for 0 should be 0'
);
console.assert(
  (fibonateIt(10) === 55),
  'Fibonacci for 10 should be 55'
);
```

## Pretty-print tabular datas (Arrays, objects, etc.)

`console.table()` allows you to debug some tabular datas in a graphical table
in your console :

```javascript
console.table([['a', 'b', 'c'], ['easy as'], [1,2,3]]);
```

:arrow_double_down:

![Simple table](javascript/console_lesser_known_features/table_simple.png)

:point_right: Some browsers "decides" if whether a table is needed or not to
display your data. For example, ```console.table([1,2,3]);``` will probably not
be displayed in a table.

You can filter out the fields you would like to show :

```javascript
var Crush = function(name, hobby, salary, cute) {
  this.name = name;
  this.hobby = hobby;
  this.salary = salary;
  this.cute = cute;
};

var venal_crushes = [
  new Crush('john', 'animals', '70K', true),
  new Crush('steeve', 'cars', '0K', false),
  new Crush('peter', 'computers', '160K', false),
  new Crush('marcel', 'france', '20K', true)
];

console.table(venal_crushes, ['name', 'salary']);
```

:arrow_double_down:

![Filtered table](javascript/console_lesser_known_features/table_filter.png)

## Log a stack trace

`console.trace()` allows you to show a stack trace to the line where you called
it.

```javascript
var a = function() {
  console.trace('Hello I\'m a stack trace');
};
var b = function() {
  a(5);
};
var c = function() {
  b();
};
var d = function() {
  try {
    throw new Error('Ouch');
  } catch(err) {
    c(err);
  }
};

(function() { d(); })();
```

:arrow_double_down:

![Stack trace](javascript/console_lesser_known_features/stack.png)
