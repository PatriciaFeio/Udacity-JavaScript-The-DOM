# Udacity: JavaScript & the DOM
Module from Udacity's Front End Developer Nanodegree Program.

<br>

## Table of contents
<a name="top"></a>

<details>
  
[1. JavaScript Syntax](#javaScript-syntax)
  * [Let and Const](#let-and-const)
  * [Template Literals](#template-literals)
  * [Destructuring](#destructuring)
  * [Object Literal Shorthand](#object-literal-shorthand)
  * [Iteration](#iteration)
  * [Family of For Loops](#family-of-for-loops)
  * [For...of Loop](#for-of-loop)
  * [Spread... Operator](#spread-operator)
  * [...Rest Parameter](#rest-parameter)
  
[2. The Document Object Model](#the-document-object-model)
  * [The DOM](#the-dom)
  * [Select Page Element By ID](#select-page-element-by-id)
  * [Select Page Elements By Class or Tag](#select-page-elements-by-class-or-tag)
  * [Nodes, Elements, and Interfaces](#nodes-elements-interfaces)
  * [More Ways To Access Elements](#more-ways-to-access-elements)

[3. Creating Content with JavaScript](#creating-content-with-javaScript)
  * [Update Existing Page Content](#update-existing-page-content)
  * [Add New Page Content](#add-new-page-content)
  * [Remove Page Content](#remove-page-content)
  * [Style Page Content](#style-page-content)

[4. Working with Browser Events](#working-with-browser-events)
  * [Events - what they are](#events-what-they-are)
  * [Responding to Events](#responding-to-events)
  * [Removing an Event Listener](#removing-an-event-listener)
  * [Phases of an Event](#phases-of-an-event)
  * [Avoid Too Many Events](#avoid-too-many-events)
  * [Know When the DOM Is Ready](#know-when-the-dom-is-ready)

[5. Performance](#performance)
  </details>


## JavaScript Syntax <a name="javaScript-syntax"></a>


### *Let and Const* <a name="let-and-const"></a>

* **Global scope vs local scope** -> [JavaScript scope](https://www.w3schools.com/js/js_scope.asp).

* **Hoisting** -> Variables declared with ```var``` are raised to the top of the function scope -> "hoisted".

* **Let and const** -> variables declared with ```let``` and ```const``` eliminate the issue of hoiting (they are non-hoisted) -> they´re **scoped to the block** (not to the function).

**Rules for using ```let``` and ```const```** :

* variables declared with ```let``` can be reassigned, but can't be declared in the same scope;
* variables declared with ```const``` must be assigned an initial value, but can't be declared in the same scope, nor reassigned;
* use ```let``` when we plan to reassign new values to a variable;
* use ```const``` when we don't plan on reassigning new values to a variable;
* avoid using ```var```.

<br>

### *Template Literals* (or template strings in development releases of ES6) <a name="template-literals"></a>

* Prior to ES6, strings were concatenated using the string concatenation operator (```+```).
* Now we use template literals -> backticks (``` ` ` ```) and placeholders inside represented using ```${expression}```.
* Template literals preserve newlines as part of the string.
* Inside embeded expressions we can perform operations, call functions and use loops.

<br>

### *Destructuring* (destructuring assignment syntax) <a name="destructuring"></a>

* Is a JavaScript expression that makes it possible to unpack values (extract data) from arrays, or properties from objects, into distinct variables.
* It allows us to specify the elements we want to extract from the array or object on the left side of an assignment.
* For ignoring values, we just leave an empty space between commas:  ```[x, , z] = array;```.
* Destructuring values from an array: ```const [x, y, z] = array;```.
* Destructuring values from an object: ```const {variable1, variable2, variable3} = object;```.
* If the object has a property with the same name as variable1, we don't need to specify the property from where we want to extract the values, because the value is automatically stored in the variable1 variable.

<br>

### *Object Literal Shorthand* <a name="object-literal-shorthand"></a>

* New shorthand ways for initializing objects and adding methods to objects.
* If the object properties have the same name as the variables being assigned to them, we can remove the duplicate variable names from objects:

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

* Shorthand method names without the function keyword:

```
let gemstone = {
  type,
  color,
  carat,
  calculateWorth() { ... }
};
```
<br>

### *Iteration* <a name="iteration"></a>

* Process of getting  an item one after the other.

<br>

### *Family of For Loops* <a name="family-of-for-loops"></a>

1. The for loop:

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (let i = 0; i < digits.length; i++) {
  console.log(digits[i]);
}
```
* Downside: having to keep track of hthe counter and exit condition.

</br> 

2. The for...in loop:

* Eliminates the counting logic and the exit condition:

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const index in digits) {
  console.log(digits[index]);
}
```

* Downside: still using an index to access the values of the array.

forEach loop

```forEach()``` is an array method , so it can only be used exclusively with arrays; there is also no way to stop or break a forEach() loop.

</br> 

### *For...of Loop* <a name="for-of-loop"></a>

* Used to loop over any type of data that is iterable.
* No index used.
* The most concised version of all the for loops.

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  console.log(digit);
}
```

* TIP: It’s good practice to use plural names for objects that are collections of values. That way, when you loop over the collection, you can use the singular version of the name when referencing individual values in the collection.

* We can stop or break a for...of loop at anytime:

```
const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];

for (const digit of digits) {
  if (digit % 2 === 0) {
    continue;
  }
  console.log(digit);
}
```

* We can add new properties to objects because the for...of loop will only loop over the values in the object:

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
<br>

### *Spread... Operator* (three consecutive dots ```( ... )```) <a name="spread-operator"></a>

* Allows to expand iterable objects into multiple elements:

```
const books = ["Don Quixote", "The Hobbit", "Alice in Wonderland", "Tale of Two Cities"];
console.log(...books); 
// Don Quixote The Hobbit Alice in Wonderland Tale of Two Cities
```

* Useful for:

1. Combining arrays:

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
<br>

### *...Rest Parameter* (also three consecutive dots (```...```)) <a name="rest-parameter"></a>

* Allows us to represent an indefinite number of elements as an array.

* Useful for:

1. Assign the values of an array to variables:

```
const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
const [total, subtotal, tax, ...items] = order;
console.log(total, subtotal, tax, items);
// 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]
```

</br>

2. When working with variadic functions (functions that take an indefinite number of arguments), like when we have a function called sum() which calculates the sum of an indefinite amount of numbers.

* Using the arguments object:  (an array-like object that is avaiable as a local variable inside all function; it contains a value for each argument being passed to the function starting at 0 for the first argument, 1 for the second argument, and so on):

```
function sum() {
  let total = 0;  
  for(const argument of arguments) {
    total += argument;
  }
  return total;
}
```

* Using the rest parameter:

```
function sum(...nums) {
  let total = 0;
    for(const num of nums) {
      total += num;
    }
    return total;
}
```
<br>

[Back to top](#top)


## The Document Object Model <a name="the-document-object-model"></a>

### *The DOM* <a name="the-dom"></a>

* DOM: document object model, the full, parsed representation of the HTML; a tree-like structure that is a representation of the HTML document, the relationship between elements, and contains the content properties of the elements.

- HTML received - HTML tags are converted to tokens - tokens are converted to Nodes - Nodes are converted to the DOM.

* The DOM is:

- constructed from the browser;

- globally accessible by JavaScript code using the ```document``` object.

Resources: [Intro to the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction).

<br>

### *Select Page Element By ID* <a name="select-page-element-by-id"></a>

* ```document.getElementById()```.
* It is called on the ```document``` object.
* It returns a single item.
* If there is no element with the given ```id```, it returns ```null```.
* The ```id``` parameter is case-sensitive.

Resources: [Document: getElementById() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById).

<br>

### *Select Page Elements By Class or Tag* <a name="select-page-elements-by-class-or-tag"></a>

1. Selecting Multiple Elements At Once

* Accessing Elements By Their Class: ```document.getElementsByClassName()```.
* Accessing Elements By Their Tag: ```document.getElementsByTagName()```.
* The return value of both methods is a live ```HTMLCollection``` of found elements.

Resources: 
* [Document: getElementsByClassName() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName)
* [Element: getElementsByTagName() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName)
* [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)

<br>

### *Nodes, Elements, and Interfaces* <a name="nodes-elements-interfaces"></a>

1. How the DOM is constructed:
* characters
* tags
* tokens
* nodes
* DOM

2. The ```node``` Interface:
* Node (capital "N") is a blueprint (interface) that contains information about all of the properties (data) and methods (functionality) that every real node (lowercase "n") has after been created.

3. Element Interface:
* Is a blueprint for creating elements.
* It is a descendent of the Node interface (= parent of Element) - EventTarget <- Node <- Element - so it inherits all of the Node Interface's properties and methods. It means that any element that was created from the Element Interface is also a descendent from the Node Interface, so the element is also a node.

Resources:
* [Node](https://developer.mozilla.org/en-US/docs/Web/API/Node)
* [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)
* [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API)

<br>

### *More Ways To Access Elements* <a name="more-ways-to-access-elements"></a>

1. The querySelector Method:
* With ```.querySelector()``` method we can select an element by its id, class or tag name.
* It returns a single element (if we are searching an element by class or tag name, this method will only return the first item it finds).

2. The querySelectorAll Method:
* ```querySelectorAll()``` method.
* It returns a non-live ```NodeList``` containing one ```Element``` object for each element that matches at least one of the specified selectors or an empty ```NodeList```in case of no matches. We can access the contents of the list using any standard array notation or a looping statement like a ```for``` loop, a ```for...of``` loop, the ```forEach()``` method.

Resources:
* [Document: querySelector() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
* [Document: querySelectorAll() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)
* [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

<br>

[Back to top](#top)

## Creating Content with JavaScript <a name="creating-content-with-javaScript"></a>

### *Update Existing Page Content* <a name="update-existing-page-content"></a>

With the element's property ```.innerHTML``` we can:
* get/set an element's (and all of its descendents) HTML content (inside the selected element);
* it returns a ```DOMString```.

 The ```.outerHTML ```:
* represents the HTML element itself, as well as its children.

 The ```.textContent``` property will:
* set/get the text content of an element and all its descencents;
* returns all text content, regardless of CSS.

* To update an element, including its HTML, we need to use the ```.innerHTML``` property (```.innerHTML``` will render any HTML on the string).

 With the element's property ```.innerText``` we can:
* get/set an element's text content, but only the visible text of the element.

Resources:
* [Element: innerHTML property](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML)
* [Node: textContent property](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent)
* [HTMLElement: innerText property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText)
* [The poor, misunderstood innerText](http://perfectionkills.com/the-poor-misunderstood-innerText/)
* [innerText vs. textContent](https://kellegous.com/j/2013/02/27/innertext-vs-textcontent/)


<br>

### *Add New Page Content* <a name="add-new-page-content"></a>


```.createElement()``` method creates the HTML element specified by tagName:
* is a method on the ```document``` object;
* ```document.createElement("tagName");```;
* it just creates an element, it doesn't add it to the DOM.


```.appendChild()``` method adds an element to the page appending it (adding something to the end of a piece of writing):
* it must be called on another element, not the ```document```;
* it's a method of the Node interface;
* if the given child is a reference to an existing node in the document, ```appendChild()``` moves it from its current position to the new position;
* ```element.appendChild(newElement);```.


```.createTextNode()``` method to create a new text nodes. The element's ```.textContent()``` property is used more often than creating a text node with the ```.createTextNode()```method.


Inserting HTML in other locations with the ```.insertAdjacentHTML()``` method:
* method of the ```Element``` interface that parses the specified text as HTML or XML and inserts the resulting nodes into the DOM tree at a specified position: ```insertAdjacentHTML(position, text)```
* the second argument text of ```insertAdjacentHTML()``` method parses the specified text as HTML and inserts the resulting nodes into the DOM tree at a specified position;
* the position is a string representing the position relative to the element in one of the four positions:
1. ```beforebegin``` - inserts the HTML text as a previous sibling;
2. ```afterbegin``` - inserts the HTML text as the first child;
3. ```beforeend``` - inserts the HTML text as the last child;
4. ```afterend```- inserts the HTML text as a following sibling.



Resources:
* [Document: createElement() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)
* [Node: appendChild() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)
* [Document: createTextNode() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode)
* [Element: insertAdjacentHTML() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML)



<br>

### *Remove Page Content* <a name="remove-page-content"></a>

```.removeChild()``` method:
* method of the ```Node``` interface
* the opposite of the ```appendChild()```method;
* requires a parent element, and
* the child element that will be removed;
*   <parent-element>```.removeChild```(<child-to-remove>).


```remove()``` method:
* removes the element from the DOM;
*  <element>.remove().


```firstChild```property:
* returns the node's first child in the tree, or ```null``` if the node has no children;
* might return whitespace (if there is any) to preserve the formating of the underlying HTML source code.


```firstElementChild``` property:
* returns an element's first child ```Element```, or ```null```if there are no child elements.


```parentElement``` property:
* returns the DOM node's parent ```Element```, or ```null```if the node either has no parent, or its parent isn't a DOM ```Element```.

*If we don't have the parent element, we can call the ```parentElement``` property on the element we want to remove to refer to its parent. This way, we "move focus" to the element's parent. Then we call ```.removeChild()``` on that referenced parent Element.

Resources:
* [Node: removeChild() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild)
* [Element: remove() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/remove)
* [Node: firstChild property](https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild)
* [Element: firstElementChild property](https://developer.mozilla.org/en-US/docs/Web/API/Element/firstElementChild)
* [Node: parentElement property](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentElement)

<br>

### *Style Page Content* <a name="style-page-content"></a>

Modifying an element's style attribute:
* ```element.style.property = value```;
* we can only modify on CSS style at a time.

Adding multiple styles at once:
* return the cssText property: ```object.style.cssText```;
* set the cssText property: ```object.style.cssText = string``` (string with the list of styles/values we want to modify; here hte property names can have hyphens).

Setting an element's attributes:
* ```element.setAttribute(name, value)```;
* ```.setAttribute``` is not just for styling page elements. This method can be used to set any attribute for an element.

Accessing an element's classes:
* getting/setting a list of classes with ```.className```;
* the returned list is a space-separated string of the classes, like "class-1  class-2";
* we can convert the space-separated string into an array using the JavaScript method ```.split()```:

```const arrayOfClasses = listOfClasses.split(' ');```

```console.log(arrayOfClasses);  // ["class-1", "class-2"]```

and then we can use any different array methods to search for a class to remove it or update it.

Getting/setting/toggling CSS classes with the ```.classList``` property:
* it returns a live ```DOMTokenList``` collection of the ```class``` attributes of the element;
* it has a number of properties of is own:
* ```.add()``` to add a class to the list;
* ```.remove()``` to remove a class from the list;
* ```.toggle()``` adds a class if it doesn't exist or remove it from the list if it does;
* ```.contains()``` returns a boolean based on if the class exists on the list or not.


Resources:
* [CSS Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
* [HTMLElement: style property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
* [Element: setAttribute() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute)
* [HTMLElement: style property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style)
* [Element: className property](https://developer.mozilla.org/en-US/docs/Web/API/Element/className)
* [Element: classList property](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList)
* [Using dynamic styling information](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Using_dynamic_styling_information)
* [Element: nextElementSibling property](https://developer.mozilla.org/en-US/docs/Web/API/Element/nextElementSibling)


<br>

[Back to top](#top)

## Working with Browser Events <a name="working-with-browser-events"></a>

  1. Events - what they are <a name="events-what-they-are"></a>

* Events are actions that take place in the browser that can be initiated by either the user or the browser itself.
* The Chrome browser has a special ```monitorEvents()``` function that will let us see different events as they are occurring, and there is also the ```unmonitorEvents()``` function that will turn off the announcing of events for the targeted element (for development/testing purposes only):

```
// start displaying all events on the document object
monitorEvents(document);

// turn off the displaying of all events on the document object.
unmonitorEvents(document);
```

Resources:
* [Introduction to events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
* [Understanding Events in JavaScript](https://www.digitalocean.com/community/tutorials/understanding-events-in-javascript)
* [Console Utilities API reference](https://developer.chrome.com/docs/devtools/console/utilities/#monitorevents)

<br>

2. Responding to Events - how to listen for an event and respond when one happens <a name="responding-to-events"></a>

* An Event Target

   The EventTarget Interface is inherited by all nodes and elements: 

  ```EventTarget```  <----  ´´´Node```   <----   ```Element```
  
   The EventTarget is at the top of the chain, it doesn't inherit any properties or methods from any other interfaces, but every other interface inherits from it and therefore contain its properties and methods.
   Both the ```document``` object and any ```DOM element``` can be an event target because both the Element Interface and the Document Interface inherit from the EventTarget Interface.
   The EventTarget Interface:
   * doesn't have any properties;
   * only has three methods - ```.addEventListener()``` , ```.removeEventListener()``` , ```.dispatchEvent()``` .
  
* Adding an Event Listener
  
  * ```.addEventListener()``` method - to listen for events and respond to them.
  * How to set an event listener:
  
    ```<event-target>.addEventListener(<event-to-listen-for>, <function-to-run-when-an-event-happens>);```
  
    where:
    * ```<event-target>``` is the **target**;
    * ```<event-to-listen-for>``` is the **type** of event to listen for;
    * ```<function-to-run-when-an-event-happens>``` is a function to run when the event occurs - the ***listener***.
  
  Resources:
* [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)
* [EventTarget: addEventListener() method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
* [Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)
  
  <br>

3. Removing an Event Listener <a name="removing-an-event-listener"></a>

  * We remove an event listener using the ```.removeEventListener()``` method and passing to it the same exact listener function to it as the one we passed to ```.addEventListener()```. So we have to understand how equality works in JS.

  * Are objects (objects, arrays, and function) Equal in JavaScript
  
    Equality in JavaScript:
      - double equality (```==```) operator that will allow type coercion;
      - triple equality (```===```) that will prevent type coercion when comparing.
      - In JavaScript, objects are a reference type. Two distinct objects are never equal, even if they have the same properties. Only comparing the same object               reference with itself yields true.
      
  * Using the ```.removeEventListener()```:
  
      ```<event-target>.removeEventListener(<event-to-listen-for>, <function-to-remove>)```, where:
       - event-target is the **target**;
       - event-to-listen-for is the **type** of event to listen for; and
       - function-to-remove is the **listener** (the function to remove).
          
      So, the **listener** function must be the exact same function as the one used in the ```.addEventListener()``` call. 
      
      
      
 Resources:
  * [Equality comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
  * [Object Equality in JavaScript](http://adripofjavascript.com/blog/drips/object-equality-in-javascript.html)
  * [Comparing objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#comparing_objects)
  * [Type coercion](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion)
  * [EventTarget: removeEventListener() method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener)
  * [Easily jump to event listeners](https://developer.chrome.com/blog/easily-jump-to-event-listeners/)
      
  <br>
  
  4. Phases of an Event <a name="phases-of-an-event"></a>
  
  * Phases of the lifecycle of an event:
    * the **capturing** phase (the process by which an event can be handled by one of the target’s ancestors before being handled by the event target);
    * the **at target** phase (the process by which an event can be handled by the event target);
    * and the **bubbling** phase (the process by which an event can be handled by one of the target’s ancestors after being handled by the event target).
  
  * Most event handlers:
    * run during the **at target** phase
  
  * But sometimes, in a collection of items (such as a list), if we click on a child item and a handler doesn't intercept the click, the event will "bubble" upward to the parent, and keeps bubbling until something handles it or hits the document.
  
  * Capturing lets the parent intercept an event before it reaches a child.
  
  * Complete syntax of the ```.addEventListener()``` method:
    * addEventListener(type, listener, useCapture), where:
      * type is the **event type** to listen for;
      * listener can be ```null```, an object with a ```handleEvent()``` method, or a JS function;
      * ```useCapture``` is a boolean indicating whether events of this type will be dispatched to the registered ```listener``` before being dispatched to any                 ```eventTarget``` beneath it in the DOM tree. If not specified, ```useCapture``` defaults to false.
  
  * So, the ```.addEventListener()``` method can be called with two or three arguments:
    * if called with two arguments (event type and the listener) it will invoke the listener during the **bubbling phase**;
    * if called with three arguments (event type, the listener and useCapture being true) it will invoke the listener during the **capturing phase**.
  
  * The Event Object
  
    * The event object is a regular JS object included by the browser when an event occurs.
    * We can add a parameter to a listener function to store the **event object** (and then have access to a lot of information):
    
        ```
        document.addEventListener('click', function(event) {
          console.log('The document was clicked');
        });
        ```
        
   * The ```event``` paramenter can have the following names:
    * ```evt```
    * ```e```
    * we can give it any name we want, but it must be informative/descriptive.
    
  * The Default Action
  
    * One of the reasons to use the event object is to prevent default action from happening, like the default action of a link (navigate to the location provided by its ```href``` attribute) or on a form (data being send to the location in its ```action```attribute).
    
    * Prevent default action with the event object's ```.preventDefault()``` method: ```event.preventDefault()```
    
    ```
    target.addEventListener('click', function (event) {
    event.preventDefault();
    //code for somethign to happen
    });
    ```
    
    
  Resources:
  
  * [Event dispatch and DOM event flow](https://www.w3.org/TR/DOM-Level-3-Events/#event-flow)
  * [capture phase](https://www.w3.org/TR/DOM-Level-3-Events/#capture-phase)
  * [target phase](https://www.w3.org/TR/DOM-Level-3-Events/#target-phase)
  * [bubbling phase](https://www.w3.org/TR/DOM-Level-3-Events/#bubble-phase)
  * [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)
  * [Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)
  * [EventTarget: addEventListener() method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
  * [Event: preventDefault() method](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
  
  <br>
  
  5. Avoid Too Many Events <a name="avoid-too-many-events"></a>
  
  * When we use ```.addEventListener()``` on a common ancestor of several element and we want to access any of those elements, we use event delegation. So, event delegation is the process of delegating to a parent element the ability to manage events for child elements.
  
  * Using event delegation:
    * the event object has a ```.target``` property, that references the target of the event. So, ```event.target``` gives us access to the element we want.
    
  * Checking the Node Type in Event Delegation:
  
    * Sometimes we have to check the Node type in event delegation by, for exemple, use an if statement:
    
    ``` if (evt.target.nodeName === 'desired element') {  // ← verifies target is desired element ```
    
      * Here we are using the ```.nodeName``` property of the Node interface that is inherited
      
  * The ```.nodeName``` property
  
    * The ```nodeName``` property will return an uppercase string (not a lowercase one).
    
    * So, we can check using capital letters:
    
    ```
    if (evt.target.nodeName === 'SPAN') {
    console.log('A span was clicked with text ' + evt.target.textContent);
    }
    ```

      Or convert nodeName to lowercase:
      
    ```
    if (evt.target.nodeName.toLowerCase() === 'span') {
    console.log('A span was clicked with text ' + evt.target.textContent);
    }
    ```
    
  Resources:
  
  * [Event delegation](https://javascript.info/event-delegation)
  * [How JavaScript Event Delegation Works](https://davidwalsh.name/event-delegate)
  
  <br>
  
  6. Know When the DOM Is Ready <a name="know-when-the-dom-is-ready"></a>
  
  * The DOM is built incrementally, meaning, it is a sequencial process when the HTML is received and converted into tokens and built into the document object model. That's why it is important where the JS file is placed.
  
  * The **content is loaded event**, ```DOMContentLoaded``` event, is fired by the browser when the document object model has been fully loaded.
  
  * We can listen for the ```DOMContentLoaded``` event:
  
  ```
  document.addEventListener('DOMContentLoaded', function () {
    console.log('the DOM is ready to be interacted with!');
  });
  ```
  
  * The target of the ```DOMContentLoaded``` event is the ```document``` object.
  
  * Using the ```DOMContentLoaded``` Event:
  
    * if we want to have JS code in the ```head``` element, we have to wrapp it in an event listener for the ```DOMContentLoaded``` event. This will prevent the JS code to run before the DOM is constructed.
    
    * Example:
    
    ```
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <link rel="stylesheet" href="/css/styles.css" />
      <script>
        document.addEventListener('DOMContentLoaded', function () {
          document.querySelector('footer').style.backgroundColor = 'purple';
        });
      </script>
    ```
    
    * The ```load``` event is similar (e.g. ```document.onload(...)```), but ```load``` fires later than ```DOMContentLoaded``` (```load``` waits until all of the images, stylesheet, etc. have been loaded) (this is generally the old way).
    
    * JS code in the ```head``` should only be used if we have JS code that needs to run as soon as possible; in this case, this JS code must be wrapped in a ```DOMContentLoaded``` event listener.
    
  Resource:
  
  * [Window: DOMContentLoaded event](https://developer.mozilla.org/en-US/docs/Web/API/Window/DOMContentLoaded_event)
    
<br>

[Back to top](#top)

## Performance <a name="performance"></a>

<br>

[Back to top](#top)













