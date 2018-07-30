# Javascript
Functions are a plan for how to handle something that will happen at a later date using arguments and parameters as placeholders for information we don't have yet.


## Create a Function
```javascript
function myFunction() {}

// You call a function using its name followed immediately by two parentheses //

function robot() {
console.log('Beep!');
}

var robot2 = function() {
console.log('Beep! Beep!');
}

robot(); // Writes 'Beep!' to the console.
robot2(); // Writes 'Beep! Beep!' to the console.
```

## Parameters
You can create the plan and leave parameters as placeholders

```javascript
function greet(name, age) {
console.log('My name is ' + name + ' and I am ' + age + ' years old.');
}
```

## Arguments
You can now call your function and pass that information in as arguments

```javascript
greet('Helen', 32);
Results in:  'My name is Helen and I am 32 years old.'
```

You can see what arguments a function was called with using the arguments object

```javascript
function greet() {
console.log(arguments);
}

greet('Helen', 32);

Constructor functions
function Dog(name) {
this.name = name;
}

var benji = new Dog('benji');
var spot = new Dog('spot');

console.log(benji); // { name: 'benji' }
console.log(spot); // { name: 'spot' }
```
