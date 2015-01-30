# Property Brace Expansion

Say you want to observe multiple properties on a single object in a computed
property:

```javascript
name: function() {
  return this.get('person.firstName') + ' ' + this.get('person.lastName');
}.property('person.firstName', 'person.lastName')
```

As of Ember 1.4, you can use property brace expansion for an abbreviated syntax:

```javascript
name: function() {
  return this.get('person.firstName') + ' ' + this.get('person.lastName');
}.property('person.{firstName,lastName}')
```
