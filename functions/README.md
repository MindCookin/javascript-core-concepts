# Functions

> _"The best thing about Javascript is its implementation of functions. It got almost everything right. But, as you ahould expect with Javascript, it didn't get everything right."_ Douglas Crockford

### function are objects

Functions in Javascript are just like any other JS Object. They inherit from `Function.prototype` (who also inherit from `Object.prototype`).

Function literals let you create functions. You can add a name, but you can also leave the function anonymous. You may also bind the function to a variable.

Anonymous functions are commonly used for specific functionality (i.e. callbacks) but they do not have a "name" property. So they are harder to debug.

```
function namedFunction() {....} // named function
function () {....} // anonymous function
var variableLinkedFunction = function () {....} // variable linked function
```

### invocation and `this` keyword

When executing a function _as is_ (Function Invocation Pattern) `this` keyword is bind to the global object.

```
function aFunction () {
  console.log(this)
}

aFunction() // 'Window' or 'global'
```

When the function is stored as an object's property, we will execute the function _as a method_ (Method Invocation Pattern). Then `this` is bound to the object at invocation time

```
var obj = {
  aMethod: function aFunction () {
    console.log(this)
  }
};

obj.aMethod() // Object
```

When a function is invoked with the `new` prefix, then a new object is created (with a hidden link to the function's prototype) and `this` will be bound to that new object. This is the Constructor Invocation Pattern

```
var AConstructor = function () {
  console.log(this);
};

new AConstructor() // AConstructor
```

> There are some drawbacks with the Constructor Invocation Pattern #TODO

When a function is invoked with `apply` or `call`, you can choose the `this` binding at execution time.

```
aFunction.apply(null) // Window
aFunction.apply({}) // Objects
aFunction.apply(document) // #document
```

More examples and explanation [on this subject](http://blog.amatiasq.com/2012/01/javascript-conceptos-basicos-this-call-y-apply/)

### binding `this`

You may create a function instance binding `this` dynamically at execution time. This is particularly useful with callback functions. It is important to notice that a new instance of the function will be created when executing bind.

```
aFunction() // Window

var linkedFunction = aFunction.bind(document);
linkedFunction() // #document
```

### function scope

Instead of common "block scope" languages like C, Javascript has **"function scope"**.

This means that scope is contained inside a function, and curly brace blocks do not really mean encapsulation block. Better with an example:

```
// C like scope (FAKE JAVASCRIPT)

function() { // scope 1

  var foo = 'foo';

  if (foo) { // scope 2

    var baz = 'baz' // will only be seen inside the conditional block

  } // end scope 2

  console.log(foo) // 'foo'
  console.log(baz) // undefined

} // end scope 1
```

```
// TRUE JAVASCRIPT scope

function() { // scope 1

  var foo = 'foo';

  if (foo) { // do not change scope!

    var baz = 'baz' // baz var is created in function scope
  }

  console.log(foo) // 'foo'
  console.log(baz) // 'baz'

} // end scope 1
```

> With ES6 _let_ key word you can encapsulate variables in block scopes.

### closures
Understanding function scopes bring us to closures. Closures are the capability of sharing parent scope between functions.

It is easier to see with an example:
```
function outerFunction() {

  var outerVar = 'outer';

  function innerFunction () {
    var innerVar = 'inner';

    console.log(outerVar) // 'outer'
    console.log(innerVar) // 'inner'
  }

  console.log(outerVar) // 'outer'
  console.log(innerVar) // undefined
}
```

### passing by reference or value
Arguments are always passed by reference, never copied. With the exception of primitive types: `undefined`, `null`, `boolean`, `string` and `number`.

```
function double (a) {
  a = a * 2;
  console.log(a) // 4
}

var out = 2;
double(out);

console.log(out); // 2
```

```
function double (a) {
  a.num = a.num * 2;
  console.log(a.num) // 4
}

var out = { num: 2};
double(out);

console.log(out.num); // 4
```

### arguments
Arguments are optional. You can execute functions with full argument list or just part of them.

```
function optionalArguments (a, b, c) {
  console.log(a, b, c);
}

optionalArguments(1, 2, 3) // 1, 2, 3
optionalArguments(1, 2) // 1, 2, undefined
optionalArguments() // undefined, undefined, undefined

optionalArguments(1, 2, 3, 4, 5, 6, 7, 8) // 1, 2, 3
```

You can also capture the argument list that a function have been called with, [thanks to the arguments object](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/Funciones/arguments).

```
function unknownArguments () {
  console.log(arguments);
}

unknownArguments(1, 2, 3) // [1,2,3]
```

### object specifiers
When a function is given a lot of parameters, is better to constrain them in a single object. This also prevent from mistakes in the parameters order.

```
function constrainedArguments (options) {
  console.log(options.a, options.b, options.c);
}

constrainedArguments({a: 1, b: 2, c: 3}) // 1, 2, 3
```
