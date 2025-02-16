## topics to cover
- Hoisting
- How this works in JavaScript
- Closures
- mul function 
- recursion
- prototype - inheritance in js, how it differs from other languages

- scoping - functions as first class objects, closures, function vs block scoping

- AJAX - just general stuff, how you've used it, etc, not really super technical questions here

- Web Security - same origin policy, Cross Site Scripting, Cross Site Request Forgery, cookies (secure flag, http only flag, what to store in cookies, what not to, etc), basic session based security

- REST API design - given a random data model that I come up with on the spot, design a good API for it

- Troubleshooting techniques - race conditions, developer tools (firebug, chrome dev tools, windows script debugger), understanding that breakpoints affect the behavior of your code, proxy tools (Fiddler or the like), understanding that proxies can affect the behavior of your code (fiddler mishandles edge cases of content-encoding chunked, as an example), wireshark or similar

- code organization and dependency management - what do you do, are you familiar with AMD/require.js, commonjs, or es6 modules?

- Array functions - map/reduce/filter/reduce/sort/etc

- new ES6 features - not make-or-break, but it's good to know, babel transpiler experience also good.

- build tools - webpack, grunt, etc

- server side js - node.js, npm experience

- currently popular frameworks/libraries - don't care which, just like to hear they know about some, have an opinion, bonus points if they can give some advantages and disadvantages of a few of them.



## 1. Can you name two programming paradigms important for JavaScript app developers?

JavaScript is a multi-paradigm language, supporting imperative/procedural programming along with OOP (Object-Oriented Programming) and functional programming. JavaScript supports OOP with prototypal inheritance.

## 2. What is functional programming?

Functional programming produces programs by composing mathematical functions and avoids shared state & mutable data. Lisp (specified in 1958) was among the first languages to support functional programming, and was heavily inspired by lambda calculus. Lisp and many Lisp family languages are still in common use today.

Functional programming is an essential concept in JavaScript (one of the two pillars of JavaScript). Several common functional utilities were added to JavaScript in ES5.

## 3. What is the difference between classical inheritance and prototypal inheritance?

Class Inheritance: instances inherit from classes (like a blueprint — a description of the class), and create sub-class relationships: hierarchical class taxonomies. Instances are typically instantiated via constructor functions with the ```new``` keyword. Class inheritance may or may not use the `class` keyword from ES6.

Prototypal Inheritance: instances inherit directly from other objects. Instances are typically instantiated via factory functions or `Object.create()`. Instances may be composed from many different objects, allowing for easy selective inheritance. 
## 4. What are the pros and cons of functional programming vs object-oriented programming?
OOP Pros: It’s easy to understand the basic concept of objects and easy to interpret the meaning of method calls. OOP tends to use an imperative style rather than a declarative style, which reads like a straight-forward set of instructions for the computer to follow.

OOP Cons: OOP Typically depends on shared state. Objects and behaviors are typically tacked together on the same entity, which may be accessed at random by any number of functions with non-deterministic order, which may lead to undesirable behavior such as race conditions.

FP Pros: Using the functional paradigm, programmers avoid any shared state or side-effects, which eliminates bugs caused by multiple functions competing for the same resources. With features such as the availability of point-free style (aka tacit programming), functions tend to be radically simplified and easily recomposed for more generally reusable code compared to OOP.

FP also tends to favor declarative and denotational styles, which do not spell out step-by-step instructions for operations, but instead concentrate on what to do, letting the underlying functions take care of the how. This leaves tremendous latitude for refactoring and performance optimization, even allowing you to replace entire algorithms with more efficient ones with very little code change. (e.g., memoize, or use lazy evaluation in place of eager evaluation.)

Computation that makes use of pure functions is also easy to scale across multiple processors, or across distributed computing clusters without fear of threading resource conflicts, race conditions, etc…

FP Cons: Over exploitation of FP features such as point-free style and large compositions can potentially reduce readability because the resulting code is often more abstractly specified, more terse, and less concrete.

More people are familiar with OO and imperative programming than functional programming, so even common idioms in functional programming can be confusing to new team members.

FP has a much steeper learning curve than OOP because the broad popularity of OOP has allowed the language and learning materials of OOP to become more conversational, whereas the language of FP tends to be much more academic and formal. FP concepts are frequently written about using idioms and notations from lambda calculus, algebras, and category theory, all of which requires a prior knowledge foundation in those domains to be understood.

## 5. When is classical inheritance an appropriate choice?
The answer is never, or almost never. Certainly never more than one level. Multi-level class hierarchies are an anti-pattern. I’ve been issuing this challenge for years, and the only answers I’ve ever heard fall into one of several common misconceptions. More frequently, the challenge is met with silence.

## 6. When is prototypal inheritance an appropriate choice?
There is more than one type of prototypal inheritance:

- Delegation (i.e., the prototype chain).
- Concatenative (i.e. mixins, `Object.assign()`).
- Functional (Not to be confused with functional programming. A function used to create a closure for private state/encapsulation).

Each type of prototypal inheritance has its own set of use-cases, but all of them are equally useful in their ability to enable composition, which creates has-a or uses-a or can-do relationships as opposed to the is-a relationship created with class inheritance.

## 7. What does “favor object composition over class inheritance” mean?
This is a quote from “Design Patterns: Elements of Reusable Object-Oriented Software”. It means that code reuse should be achieved by assembling smaller units of functionality into new objects instead of inheriting from classes and creating object taxonomies.

In other words, use can-do, has-a, or uses-a relationships instead of is-a relationships.
## 8. What are two-way data binding and one-way data flow, and how are they different?
Two way data binding means that UI fields are bound to model data dynamically such that when a UI field changes, the model data changes with it and vice-versa.

One way data flow means that the model is the single source of truth. Changes in the UI trigger messages that signal user intent to the model (or “store” in React). Only the model has the access to change the app’s state. The effect is that data always flows in a single direction, which makes it easier to understand.

One way data flows are deterministic, whereas two-way binding can cause side-effects which are harder to follow and understand.
## 9. What are the pros and cons of monolithic vs microservice architectures?
A monolithic architecture means that your app is written as one cohesive unit of code whose components are designed to work together, sharing the same memory space and resources.

A microservice architecture means that your app is made up of lots of smaller, independent applications capable of running in their own memory space and scaling independently from each other across potentially many separate machines.

Monolithic Pros: The major advantage of the monolithic architecture is that most apps typically have a large number of cross-cutting concerns, such as logging, rate limiting, and security features such audit trails and DOS protection.

When everything is running through the same app, it’s easy to hook up components to those cross-cutting concerns.

There can also be performance advantages, since shared-memory access is faster than inter-process communication (IPC).

Monolithic cons: Monolithic app services tend to get tightly coupled and entangled as the application evolves, making it difficult to isolate services for purposes such as independent scaling or code maintainability.

