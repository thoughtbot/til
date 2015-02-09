#Prototype Your (Character) Class#

Continuing in [using Javascript to build D&D characters](https://github.com/thoughtbot/til/blob/master/javascript/funWithFunctions.md), I decided to use prototypes.

```javascript
function Character (name, hpBonus, profession, hd, castingAbility) {
	this.name = name;
	this.profession = profession;
	this.hd = hd;
	this.hpBonus = hpBonus;
	this.lvl = 1;
	this.profBonus = 2;
	this.castingAbility = castingAbility;
	this.exp = 0;
	this.abilities = new Array(6);
	this.mod = this.abilities.map(function (score){ return Math.floor((score / 2) - 5); } );
	this.ac = 10 + this.mod[1];
	this.hp = this.hd + this.mod[2] + this.dr;
	this.spellSave = 8 + this.profBonus + this.mod[castingAbility];
	this.spellAttack = this.profBonus + this.mod[castingAbility];
}
``` 
	
In using a prototype over an object we gain the ability to efficiently store identical functions common to all characters without bloating objects.

```javascript
Character.prototype = {
	levelUp: function (){ 
		this.lvl++; 
		var conMod = this.mod[2];
		var lvlHP = (this.lvl-1)*(((this.hd/2)+1) + conMod); 
		this.hp = this.hd + conMod + lvlHP + (this.hpBonus * this.lvl); 
		if ((this.lvl - 1) % 4 == 0 ) {
			this.profBonus++;
			this.spellSave = 8 + this.profBonus + this.mod[this.castingAbility];
			this.spellAttack = this.profBonus + this.mod[this.castingAbility];
		}
},
	add: function (paramater, input){
		this.paramater.push(input);
	}
};
```
	
So I've added the main functionality of leveling up our character, as well the ability to add on items to an inventory, weapons list, or character attributes; should the user decide to add those optional values later.

Running a quick check, passing in & leveling up my sorcerer, Mordai:

```javascript
var abilities = [9, 10, 15, 12, 9, 19];
var Mordai = new Character("Mordai", 1, "Sorcerer", 6, 5);
Mordai.levelUp();
console.log(Mordai);
```

I get back the same results as my hand-calculated values for ability bonuses, level, proficiency bonus, and hit points.

![](http://images.thoughtbot.com/TIL/mordaiLayout.jpg)

