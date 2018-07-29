# Javascript
Javascript conditional statements use Boolean tests to choose which code blocks to run.  Here's a starter kit containing if/else statements, ternary operators, switch statements and do/while loops.

There are many different kinds of loops, but they all essentially do the same thing.  There are various situations that are more easily served by one type of loop over the others.  For more, check out the MDM page on how to use loops and iteration or use this starter kit to get going.


## Javascript If/Else Statement
```javascript
if (0 > 1) {
console.log("hi");
} else {
console.log("bye");
}
```

## Ternary Operators - an if-else in one line
```javascript
var age = 12;
//=> undefined

var allowed = (age > 18) ? "yes" : "no";
//=> undefined

allowed
//=> "no"
```

## Switch Statements
```javascript
var food = "apple";

switch(food) {
case 'pear':
console.log("I like pears");
break;
case'apple':
console.log("I like apples");
break;
default:
console.log("No favourite");
}
/* I like apples */
```

## Switch with a case statement
```javascript
var grade = 'C';

switch (grade) {
case'A':
case'B':
case'C':
console.log('You passed!')
break
case'D':
case'F':
console.log('You failed')
break
default:
console.log('Unexpected grade value entered')
}

/* You passed! */
```

## While Loop
Runs while a condition is true.

```javascript
while (i < 10) {
text += "The number is " + i;
i++;
}
```

## Do/while loop
Executes the code block once, before checking if the condition is true, then repeats as long as the condition is true.

```javascript
do {
text += "The number is " + i;
i++;
}
while (i < 10);
```
