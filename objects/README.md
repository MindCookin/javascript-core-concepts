# Objects

We can understand Javascript as an object based language.

### Objects are dynamic

Creating an object is as easy as writing `{}`. An object is, roughly, a key-value structure where *keys* can be **names**, **strings** or **numbers** and *values* can be any valid structure.
```
var object = {}
var object_built_with_name = {name: 'this is a name'}
var object_built_with_string = {'name': 'this is a string'}
var object_built_with_number = {0: 'this is a number'}

object.name // undefined
object_built_with_name.name // 'this is a name'
object_built_with_string.name // 'this is a string'
object_built_with_number.name // 'this is a number'
```

> We can think of arrays as a particular kind of object (there is not such a "array" type) that only contain integer keys. The Array's prototype provide also some special methods like `push` or `pop`.

You can also create an object with [the "new" keyword](http://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript). For example `var new_object = new Object();` or `var new_object = new Object;`. This last sentence may sound weird to non javascript developers. See [binding "this" keyword]() #TODO

We may augment the object with new properties/methods dynamically. For non "name" keys, they should be wrapped into brackets. If the property already exists, it will be updated

```
var object = {}
object.name = 'dynamically created property'
object['string ^name*$'] = 'string properties can have just any character in it.'
object[0] = 'number keys should be wrapped into brackets also'
object[0] = 'now I override old property with this text'
```

Updating has also [some peculiarities]() that come with prototype inheritance. #TODO

### (Nearly) everything is an object.

Well, this is really not true. In JavaScript there are 5 primitive types: `undefined`, `null`, `boolean`, `string` and `number` that definitely are not objects. But they act as so [in certain circumstances](https://javascriptweblog.wordpress.com/2010/09/27/the-secret-life-of-javascript-primitives/).

```
var aBoolean = true;

// booleans have methods
aBoolean.toLocaleString() // "true"

// you can add properties dynamically to booleans, but they won't be saved
aBoolean.newMethod = function() {console.log("newMethod")}

// but...
aBoolean.newMethod // undefined
```

> As Mr Crockford says: _"Numbers, strings and booleans are object-like in that they have methods [and properties], but they are immutable. Objects in Javascript are mutable keyed collections."_

In a nutshell, you can create a "boolean object" that "inherits" from "boolean", and so act as an object that have boolean properties and the flexibility of objects.

```
var aBoolean = new Boolean(true);

// "booleanic" objects have methods
aBoolean.toLocaleString() // "true"

// and dynamic properties/methods
aBoolean.newMethod = function() {console.log("newMethod")}
aBoolean.newMethod // "newMethod"

aBoolean.newProperty = "new property";
aBoolean.newProperty // "new property"
```

### Loose typing

Javascript does not cast. The lineage of an object is irrelevant. What matters is _what it can do_, not who is its parent neither whats its lineage.

This come with [some advantages](https://dzone.com/articles/understanding-loose-typing-jav) (you don't need to know which type may contain a variable, particularly useful when receiving external data) but it comes with [some disadvantages](http://stackoverflow.com/questions/964910/is-javascript-an-untyped-language), as the Javascript Virtual Machine will always have to analyze the data injected to deduct the type and it affects perf.

```
1 + 1 // 2
'1' + 1 // 11
null + '1' // null1
```

### Prototype

As a _loosely typed_ language, the linage of an object does not matter, what matters is what it can do.

JavaScript is a _prototypal language_, this means that object inherit directly from other objects through their prototype.

###### accessing prototype
Prototype chain. Linking retrieval. **Delegation**

###### shadowing

###### enumeration
`for in` will reveal all the object's properties

To prevent this, if you know the properties you may use `for + array of properties` instead

###### `delete`
Will never touch prototype(test), and will reveal elements hidden in the prototype chain. In arrays, use slice.

###### reflection
hasOwnProperty

### Inheritance techniques

> _"Javascript is conflicted about its prototypal nature. Unnecessary level of indirection such that objects are produced by constructor functions (not useful constructor method)"_

Much of the complexity of class hierarchies is motivated by the constraints of static type checking. Javascript is free of those constraints.

In classical languages, inheritance is the only way for code reuse. Javascript has more and better options.

###### Pseudoclassical
No privacy, no "super" methods, problems if you forget to initialize without "new" (this bounded to global var)

###### Prototypal
Focus in objects, not classes: A new object can inherit the properties of an old object. _Differential inheritance_ Object.create from ECMASCRIPT 5.1. _Again, no privacy_

###### Functional
No need for "new" prefix. Flexibility. Durable. Better encapsulation. Super methods.
  * It creates a new object
  * It optionally defines private instance variables and methods
  * It augments that new object with methods
  * It returns that new object

###### Parts
A constructor can be made from a set of parts. Great benefit over classical lineage, we can focus on the contents not on the inheritance. Thanks to loose typing.