Monolithic architectures are also much harder to understand, because there may be dependencies, side-effects, and magic which are not obvious when you’re looking at a particular service or controller.

Microservice pros: Microservice architectures are typically better organized, since each microservice has a very specific job, and is not concerned with the jobs of other components. Decoupled services are also easier to recompose and reconfigure to serve the purposes of different apps (for example, serving both the web clients and public API).

They can also have performance advantages depending on how they’re organized because it’s possible to isolate hot services and scale them independent of the rest of the app.

Microservice cons: As you’re building a new microservice architecture, you’re likely to discover lots of cross-cutting concerns that you did not anticipate at design time. A monolithic app could establish shared magic helpers or middleware to handle such cross-cutting concerns without much effort.

In a microservice architecture, you’ll either need to incur the overhead of separate modules for each cross-cutting concern, or encapsulate cross-cutting concerns in another service layer that all traffic gets routed through.

Eventually, even monolthic architectures tend to route traffic through an outer service layer for cross-cutting concerns, but with a monolithic architecture, it’s possible to delay the cost of that work until the project is much more mature.

Microservices are frequently deployed on their own virtual machines or containers, causing a proliferation of VM wrangling work. These tasks are frequently automated with container fleet management tools.
## 10. What is asynchronous programming, and why is it important in JavaScript?
Synchronous programming means that, barring conditionals and function calls, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.

Asynchronous programming means that the engine runs in an event loop. When a blocking operation is needed, the request is started, and the code keeps running without blocking for the result. When the response is ready, an interrupt is fired, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations.

User interfaces are asynchronous by nature, and spend most of their time waiting for user input to interrupt the event loop and trigger event handlers.

Node is asynchronous by default, meaning that the server works in much the same way, waiting in a loop for a network request, and accepting more incoming requests while the first one is being handled.

This is important in JavaScript, because it is a very natural fit for user interface code, and very beneficial to performance on the server.
## 11. What is a “closure” in JavaScript? Provide an example
A closure is a function defined inside another function (called the parent function), and has access to variables that are declared and defined in the parent function scope.

The closure has access to variables in three scopes:

- Variables declared in their own scope
- Variables declared in a parent function scope
- Variables declared in the global namespace
```
var globalVar = "abc"; 

// Parent self invoking function 
(function outerFunction (outerArg) { // begin of scope outerFunction
    // Variable declared in outerFunction function scope 
    var outerFuncVar = 'x';    
    // Closure self-invoking function 
    (function innerFunction (innerArg) { // begin of scope innerFunction
        // variable declared in innerFunction function scope
        var innerFuncVar = "y"; 
        console.log(          
            "outerArg = " + outerArg + "\n" +
            "outerFuncVar = " + outerFuncVar + "\n" +
            "innerArg = " + innerArg + "\n" +
            "innerFuncVar = " + innerFuncVar + "\n" +
            "globalVar = " + globalVar);
 
    }// end of scope innerFunction)(5); // Pass 5 as parameter 
}// end of scope outerFunction )(7); // Pass 7 as parameter 
```

## 12. How to empty an array in JavaScript?
For instance,
```
 var arrayList =  ['a','b','c','d','e','f'];
 ```


There are a couple ways we can use to empty an array, so let's discuss them all.

- Method 1
```
arrayList = []
```
Above code will set the variable arrayList to a new empty array. This is recommended if you don't have references to the original array arrayList anywhere else, because it will actually create a new, empty array. You should be careful with this method of emptying the array, because if you have referenced this array from another variable, then the original reference array will remain unchanged.

For Instance,
```
var arrayList = ['a','b','c','d','e','f']; // Created array 
var anotherArrayList = arrayList;  // Referenced arrayList by another variable 
arrayList = []; // Empty the array 
console.log(anotherArrayList); // Output ['a','b','c','d','e','f']
```
- Method 2
```
arrayList.length = 0;
```
The code above will clear the existing array by setting its length to 0. This way of emptying the array also updates all the reference variables that point to the original array. Therefore, this method is useful when you want to update all reference variables pointing to arrayList.

For Instance,
```
var arrayList = ['a','b','c','d','e','f']; // Created array 
var anotherArrayList = arrayList;  // Referenced arrayList by another variable 
arrayList.length = 0; // Empty the array by setting length to 0
console.log(anotherArrayList); // Output []
```
- Method 3
```
arrayList.splice(0, arrayList.length);
```
The implementation above will also work perfectly. This way of emptying the array will also update all the references to the original array.
```
var arrayList = ['a','b','c','d','e','f']; // Created array 
var anotherArrayList = arrayList;  // Referenced arrayList by another variable 
arrayList.splice(0, arrayList.length); // Empty the array by setting length to 0
console.log(anotherArrayList); // Output []
Method 4
while(arrayList.length){
  arrayList.pop();
}
```

## 13. What is function hoisting in JavaScript?
Function Expression
```
var foo = function foo(){ 
 	return 12; 
}; 
```
In JavaScript, variable and functions are hoisted. Let's take function hoisting first. Basically, the JavaScript interpreter looks ahead to find all variable declarations and then hoists them to the top of the function where they're declared. For example:
```
foo(); // Here foo is still undefined 
var foo = function foo(){ 
 	return 12; 
}; 
```

## 14. What is the difference between declaring a function in the two formats below?
```
var foo = function() {
/* Some code */
};
```
```
function bar() {
/* Some code */
};
```
The main difference is the function foo is defined at run-time whereas function bar is defined at parse time. To understand this in better way, let's take a look at the code below:

Run-Time function declaration 
```
<script>
foo(); // Calling foo function here will give an Error
  var foo = function(){ 
    console.log("Hi I am inside Foo");
 }; 
 </script>
 <script>
Parse-Time function declaration 
bar(); // Calling foo function will not give an Error
 function bar(){ 
  console.log("Hi I am inside Foo");
 }; 
</script>
```
## 16. What is the drawback of declaring methods directly in JavaScript objects?
One of the drawbacks of declaring methods directly in JavaScript objects is that they are very memory inefficient.


## 17.  Write a mul function which will work properly when invoked with following syntax.
```
console.log(mul(2)(3)(4)); // output : 24
console.log(mul(4)(3)(4)); // output : 48
Answer
function mul (x) {
  return function (y) { // anonymous function
    return function (z) { // anonymous function
      return x * y * z;
    };
  };
}
```
Here the mul function accepts the first argument and returns an anonymous function which then takes the second parameter and returns one last anonymous function which finally takes the third and final parameter; the last function then multiplies x, y and z, and returns the result of the operation.

In Javascript, a function defined inside another function has access to the outer function's scope and can consequently return, interact with or pass on to other functions, the variables belonging to the scopes that incapsulate it.

