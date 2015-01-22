## Functional Expressions in D&D ##
I've been having fun with functions while creating a JavaScript version of the 5th edition D&D character sheet.

In recreating the character bonus table I got thru 47 lines of inline conditionals before the formula slapped me in the face:  
![](http://images.thoughtbot.com/TIL/OG_s.jpg)


Even in adding abilities to an array, I was still left with 6 variables and a declared function:

```javascript
var abilities = [9, 10, 15, 12, 9, 19];  //The [str, dex, con, int, wis, chr] of character
function abilityMod(score) { return Math.floor((score / 2) - 5); }  
var strMod = abilityMod(abilities[0]);  
var dexMod = abilityMod(abilities[1]);  
var conMod = abilityMod(abilities[2]);  
var intMod = abilityMod(abilities[3]);  
var wisMod = abilityMod(abilities[4]);  
var chrMod = abilityMod(abilities[5]);
```

Until I used an expression with arrays and `.map`:

```javascript
var abilities = [9, 10, 15, 12, 9, 19];  
var mod = abilities.map(function(score) { return Math.floor((score / 2) - 5); });
```