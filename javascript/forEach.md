## A Brief explanation of the forEach ##
The 'forEach' is faster than the common 'for', it is functional, it traverses the array and can receive three parameters as the base:

- the item: which refers to the element
- the index: which refers to the position of the element
- the array: which refers to the array itself

The forEach is an Array method and receives a Callback function as a parameter.
A callback function is a function passed as a parameter to another function, to be executed later, when some process ends.

a simple example:

```javascript
  let arr = [1, 2, 3, 4 , 5]; // the array
  
  let result = arr.forEach( (item, index, array) => {
    console.log( `Element: ${item} ` );
    console.log( `Position: ${index}` );
    console.log( `Array itself: ${array}` );
  });
  
  console.log( result );
```
  
Example writing using es6.