- A function is an instance of the Object type
- A function can have properties and has a link to its constructor method
- A function can be stored as a variable
- A function can be passed as a parameter to another function
- A function can be returned by another function
## 18. What will be the output of the following code?
```
var output = (function(x) {
  delete x;
  return x;
})(0);

console.log(output);
```
The code above will output 0 as output. delete operator is used to delete a property from an object. Here x is not an object, it's a local variable. delete operator doesn't affect local variables.

## 19. What will be the output of the following code?
```
var x = 1;
var output = (function() {
  delete x;
  return x;
})();

console.log(output);
```
The code above will output 1 as output. delete operator is used to delete a property from an object. Here x is not an object it's global variable of type number.

## 20.  What is negative Infinity?
Negative Infinity is a number in JavaScript which can be derived by dividing negative number by zero.

## 21. What is the use of the Push method in JavaScript?
The push method is used to add or append one or more elements to an Array end. Using this method, we can append multiple elements by passing multiple arguments.

## 22. What is event bubbling?
JavaScript allows DOM elements to be nested inside each other. In such a case, if the handler of the child is clicked, the handler of the parent will also work as if it were clicked too.

## 23.  What are some important JavaScript Unit Testing Frameworks?
Following is a curated list of popular JavaScript Unit Testing Frameworks and Tools that are widely used :

- Unit.js: It is known as an open-source assertion library running on browser and Node.js. It is extremely compatible with other JavaScript Unit Testing frameworks like Mocha, Karma, Jasmine, QUnit, Protractor, etc. Provides the full documented API of assertion list.

- QUnit: It is used for both client-side and server-side JavaScript Unit Testing. This Free JavaScript testing framework is used for jQuery projects. It follows Common JS unit testing Specification for unit testing in JavaScript. It supports the Node Long-term Support Schedule.

- Jasmine: Jasmine is the behavior-driven development framework to unit test JavaScript. It is used for testing both synchronous and asynchronous JavaScript codes. It does not require DOM and comes with an easy syntax that can be written for any test.

- Karma: Karma is an open-source productive testing environment. Easy workflow control running on the command line. Offers the freedom to write the tests with Jasmine, Mocha, and QUnit. You can run the test on real devices with easy debugging.

- Mocha: Mocha runs on Node.js and in the browser. Mocha performs asynchronous testing more simply. Provides accuracy and flexibility in reporting. Provides tremendous support of rich features such as test-specific timeouts, JavaScript APIs.

- Jest: Facebook uses jest so far to test all the JavaScript code. It provides the ‘zero-configuration testing experience. Supports independent and non-interrupting running tests without any conflict. Do not require any other setup configuration and libraries.

- AVA: AVA is a simple JavaScript Unit Testing Framework. Tests are being run in parallel and serially. Parallel tests run without interrupting each other. This testing framework supports asynchronous testing as well. AVA uses subprocesses to run the unit test JavaScript.

## 24. What is Event Propagation?
↑ When an event occurs on a DOM element, that event does not entirely occur on that just one element. In the Bubbling Phase, the event bubbles up or it goes to its parent, to its grandparents, to its grandparent's parent until it reaches all the way to the window while in the Capturing Phase the event starts from the window down to the element that triggered the event or the event.target.

Event Propagation has three phases.

- Capturing Phase – the event starts from window then goes down to every element until it reaches the target element.
- Target Phase – the event has reached the target element.
- Bubbling Phase – the event bubbles up from the target element then goes up every element until it reaches the window.

