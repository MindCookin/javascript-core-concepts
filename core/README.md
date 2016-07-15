# CORE

### Interpreter

Javascript is an interpreted language. There is a [Javascript engine](https://en.wikipedia.org/wiki/JavaScript_engine) that act as an interpreter, it is common in every web browser.

Javascript is process through a [REPL](https://repl.it/languages). To understand it, let's say there is a loop passing iteratively through the code. This loop will execute our code. It will wait until the code finishes execution to execute the next loop.

### Asynchrony

Javascript Engines are _single thread_. So any execution blocking task will block the full application execution. This is the same for NodeJS and browsers, and it may also block rendering, interaction and any action in browsers, and may also block requests in NodeJS.

Javascript engine is certainly synchronous. More, its REPL, single thread and interpreter based nature makes it a heavy CPU process for complex tasks.

Here comes the importance of **asynchrony**. This performance blocking behaviours make necessary the use of special techniques to handle them: Event based applications can delay the execution of code, callbacks encapsulate functionality, and promises add some sugar to the mix.

### Global scope

Code executes in a global scope. Every JS code is executed in the same unique global scope. This is important to understand, because we can target this global scope (
voluntarily or involuntarily) from everywhere.

This makes specially useful the use of modularization techniques, like:
* [Immediately Invocated Functions](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression) to create an encapsulated scope
```
(function(){ /* encapsulated scope*/ })()
```
* Creating an APP variable that will receive all our APP methods and objects
```
var APP = {} || APP;
(function(app){ /* encapsulated scope with access to global APP*/ })(APP)
```
* Use [Asynchronous Module Definition](https://es.wikipedia.org/wiki/Asynchronous_module_definition)
```
define(['foo'], function (Foo) { /* AMD scope */ })
```
* Use [CommonJS](https://en.wikipedia.org/wiki/CommonJS)
```
// module.js
function encapsulatedFunction() {}
exports.externalAccessedFunction = encapsulatedFunction;
```
* [ES6 modules](http://www.2ality.com/2014/09/es6-modules-final.html)
```
// module.js
export function square(x) {
       return x * x;
   }
```

### Hoisting

While interpreting the code syntax the Javascript engine will put all our variables, and named functions at the top before executing a scope block. This is useful to prevent undeclared variables, but it may bring up some errors.

```
(function scopeBlock (){

  if (aFunction && aVar) {
    // aFunction and aVar exist, even though they are defined lately
  } else {
    // this will never happen
  }

  function aFunction () {}
  var aVar = 'I am a variable';

})()
```

### Global variable linking

If an undefined variable is assigned, and no "var" is specified, then the variable is linked to the global object. This could be prevented with 'use script'.

```
(function scopeBlock (){
  myVar = 'hola' // this var is created into the global object
  var myOtherVar = 'aloh' // this var is linked to the function block, as you may expect.
})()

console.log(myVar) // 'hola'
console.log(myOtherVar) // undefined
```

### Auto completed statements

The Javascript interpreter will always check your syntax and, in some cases, when the syntaxis is not strict or explicit, it will complete the sentence "automatically" adding semicolons where they are needed. Semicolons mean "end of statement execution", so your code could break.

Here are some examples:
```
function myFunction(a) {
    var
    power = 10;  
    return
    a * power;
}
```
Will execute:
```
function myFunction(a) {
    var power = 10;  
    return;
}
```
While you may expect:
```
function myFunction(a) {
    var power = 10;  
    return a * power;
}
```

See [common javascript mistakes](http://www.w3schools.com/js/js_mistakes.asp) in w3schools.

This is the reason [you should always complete an statement with a semicolon in JS](http://mislav.net/2010/05/semicolons/), and [you should always write in K&R style](http://stackoverflow.com/questions/12233999/is-it-true-that-i-should-use-kr-styling-when-writing-javascript), *unless you know what you are doing*
