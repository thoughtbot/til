## Strings and Regular Expressions in JS ##
I've been using RE in JS for a while now, but today I learned something I just had to share, and thought this might be the place to do it.

### Find & Replace ###
It's common knowledge that one can find a substring with `indexOf`:

```javascript
var text = 'This is a string';
console.log(text.indexOf('str')); // 10
```

Or replace using strings:

```javascript
var text = 'This is a string';
console.log(text.replace('str', 'fl')); //'This is a fling'
```

However, you only replace the first occurrence thusly.

### Enter RegEx ###

I'm going to assume you're familiar with [creating RE in JS](https://developer.mozilla.org/en/docs/Web/JavaScript/Guide/Regular_Expressions).

These are some nifty things you can do with them that work better than the former methods:

```javascript
var text = 'A string is a string is a string';
var exp = /a (string)/ig;

// Replace .indexOf clumsy -1 as false
exp.test(text); // is there at least a single match for exp in text? (true)

// Better replace
text.replace(exp, 'A meow'); // 'A meow is A meow is A meow is'
text.replace(exp, 'a long $1'); // 'a long string is a long string is a long string'

// But this is what I came here to tell you!
text.replace(exp, function (completeMatch, ...groups, matchStartIndex, completeText) {
  // This will be called for every match found!
  return (matchStartIndex ? 'a' : 'A') + ' ' + groups[0].replace('i', 'o');
}); // 'A strong is a strong is a strong'
```
