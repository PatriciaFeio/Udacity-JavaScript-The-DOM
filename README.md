# Udacity-JavaScript-The-DOM
Module from the Udacity's Front End Developer Nanodegree Program

# JavaScript Syntax

## Let and Const

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
