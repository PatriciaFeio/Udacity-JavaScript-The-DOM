# Udacity: JavaScript & the DOM
Module from the Udacity's Front End Developer Nanodegree Program

[1. JavaScript Syntax](#javaScript-syntax)
  1. [Let and Const](#let-and-const)
2. [The Document Object Model](#the-document-object-model)
3. [Creating Content with JavaScript](#creating-content-with-javaScript)
4. [Working with Browser Events](#working-with-browser-events)
5. [Performance](#performance)

## JavaScript Syntax <a name="javaScript-syntax"></a>

### Let and Const <a name="let-and-const"></a>

**Global scope vs local scope** -> [JavaScript scope](https://www.w3schools.com/js/js_scope.asp)

**Hoisting** -> Variables declared with ```var``` are raised to the top of the function scope -> "hoisted"

**let and const** -> variables declared with ```let``` and ```const``` eliminate the issue of hoiting (they are non-hoisted) -> they´re **scoped to the block** (not to the function)

**Rules for using ```let``` and ```const```** :

* variables declared with ```let``` can be reassigned, but can't be declared in the same scope
* variables declared with ```const``` must be assigned an initial value, but can't be declared in the same scope, nor reassigned

* use ```let``` when we plan to reassign new values to a variable
* use ```const``` when we don't plan on reassigning new values to a variable

* avoid using ```var```

## Template Literals (or template strings in development releases of ES6)

* prior to ES6, strings were concatenated using the string concatenation operator (```+```)
* now we use template literals -> backticks (``` ` ` ```) and placeholders inside represented using ```${expression}```
* template literals preserve newlines as part of the string
* inside embeded expressions we can perform operations, call functions and use loops

## Destructuring (destructuring assignment syntax)

* is a JavaScript expression that makes it possible to unpack values (extract data) from arrays, or properties from objects, into distinct variables
* it allows us to specify the elements we want to extract from the array or object on the left side of an assignment
* for ignoring values, we just leave an empty space between commas:  ```[x, , z] = array;```
* destructuring values from an array: ```const [x, y, z] = array;```
* destructuring values from an object: ```const {variable1, variable2, variable3} = object;```
* if the object has a property with the same name as variable1, we don't need to specify the property from where we want to extract the values, because the value is automatically stored in the variable1 variable

## Object Literal Shorthand

*  new shorthand ways for initializing objects and adding methods to objects:
* if the object properties have the same name as the variables being assigned to them, we can remove the duplicate variable names from objects:

```let type = "quartz";
let color = "rose";
let carat = 21.29;

const gemstone = {type, color, carat};
```

instead of:

```
let type = "quartz";
let color = "rose";
let carat = 21.29;

const gemstone = {
  type: type,
  color: color,
  carat: carat
};
```

* shorthand method names without the function keyword:

```
let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... }
};
```

## Iteration

* process of getting  an item one after the other

### Family of For Loops

1. The for loop

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (let i = 0; i < digits.length; i++) {
  console.log(digits[i]);
}
```
Downside: having to keep track of hthe counter and exit condition

</br> 

2. The for...in loop

* eliminates the counting logic and the exit condition:

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

Downside: still using an index to access the values of the array

forEach loop

```forEach()``` is an array method , so it can only be used exclusively with arrays; there is also no way to stop or break a forEach() loop

</br> 

3. **For...of Loop**

* used to loop over any type of ata that is iterable
* no index used
* the most concised version of all the for loops

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```

* TIP: It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection

* we can stop or break a for...of loop at anytime:

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```

* we can add new properties to objects because the for...of loop will only loop over the values in the object

```
Array.prototype.decimalfy = function() {
  for (i = 0; i < this.length; i++) {
    this[i] = this[i].toFixed(2);
  }
};

const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```

## Spread... Operator (three consecutive dots ```( ... )```)

* allows to expand iterable objects into multiple elements:

```
const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
console.log(...books); 
// Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities
```

* useful for:

1. combining arrays:

```concat()``` method:

```
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];
const produce = fruits.concat(vegetables);
console.log(produce);
// ["apples", "bananas", "pears", "corn", "potatoes", "carrots"]
```

spread operator:

```
const fruits = ["apples", "bananas", "pears"];
const vegetables = ["corn", "potatoes", "carrots"];
const produce = [...fruits, ...vegetables];
console.log(produce);
// [ 'apples', 'bananas', 'pears', 'corn', 'potatoes', 'carrots' ]
```

## ...Rest Parameter (also three consecutive dots ```( ...)```)

* allows us to represent an indefinite number of elements as an array

* useful for:

1. assign the values of an array to variables

```
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
const [total, subtotal, tax, ...items] = order;
console.log(total, subtotal, tax, items);
// 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]
```

</br>

2. when working with variadic functions (functions that take an indefinite number of arguments), like when we have a function called sum() which calculates the sum of an indefinite amount of numbers.

* using the arguments object:  (an array-like object that is avaiable as a local variable inside all function; it contains a value for each argument being passed to the function starting at 0 for the first argument, 1 for the second argument, and so on):

```
function sum() {
  let total = 0;  
  for(const argument of arguments) {
    total += argument;
  }
  return total;
}
```

* using the rest parameter:

```
function sum(...nums) {
  let total = 0;
    for(const num of nums) {
      total += num;
    }
    return total;
}
```
</br>

# The Document Object Model <a name="the-document-object-model"></a>

# Creating Content with JavaScript <a name="creating-content-with-javaScript"></a>

# Working with Browser Events <a name="working-with-browser-events"></a>

# Performance <a name="performance"></a>













