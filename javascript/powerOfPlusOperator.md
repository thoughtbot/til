## Power of the plus operator ##
While playing around in Google Chrome Developer Tools, I had stumbled upon 
the power of the plus operator.

As an example, it is possible to add together an object and array using the '+' operator to return a string object,

```javascript
([] + {}) // returns string "[object Object]"
```

To take this one step further now that we have a string object, we have the ability
of indexing the resultant string to retrieve specific characters by yet using another interesting
syntax of using the '!' operator against types to return their equivalent numeric values,

```javascript
!{} + !{}  // !{} returns false (or numeric value, 0) so !{} + !{} (or, 0 + 0) will result in the value of 0
!!{} + !{} // !!{} evalutes to !false which returns true (ie, 1) so this will result in 1 + 0 or the value of 1
```

This can be used as an obfuscation tactic to generate a string in an unexpected manner,

```javascript
([] + {})     // returns "[object Object]"
  [!![] + !![] + !![] + !![] + !![] + !![] + !![] + !![]]   // evaluates to value '8' so ninth character in string (ie, 'O')
 + ([] + {})  // again another instance of string, "[object Object]"
[!![] + !![] + !![] + !![] + !![]] // evalutes to value '4' so fifth character into string (ie 'c')
 + ([] + {})  // string "[object Object]" again
[!![] + !![] + !![] + !![] + !![] + !![]] // evalutes to value '6' so seventh character (ie, 't')
// the final resultant is a string literal of 'Oct'`