Javascript arrays are objects that can hold a series of values and have built-in 'iterator methods'.  Here are the basics with a guide on how to create, add and remove items.



Create an Array
var fruits = ['Apple', 'Banana'];
console.log(fruits.length);
/* 2 */

Access an Array item
var first = fruits[0];
/* Apple */
var last = fruits[fruits.length - 1];
/* Banana */

Loop over an Array
fruits.forEach(function(item, index, array) {
console.log(item, index);
});
/* Apple 0 */
/* Banana 1 */

Add to the end of an Array
var newLength = fruits.push('Orange');
/* ["Apple", "Banana", "Orange"] */

Remove from the end of an Array
var last = fruits.pop();
/* ["Apple", "Banana"]; */

Remove from the front of an Array
var first = fruits.shift();
/* ["Banana"]; */

Add to the front of an Array
var newLength = fruits.unshift('Strawberry') // add to the front
// ["Strawberry", "Banana"];

Find the index of an item in the Array
fruits.push('Mango');
/* ["Strawberry", "Banana", "Mango"] */

var pos = fruits.indexOf('Banana');
/* 1 */

Remove an item by index position
var removedItem = fruits.splice(pos, 1);
/* ["Strawberry", "Mango"] */

Remove items from an index position
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

Copy an Array
var shallowCopy = fruits.slice();
/* ["Strawberry"] */