![](https://res.cloudinary.com/practicaldev/image/fetch/s--pU4TmVPB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https://thepracticaldev.s3.amazonaws.com/i/hjayqa99iejfhbsujlqd.png)
## 25.  What's Event Bubbling?
↑ When an event occurs on a DOM element, that event does not entirely occur on that just one element. In the Bubbling Phase, the event bubbles up or it goes to its parent, to its grandparents, to its grandparent's parent until it reaches all the way to the window.

If we have an example markup like this.
```
 <div class="grandparent">
    <div class="parent">
      <div class="child">1</div>
    </div>
  </div>
```
And our js code.
```
function addEvent(el, event, callback, isCapture = false) {
  if (!el || !event || !callback || typeof callback !== 'function') return;
  if (typeof el === 'string') {
    el = document.querySelector(el);
  };
  el.addEventListener(event, callback, isCapture);
}

addEvent(document, 'DOMContentLoaded', () => {
  const child = document.querySelector('.child');
  const parent = document.querySelector('.parent');
  const grandparent = document.querySelector('.grandparent');

  addEvent(child, 'click', function (e) {
    console.log('child');
  });

  addEvent(parent, 'click', function (e) {
    console.log('parent');
  });

  addEvent(grandparent, 'click', function (e) {
    console.log('grandparent');
  });

  addEvent(document, 'click', function (e) {
    console.log('document');
  });

  addEvent('html', 'click', function (e) {
    console.log('html');
  })

  addEvent(window, 'click', function (e) {
    console.log('window');
  })

});
```
The addEventListener method has a third optional parameter useCapture with a default value of false the event will occur in the Bubbling phase if true the event will occur in the Capturing Phase. If we click on the child element it logs child,parent,grandparent, html, document and window respectively on the console. This is Event Bubbling.

## 26. What's the difference between event.preventDefault() and event.stopPropagation() methods?
↑ The event.preventDefault() method prevents the default behavior of an element. If used in a form element it prevents it from submitting. If used in an anchor element it prevents it from navigating. If used in a contextmenu it prevents it from showing or displaying. While the event.stopPropagation() method stops the propogation of an event or it stops the event from occurring in the bubbling or capturing phase.

## 27.  What does the !! operator do?
↑ The Double NOT operator or !! coerces the value on the right side into a boolean. basically it's a fancy way of converting a value into a boolean.
```
console.log(!!null); //logs false
console.log(!!undefined); //logs false
console.log(!!''); //logs false
console.log(!!0); //logs false
console.log(!!NaN); //logs false
console.log(!!' '); //logs true
console.log(!!{}); //logs true
console.log(!![]); //logs true
console.log(!!1); //logs true
console.log(!![].length); //logs false
```

## 28. What is Hoisting?
↑ Hoisting is the term used to describe the moving of variables and functions to the top of their (global or function) scope on where we define that variable or function.

Ok to understand Hoisting, I have to explain the execution context.
The Execution Context is the "environment of code" that is currently executing. The Execution Context has two phases compilation and execution.

Compilation - in this phase it gets all the function declarations and hoists them up to the top of their scope so we can reference them later and gets all variables declaration (declare with the var keyword) and also hoists them up and give them a default value of undefined.

Execution - in this phase it assigns values to the variables hoisted earlier and it executes or invokes functions (methods in objects).

## 29. What is the prototype of an object?
↑ A prototype in simplest terms is a blueprint of an object. It is used as a fallback for properties and methods if it does exist in the current object. It's the way to share properties and functionality between objects. It's the core concept around JavaScript's Prototypal Inheritance.
```
  const o = {};
  console.log(o.toString()); // logs [object Object] 
```
Even though the o.toString method does not exist in the o object it does not throw an error instead returns a string [object Object]. When a property does not exist in the object it looks into its prototype and if it still does not exist it looks into the prototype's prototype and so on until it finds a property with the same in the Prototype Chain. The end of the Prototype Chain is null after the Object.prototype.
```
   console.log(o.toString === Object.prototype.toString); // logs true
   // which means we we're looking up the Prototype Chain and it reached 
   // the Object.prototype and used the "toString" method.
```
## 30.  What's the difference between Function.prototype.apply and Function.prototype.call?
↑ The only difference between apply and call is how we pass the arguments in the function being called. In apply we pass the arguments as an array and in call we pass the arguments directly in the argument list.
```
const obj1 = {
 result:0
};

const obj2 = {
 result:0
};

function reduceAdd(){
   let result = 0;
   for(let i = 0, len = arguments.length; i < len; i++){
     result += arguments[i];
   }
   this.result = result;
}

reduceAdd.apply(obj1, [1, 2, 3, 4, 5]); // returns 15
reduceAdd.call(obj2, 1, 2, 3, 4, 5); // returns 15
```
## 31.  What is Object Destructuring?
↑ Object Destructuring is a new and cleaner way of getting or extracting values from an object or an array.
## 32.  Show the usage of typeof operator on different types of values
The typeof operator returns a string indicating the type of the operand
```
typeof 50; //   "number"
typeof "text"; //   "string"
typeof true; //   "boolean"
typeof undefined; //   "undefined"
typeof function () {}; //   "function"
typeof 10n; //   "bigint"
typeof Symbol(); //   "symbol"
typeof [1, 2]; //   "object"
typeof {}; //   "object"
 
typeof NaN; //   "number"        (NaN is Not a Number)
typeof undeclaredVar; //   "undefined"     (undeclaredVariable is never declared)
typeof Infinity; //   "number"        (Infinity, -Infinity, -0 are all valid numbers in JavaScript)
typeof null; //   "object"        (This stands since the beginning of JavaScript)
typeof /regex/; //   "object"        (regular expressions start and end with '/' in literal form)
```
## 33.  Show the different ways of concatenating numbers and strings
```
// numbers and strings
1 + "2"; // 12
1 + 2 + "3"; // 33
1 + 2 + "3" + "4"; // 334
1 + "One"; // 1One
 
// strings and numbers
"1" + 2; // 12
"1" + "2" + 3; // 123
"1" + "2" + 3 + 4; // 1234
"1" + "2" + (3 + 4); // 127
"One" + 1; // One1
 
// mix of string and numbers
1 + 2 + "3" + "4" + 5 + 6; // 33456
1 + 2 + "3" + "4" + (5 + 6); // 33411
"1" + "2" + (3 + 4) + 5 + "6"; // 12756
```
## 34. Show the conversion from number to string and vice versa
```
// number to string conversion
const num = 12;
 
String(num); // "12"
num.toString(); // "12"
num + ""; // "12"

// string to number conversion
const str = "12";
 
Number(str); // 12
+str; // 12
parseInt(str); // 12
```

## 35. Show the frequently and commonly used methods available on Number object with coding examples
- isInteger is used to check if the given number is integer or not
- parseInt is used to convert a given value in to integer
- parseFloat is used to convert a given value in to floating number
- isNaN is used to check if the given value is NaN or no
- toFixed is used to limit the number of digits after the decimal place
- toPrecision is used to limit the total number of digits to represent the number
```
Number.isInteger(1.5); // false
Number.isInteger(-15); // true
 
Number.parseInt("5.8"); // 5
Number.parseInt("123x"); // 123
 
Number.parseFloat("5.86"); // 5.86
Number.parseFloat("-12.69x"); // -12.69
 
Number.isNaN(NaN); // true
Number.isNaN("text" - 10); // true
Number.isNaN("text"); // false

(56.369).toFixed(2); // 56.37
(59).toFixed(3); // 59.000
 
(32.458).toPrecision("3"); // 32.5
(98.1).toPrecision(1); // 1e+2
```
## 36. Create a function which returns a random number in the given range of values both inclusive
Math.random function returns a floating-point, pseudo-random number between 0 (inclusive) and 1 (exclusive)
```
function randomNumberGeneratorInRange(rangeStart, rangeEnd) {
  return rangeStart + Math.round(Math.random() * (rangeEnd - rangeStart));
}
 
randomNumberGeneratorInRange(10, 50); // 12
```
## 37. Write a program to reverse a string
- String can be reversed by iterating it and storing it in reverse order
- String can also be reversed by converting it to array, then joining it after reversing
```
const str = "JavaScript is awesome";
let reversedString = "";
for (let i = 0; i < str.length; i++) {
  reversedString = str.charAt(i) + reversedString;
}
 
reversedString; // "emosewa si tpircSavaJ"

const str = "JavaScript is awesome";
str.split("").reverse().join(""); // "emosewa si tpircSavaJ"
```
## 38.  Write a program to reverse a given integer number
- The remainder of the number can be fetched and the number can be divided by 10 to remvoe the the digit in loop till number becomes 0
- A simple approach to reverse a number could also be to convert it in to a string and then reverse it
```
let num = 3849;
 
let reversedNum = 0;
while (num !== 0) {
  reversedNum = reversedNum * 10 + (num % 10);
  num = Math.floor(num / 10);
}
 
reversedNum; // 9483
```
```
let num = 3849;
 
let numStr = String(num);
+numStr.split("").reverse().join(""); // 9483
```
## 39. Write a function to truncate a string to a certain number of letters
```
// Example
truncateString("JavaScript", 7); // "Java..."
truncateString("JS is fun", 10); // "JS is fun"
truncateString("JS is funny", 10); // "JS is f..."
```
- Text can be truncated by fetching the substring from start till the count of characters
- substr methods of String can be used to fetch the part of the string
```
function truncateString(str, charCount) {
  if (str.length > charCount) {
    return str.substr(0, charCount - 3) + "...";
  } else {
    return str;
  }
}
```
## 40. Write a code to truncate a string to a certain number of words
```
const str = "JavaScript is simple but not easy to master";
const wordLimit = 3;
 
str.split(" ").slice(0, wordLimit).join(" "); // "JavaScript is simple"
```
## 41.  Create a function which returns random hex color code
- The color code is popularly represented in hexadecimal format for RGB colors
- The minimum value for the color is '#000000' and maximum is '#FFFFFF'
```
function getGetHEXColorCode() {
  const rValue = Math.round(0xff * Math.random())
    .toString(16)
    .padStart(2, "0");
  const gValue = Math.round(0xff * Math.random())
    .toString(16)
    .padStart(2, "0");
  const bValue = Math.round(0xff * Math.random())
    .toString(16)
    .padStart(2, "0");
  return "#" + rValue + gValue + bValue;
}
```
## 42.  Explain hoisting in JavaScript.

Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope during the compile phase.
```
console.log(x);  // Output: undefined
var x = 10;
console.log(x);  // Output: 10
```
## 43. Show the most common ways of creating functions in JavaScript
Functions are most commonly created using function statements, function expressions and arrow functions
Function statements get hoisted unlike function expressions
```
// Regular function as a function statement
function functionName(params) {
  //code block
}

// Regular function as a function expression
const functionName = function (params) {
  //code block
};

// Arrow function as a function expression
const arrowFunctionName = (params) => {
  //code block
};
```
## 44. Achieve prototypal inheritance using functions to create objects in JavaScript
- 2 functions can be used to create objects with constructor call to the functions
- The prototype of the child function is connected with the parent function to achieve the inheritance behavior
```
function parent(name) {
  this.name = name;
}
 
parent.prototype.getName = function () {
  return this.name;
};
 
function child(name) {
  parent.call(this, name);
}
 
child.prototype = Object.create(parent.prototype);
child.prototype.getMyName = function () {
  return this.name;
};
 
// driver code
var fk = new child("FK");
console.log(fk.getName());
console.log(fk.getMyName());
 
var pk = new parent("PK");
console.log(pk.getName());
```

## 45.  Write a code to show the differences between the techniques, currying and partial application
A function returning another function that might return another function, but every returned function must take only one parameter at a time is currying
A function returning another function that might return another function, but each returned function can take several parameters is partial application
```
// currying
function multiply(num1) {
  return function (num2) {
    return function (num3) {
      return num1 * num2 * num3;
    };
  };
}

// partial application
function multiply(num1) {
  return function (num2, num3) {
    return function (num4) {
      return num1 * num2 * num3 * num4;
    };
  };
}
```
## 46.  Write a function which helps to achieve multiply(a)(b) and returns product of a and b
```
// Example
multiply(2)(4); // 8
multiply(5)(3); // 15
```
The implementation of this can be achieved by calling a function which returns a function
```
function multiply(num1) {
  return function (num2) {
    return num1 * num2;
  };
}
```
## 47. Show the different ways of creating an object
- Object can be created using Object constuctor
- Object can also be created using Object literal form
- Object can be created using new keyword to constructor function
- Object can be created using Class
```
const object = Object.create({ key: value });

const object = {
  key: value,
};
```
```
function getObject(key, value) {
  this[key] = value;
}
```
```
const object = new getObject("key", "value");
```
```
class Obj {
  constructor(key, value) {
    this[key] = value;
  }
}
```
```
const object = new Obj("key", "value");
```
## 48. What is currying in JavaScript?
Currying is an advanced technique to transform a function of arguments n, to n functions of one or fewer arguments.Currying is when you break down a function that takes multiple arguments into a series of functions that each take only one argument

Example of a curried function:
```
function add (a) {
  return function(b){
    return a + b;
  }
}

add(3)(4) 
```
For Example, if we have a function f(a,b), then the function after currying, will be transformed to f(a)(b).

By using the currying technique, we do not change the functionality of a function, we just change the way it is invoked.

Let’s see currying in action:
```
function multiply(a,b){
  return a*b;
}

function currying(fn){
  return function(a){
    return function(b){
      return fn(a,b);
    }
  }
}

var curriedMultiply = currying(multiply);

multiply(4, 3); // Returns 12

curriedMultiply(4)(3); // Also returns 12
```
## 49. What are classes in javascript?
Introduced in the ES6 version, classes are nothing but syntactic sugars for constructor functions. They provide a new way of declaring constructor functions in javascript.  Below are the examples of how classes are declared and used:
```
// Before ES6 version, using constructor functions
function Student(name,rollNumber,grade,section){
  this.name = name;
  this.rollNumber = rollNumber;
  this.grade = grade;
  this.section = section;
}

// Way to add methods to a constructor function
Student.prototype.getDetails = function(){
  return 'Name: ${this.name}, Roll no: ${this.rollNumber}, Grade: ${this.grade}, Section:${this.section}';
}


let student1 = new Student("Vivek", 354, "6th", "A");
student1.getDetails();
// Returns Name: Vivek, Roll no:354, Grade: 6th, Section:A

// ES6 version classes
class Student{
  constructor(name,rollNumber,grade,section){
    this.name = name;
    this.rollNumber = rollNumber;
    this.grade = grade;
    this.section = section;
  }

  // Methods can be directly added inside the class
  getDetails(){
    return 'Name: ${this.name}, Roll no: ${this.rollNumber}, Grade:${this.grade}, Section:${this.section}';
  }
}

let student2 = new Student("Garry", 673, "7th", "C");
student2.getDetails();
// Returns Name: Garry, Roll no:673, Grade: 7th, Section:C
```
Key points to remember about classes:

- Unlike functions, classes are not hoisted. A class cannot be used before it is declared.
- A class can inherit properties and methods from other classes by using the extend keyword.
- All the syntaxes inside the class must follow the strict mode(‘use strict’) of javascript. An error will be thrown if the strict mode rules are not followed

[few important one ](https://www.interviewbit.com/javascript-interview-questions/#output-of-following-code-1)

## 50.  What is the value of -'34'+10

 -24. minus(-) in front of a string is an unary operator that will convert the string to a number and will make it negative. Hence, -'34' becomes, -34 and then plus (+) will perform simple addition as both the operands are number.

## 51. Question: What is the value of +'dude'

Answer: NaN. The plus (+) operator in front of a string is an unary operator that will try to convert the string to number. Here, JavaScript will fail to convert the "dude" to a number and will produce NaN.

## 52. What is event bubble? How does event flows?

Answer: To understand event bubble, you have to understand what happen when you click on anything on a page.

Where you clicked: If you have a table with multiple rows and multiple columns and you click in one of the cell

- You will think that you have clicked on the cell and browser will know that you have a click handler with the cell that will be fired immediately.
- You are completely wrong. Right away, browser doesn't know where you have clicked.

The way browser find out where you have clicked are as follows-

- Capture: When you clicked, browser knows a click event occurred. It starts from the window (lowest level/root of your website), then goes to document, then html root tag, then body, then table... its trying to reach the the as lowest level of element as possible. This is called capture phase (phase -1).
- Target: When browser reach the lowest level of element. In this case, you have clicked on a table cell (table data) hence target would be "td" tag. Then browser checks whether you have any click handler attached to this element. If there is any, browser executes that click hander. This is called target phase (phase -2).
- Bubbling: After firing click hander attached to "td", browser walks toward root. One level upward and check whether there is any click handler attached with table row ("tr" element). If there is any it will execute that. Then it goes to tbody, table, body, html, document, window. In this stage its moving upward and this is called event bubbling or bubbling phase (phase-3). Please note that, you clicked on cell but all the event handler with parent elements will be fired. This is actually very powerful (check event delegation)

## 53. What is reflow? What causes reflow? How could you reduce reflow?

reflow: When you change size or position of an element in the page, all the elements after it has to change their position according to the changes you made. For example, if you change height on an element, all the elements under it has to move down in the page to accomodate a change in height. Hence, flow of the elements in the page is changed and this is called reflow.

Why reflow is bad: Reflows could be very expensive and it might have a performance hit specially in the smaller devices like phone. As it might causes changes in the portion (or whole) layout of the page.

## 54. few rapid fire
### Nth root of number
```
const nthRoot = (x, n) => Math.pow(x, 1 / n);
nthRoot(32, 5); // 2
```
### Logarithm in specific base
```
const logBase = (n, base) => Math.log(n) / Math.log(base);
logBase(10, 10); // 1
logBase(100, 10); // 2
```
### Generates Gaussian (normally distributed) random numbers.

```
const randomGauss = () => {
  const theta = 2 * Math.PI * Math.random();
  const rho = Math.sqrt(-2 * Math.log(1 - Math.random()));
  return (rho * Math.cos(theta)) / 10.0 + 0.5;
};
randomGauss(); // 0.5

```

### Sums all the numbers between 1 and n.
```
const sumN = n => (n * (n + 1)) / 2;
sumN(100); // 5050
```
### Number has decimal digits
```
const hasDecimals = num => num % 1 !== 0;

hasDecimals(1); // false
hasDecimals(1.001); // true
```
### Number is prime
```
const isPrime = num => {
  const boundary = Math.floor(Math.sqrt(num));
  for (let i = 2; i <= boundary; i++) if (num % i === 0) return false;
  return num >= 2;
};

isPrime(11); // true
```
### Checks if all the elements in values are included in arr.
```
const includesAll = (arr, values) => values.every(v => arr.includes(v));

includesAll([1, 2, 3, 4], [1, 4]); // true
includesAll([1, 2, 3, 4], [1, 5]); // false
```

### 


## 55.  Show the different ways of creating an array
- Arrays are the collection of values in javascript. Array is a special type of object in JavaScript
- Arrays values are indexed from 0 and have special property length which stores the count of elements present in array
```
// literal form
const arr = [];

// consturctor form
const arr = new Array();

// pre defined number of slots
const arr = new Array(10);

// with values
const arr = [1, true, "string"];

// constructor form with values
const arr = new Array(1, true, "string");
```
## 56. Write a program to iterate over an array and print all the values of it
- Arrays can be iterated by using its index to fetch the values
- Arrays also can be iterated with for each style loops
```
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

for (let index in arr) {
  console.log(arr[index]);
}

for (let value of arr) {
  console.log(value);
}

arr.forEach((val) => console.log(val));
```
## 57. Check if given input is an array or not
Array.isArray is a method which checks if the given argument is an array or not
Alternatively the toString method present on Object prototype can be used to check if it is an array
```
Array.isArray(arr);
```
```
Object.prototype.toString.call(arr) === "[object Array]";
```
## 58.  Write a program to iterate over a 2 dimensional array and print all the values of it
- Arrays can be iterated by using its index to fetch the values
- Arrays also can be iterated with for each style loops, with one loop to iterate the rows and inside it for cells
```
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}

for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr[i].length; j++) {
    console.log(arr[i][j]);
  }
}

for (let rowArr of arr) {
  for (let value of rowArr) {
    console.log(value);
  }
}

arr.forEach((rowArr) => rowArr.forEach((val) => console.log(val)));
```

## 59. Write a code to iterate over a map
- Map does not contain any keys by default unlike objects which has keys from its prototype
- Map's keys can be any value (including functions, objects, or any primitive) unlike object where keys are only strings
- The keys in Map are ordered in a simple, straightforward way
- The number of items in a Map is easily retrieved from its size property
- Map is an iterable object
- map is an iterable object and can be iterated using for..of loop
- map can also be iterated by simple forEach loop
```
for (let val of map) console.log(val[0], val[1]);

for (let key of map.keys()) console.log(key, map.get(key));

map.forEach((value, key) => console.log(key, value));
```
## 60. Write a program to polyfill filter functionality of the Array
- filter iterates over the all values of array and passes value, index and array (itself) as the arguments
- Function returns a new array which filtering the values of the original array
```
if (!Array.prototype.filter) {
  Array.prototype.filter = function (callback) {
    if (typeof callback !== "function")
      throw new Error("Argument passed has to be a function");
 
    let newArray = [];
 
    for (let index in this) {
      if (callback(this[index], index, this)) {
        newArray.push(this[index]);
      }
    }
    return newArray;
  };
}
```
## 61.  Write a program to polyfill map functionality of the Array
- map iterates over the all values of array and passes value, index and array (itself) as the arguments
- Function returns a new array which is same as the length of the original array
```
if (!Array.prototype.map) {
  Array.prototype.map = function (callback) {
    if (typeof callback !== "function")
      throw new Error("Argument passed has to be a function");
 
    let newArray = [];
 
    for (let index in this) {
      newArray.push(callback(this[index], index, this));
    }
    return newArray;
  };
}
```
## 62. Sort the given array of objects in ascending order according the authors lastname
```
// Example
const books = [
  { name: "Harry Potter", author: "Joanne Rowling" },
  { name: "Warcross", author: "Marie Lu" },
  { name: "The Hunger Games", author: "Suzanne Collins" },
];
```
- sort takes a function and expects the return value to be an integer for sorting
- The last names of the author can be compared and the result can be returned for sorting
```
books.sort((book1, book2) => {
  const authorLastName1 = book1.author.split(" ")[1];
  const authorLastName2 = book2.author.split(" ")[1];
  return authorLastName2 > authorLastName1 ? -1 : 1;
});
```
## 63. Write a code to generate an array with range of numbers and shuffle them
- An array of numbers in the range can be generated from a function which can take start and end value of the range
The shuffling can be achieved simply by sorting the array using a function which randomly returns positive or negative numbers
- The shuffling of the values can be also done by picking a value from a random index from the current array and moving it in to a new array
```
function rangeGenFunc(start = 1, end = 0) {
  const arr = [];
  for (let i = start; i <= end; i++) {
    arr.push(i);
  }
  return arr;
}
 
const arr = rangeGenFunc(1, 10); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.sort(() => 0.5 - Math.random()); // [6, 8, 5, 10, 4, 3, 9, 2, 7, 1]
```
```
function* rangeGen(start = 1, end = 0) {
  for (let i = start; i <= end; i++) {
    yield i;
  }
}
let arr = [...rangeGen(1, 10)]; // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let shuffledArr = [];
const length = arr.length;
for (let i = 0; i < length; i++) {
  shuffledArr.push(...arr.splice(Math.floor(Math.random() * arr.length), 1));
}
 
console.log(shuffledArr); // [5, 4, 7, 10, 3, 6, 8, 2, 1, 9]
```

## 64.  Write a program to calculate the sum of all the values of an array
- Sum of the values of an array can calculated by iterating and adding all the values of the array
- reduce method of array can be used efficiently to calculate the sum with or without initial value
```
const sum = arr.reduce((acc, value) => acc + value, 0);

const sum = arr.reduce((acc, value) => acc + value);

const sum = 0;
for (let value of arr) {
  sum = sum + value;
}
```

## 65. Create an array of length n with all the values of it set to 10
- fill is a method on Array prototype which fills all the slots of array with the value given passed as the argument
```
const n = 5;
const arr = new Array(n);
arr.fill(10);
```
## 66. Write the code to remove the duplicates from the array
Set is a data structure which does not allow duplicate elements
```
const set = new Set(arr);
const distinctArr = [...set];
```
## 67.  Design a flat function which flattens an array to any depth
Flat function can be used to flatten the array by recursive call

```
function flat(arr) {
  const flatArr = [];
  arr.forEach((value) => {
    if (Array.isArray(value)) {
      flatArr.push(...flat(value));
    } else {
      flatArr.push(value);
    }
  });
  return flatArr;
}
```
## 68. Create a function named "average" which can calculate the average of an array and should be available to be called from any Array object.
The function added to Array prototype are accessible to all the objects of Array
```
Array.prototype.average = function () {
  let total = 0;
 
  for (let index in this) {
    total += this[index];
  }
  return total / this.length;
};
```
## 69. Write a code to make xmlHTTPRequest to get data from the server asynchronously
- XMLHttpRequest (XHR) objects are used to interact with server to retrieve data from a URL without having to do a full page refresh
- XHR requests can be initiated by creating the object and providing the arguments such as 'method', url etc
The success and failure of the request can be managed by callbacks
```
const xhr = new XMLHttpRequest();
xhr.open("GET", url);
xhr.onload = function () {
  console.log(this.response);
};
xhr.onerror = function () {
  console.log(this.statusText);
};
xhr.send();
```
## 70. Convert the xmlHTTPRequest to promise based function to get the data from the server asynchronously (fetch)
- The Promise can be used to wrap the XHR request and provide cleaner interface to user for AJAX requests
- Success and failure of the XHR request can be handled to resolve or reject the promise respectively
```
function fetchData(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = function () {
      try {
        if (this.status === 200) {
          resolve(this);
        } else {
          reject(this);
        }
      } catch (e) {
        reject(e);
      }
    };
    xhr.onerror = function () {
      reject(this);
    };
    xhr.send();
  });
}
// driver code
fetchData("https://reqbin.com/echo/get/json")
  .then((data) => {
    console.log(data);
  })
  .catch((err) => console.log(err));
```
## 71. Make a fetch request to retrieve and store JSON data from server
- Fetch API is provided by the browser which returns a promise
- Fetch takes url as the 1st argument and an object with request details as 2nd optional argument
- Response is a streamable object and hence we will have to invoke JSON / text method on it which returns promise which settles to the data
```
const response = fetch("https://reqbin.com/echo/get/json", {
  method: "GET", // *GET, POST, PUT, DELETE, etc
  headers: {
    "Content-Type": "application/json", // header
  },
});
// driver code
response
  .then((response) => {
    const responseData = response.json();
    responseData.then((data) => {
      console.log(data);
    });
  })
  .catch((err) => {
    console.log(err);
  });
```
## 72. Cancel a fetch request
- AbortController is an interface which can be used to abort a fetch request
- signal object of the AbortController object can be used as the part of the argument to fetch and abort on controller object can be used to stop the request
```
const controller = new AbortController();
var signal = controller.signal;
fetch(url, { signal })
  .then((response) => {
    console.log(response);
  })
  .catch((err) => {
    console.warn(err);
  });
controller.abort();
```
## 71. Write a code to resolve all the list of asynchronous executions of promises no matter if each execution succeeds or fails. Print the output of each
- Promise.allSettled is the method which helps to achieve the functionality which completes after all promises settle no matter of failures
- It receives array of promises as an argument to it
- Array of results will be the output after completion of all promises with status as 'fulfilled' or 'rejected'
```
const asyncArr = [async1, async2, async3];
const promiseArr = asyncArr.map((async) => async());
finalResolution = Promise.allSettled(promiseArr);
finalResolution
  .then((output) => {
    for (let data of output) {
      if (data.status === "fulfilled")
        console.log(data.status + ": " + data.value);
      else if (data.status === "rejected")
        console.log(data.status + ": " + data.reason);
    }
  })
  .catch((err) => {
    console.log(err);
  });
```
```
const asyncArr = [async1, async2, async3];
const promiseArr = asyncArr.map((async) => async());
(async function () {
  try {
    output = await Promise.allSettled(promiseArr);
    for (let data of output) {
      if (data.status === "fulfilled")
        console.log(data.status + ": " + data.value);
      else if (data.status === "rejected")
        console.log(data.status + ": " + data.reason);
    }
  } catch (err) {
    console.log(err);
  }
})();
```
## 73. Create a function which receives a function as argument and executes it after 2 seconds
```
function callbackExec(callback) {
  if (typeof callback === "function") {
    setTimeout(() => {
      callback();
      console.log("Callback is executed after 2 seconds");
    }, 2000);
  }
}
 
function displayHello() {
  console.log("Hello");
}
 
callbackExec(displayHello);
```
## 74.  Implement a function to get elements by tag name (document.getElementsByTagName() method)
- The getElementsByTagName method of Document interface returns an HTMLCollection of elements with the given tag name.
- For example, document.getElementsByTagName('div') returns a collection of all div elements in the document.
```
/**
 * @param {HTMLElement | null} tree
 * @return {Array}
 */
function getElementsByTagName(root, tagName) {
  if (!root) return [];
 
  let result = [];
 
  if (root.tagName.toLowerCase() === tagName.toLowerCase()) {
    result.push(root);
  }
 
  if (root.hasChildNodes()) {
    for (let child of root.children) {
      result = result.concat(getElementsByTagName(child, tagName));
    }
  }
 
  return result;
}
```
## 75. Implement a function to check if a given DOM tree has duplicate IDs
- In a given DOM tree, the id on each node has be unique
- Although HTML is very forgiving, but we should avoid duplicate identifiers
```
/**
 * @param {HTMLElement | null} tree
 * @return {Boolean}
 */
function hasDuplicateId(tree, idSet = new Set()) {
  if (!tree) return false;
 
  if (idSet.has(tree.id)) return true;
 
  tree.id && idSet.add(tree.id);
 
  if (tree.hasChildNodes()) {
    for (let child of tree.children) {
      const result = hasDuplicateId(child, idSet);
      if (result) return true;
    }
  }
 
  return false;
}
```

## 76. What will be the output of the following code?
1. 
```
var bar = true;
console.log(bar + 0);   
console.log(bar + "xyz");  
console.log(bar + true);  
console.log(bar + false);
```
The code above will output 1, "truexyz", 2, 1 as output. Here's a general guideline for the plus operator:

- Number + Number -> Addition
- Boolean + Number -> Addition
- Boolean + Boolean -> Addition
- Number + String -> Concatenation
- String + Boolean -> Concatenation
- String + String -> Concatenation

2. 
```
var z = 1, y = z = typeof y;
console.log(y);
```
The code above will print string "undefined" as output. According to associativity rule operator with the same precedence are processed based on their associativity property of operator. Here associativity of the assignment operator is Right to Left so first typeof y will evaluate first which is string "undefined" and assigned to z and then y would be assigned the value of z.

3. 
```
var foo = function bar() { return 12; };
typeof bar();
```
The output will be Reference Error. To fix the bug we can try to rewrite the code a little bit:

Sample 1
```
var bar = function() { return 12; };
typeof bar();
```
Sample 2
```
function bar() { return 12; };
typeof bar();
```
4. difference in both code
```
// Run-Time function declaration
  foo(); // Call foo function here, It will give an error
  var foo = function() {
    console.log("Hi I am inside Foo");
  };
```
```
// Parse-Time function declaration
bar(); // Call bar function here, It will not give an Error
function bar() {
  console.log("Hi I am inside Foo");
}
```
## 77.  Difference between Function, Method and Constructor calls in JavaScript.

functions : The simplest usages of function call:
```
function helloWorld(name) {
  return "hello world, " + name;
}
```
helloWorld("JS Geeks"); // "hello world JS Geeks"
Methods in JavaScript are nothing more than object properties that are functions.
```
var obj = {
  helloWorld : function() {
    return "hello world, " + this.name;
  },
  name: 'John Carter'
}
```
obj.helloWorld(); // // "hello world John Carter"
Notice how helloWorld refer to this properties of obj. Here it's clear or you might have already understood that this gets bound to obj. But the interesting point that we can copy a reference to the same function helloWorld in another object and get a difference answer. Let see:
```
var obj2 = {
  helloWorld : obj.helloWorld,
  name: 'John Doe'
}
obj2.helloWorld(); // "hello world John Doe"
```
You might be wonder what exactly happens in a method call here. Here we call the expression itself determine the binding of this this, The expression obj2.helloWorld() looks up the helloWorld property of obj and calls it with receiver object obj2.

The third use of functions is as constructors. Like function and method, constructors are defined with function.
```
function Employee(name, age) {
  this.name = name;
  this.age = age;
}

var emp1 = new Employee('John Doe', 28);
emp1.name; // "John Doe"
emp1.age; // 28
```
## 78. Detecting object using typeof operator
```
console.log(typeof {});           // object
console.log(typeof []);           // object
console.log(typeof new Array());  // object
console.log(typeof null);         // object 
console.log(typeof new RegExp()); // object
console.log(typeof new Date());   // object
```
## 79. Is a technique for converting function calls with N arguments into chains of N function calls with a single argument for each function call?

### Currying always returns another function with only one argument until all of the arguments have been applied. So, we just keep calling the returned function until we’ve exhausted all the arguments and the final value gets returned.

Example

```js
const add = (x, y) => x + y
add(2, 3) // => 5
```

And now, below is the same function in curried form.

```js
const add = x => y => x + y
```

Same code without arrow syntax

```js
const add = function(x) {
  return function(y) {
    return x + y
  }
}
```

Calling curried functions

So in order to use our curried function, we have to call it a bit differently …

add(2)(3) // returns 5

Focus on return

It might help to visualize it another way. We know that arrow functions work like this – let's pay particular attention to the return value.

```js
const f = someParam => returnValue
```

So our add function returns a function – we can use parentheses for added clarity.

```js
const add = x => y => x + y
```

More than two arrow functions can be sequenced, if necessary -

```js
const three = a => b => c => a + b + c

const four = a => b => c => d => a + b + c + d

three(1)(2)(3) // 6

four(1)(2)(3)(4) // 10
```

In other words add of some number returns a function

#### Further Reading

[stackoverflow.com/questions/32782922/what-do-multiple-arrow-functions-mean-in-javascript/32784025](https://stackoverflow.com/questions/32782922/what-do-multiple-arrow-functions-mean-in-javascript/32784025)

## 79. How is Node.js different different from Javascript?

__Ans:__ Node.js uses a library called [libuv](https://github.com/libuv/libuv), to bring an asynchronous event driven model to Javscript. It piggy backs on Chrome's Javascript Engine called V8 to enable the use of Javascript's call stack.
![](https://github.com/rohan-paul/Awesome-JavaScript-Interviews/raw/master/Node-Express/assets/2020-10-03-16-19-59.png)

What makes Node.js special is the different set of APIs. In browsers, you have a variety of DOM/Web APIs exposed that help you interact with UI and allow you to access the hardware to a limited extent. To compare, Node.js comes with many APIs suitable for backend development, e.g. the support for file systems, http requests, streams, child processes, etc. Browsers do offer some basic support for file systems or http requests, but those are usually limited due to security concerns.

Node.js is a good choice for applications that have to

 - **process a high volume of short messages requiring low latency. Such systems are called real-time applications (RTAs)** - Thanks to its specifications, Node.js will be a good choice for the real-time collaborative drawing/editing-type apps, where you can watch the document being modified live by someone else (such as Trello, Dropbox Paper or Google Docs). One of the most popular uses of RTAs are **live-chat and instant-messaging apps**.

 - **Video conference app that will work with specific hardware or VoIP**.

 - **nline gaming apps or e-commerce transaction software, where online data is of much importance**

- **Noe is quite a natural fit for exposing the data from object DBs (e.g. MongoDB)**. JSON stored data allow Node.js to function without the impedance mismatch and data conversion.

Node.js is very efficient with real-time applications: it facilitates handling multiple client requests, enables sharing and reusing packages of library code, and the data sync between the client and server happens very fast.

## 80. When Node.js should not be used?

- When have lot of synchronous code that needs to be run. Applications which require  number crunching or data analysis should not use Node.js. For Ex. Matrix Multiplication, Summation, Aggregation of large datasets. In such cases, applications which allow Multi Threading out of the box like Python, Java should be used.

- **CPU-heavy jobs** - Node.js is based on an event-driven, non-blocking I/O model, and uses only a single CPU core. CPU-heavy operations will just block incoming requests, rendering the biggest advantage of Node.js useless.
