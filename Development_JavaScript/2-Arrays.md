# Javascript
Javascript arrays are objects that can hold a series of values and have built-in 'iterator methods'.  Here are the basics with a guide on how to create, add and remove items.


## Create an Array
```javascript
var fruits = ['Apple', 'Banana'];
console.log(fruits.length);
/* 2 */
```

## Access an Array item
```javascript
var first = fruits[0];
/* Apple */
var last = fruits[fruits.length - 1];
/* Banana */
```

## Loop over an Array
```javascript
fruits.forEach(function(item, index, array) {
console.log(item, index);
});
/* Apple 0 */
/* Banana 1 */
```

## Add to the end of an Array
```javascript
var newLength = fruits.push('Orange');
/* ["Apple", "Banana", "Orange"] */
```

## Remove from the end of an Array
```javascript
var last = fruits.pop();
/* ["Apple", "Banana"]; */
```

## Remove from the front of an Array
```javascript
var first = fruits.shift();
/* ["Banana"]; */
```

## Add to the front of an Array
```javascript
var newLength = fruits.unshift('Strawberry') // add to the front
// ["Strawberry", "Banana"];
```

## Find the index of an item in the Array
```javascript
fruits.push('Mango');
/* ["Strawberry", "Banana", "Mango"] */


var pos = fruits.indexOf('Banana');
/* 1 */

```

## Remove an item by index position
```javascript
var removedItem = fruits.splice(pos, 1);
/* ["Strawberry", "Mango"] */
```

## Remove items from an index position
```javascript
var vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
console.log(vegetables);
/* ["Cabbage", "Turnip", "Radish", "Carrot"] */

var pos = 1, n = 2;

var removedItems = vegetables.splice(pos, n);
/* n defines the number of items to be removed, from the position(pos) onward to the end of array.*/

console.log(vegetables);
/* ["Cabbage", "Carrot"] */

console.log(removedItems);
/* ["Turnip", "Radish"] */
```

## Copy an Array
```javascript
var shallowCopy = fruits.slice();
/* ["Strawberry"] */
```
