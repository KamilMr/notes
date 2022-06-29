# JavaScript notes
In general some notes on javascript. If you find it usefull use it :)

## Let

"shadowing" when inner var shadows outer var.

```javascript
function f() {
  let x = 'outer';
  if (true) {
    let x = 'inner';
  }
  return x;
}
f();
```
This rule since 2015 apply to all code inside {}. For example, an outer scope can't access a variable defined inside a `while`. Any code contained in { curly braces } will have its own scope.

## Const

Variable can never be reassigned. `Const` doesn't stop us from mutating (changing) the value held by the variable. For example, we can mutate a const array by calling its push method. However, reassigning the array variable to hold a new array isn't allowed.

ECMAScript is another name for JavaScript. We can think of var and scope as mistake that was solved by introducing let and const in 2015.

### links

Set up prefer const  eslint rules in
[Eslint](https://eslint.org/docs/rules/prefer-const)

Set up no var rule in
[Eslint](https://eslint.org/docs/rules/no-var)

## loops

Unlike most other languages, JavaScript's arrays are a special kind of JavaScript object. typeof someArray is even 'object', not 'array'! And loop in 'sparse' array skips missing array elements.

Probably better use `for...of` loop. In sparse array it will loop over missing indexes. Remember firefox slow down when timestamp was index...!

The loop body executes once per character in the string. JavaScript doesn't have a dedicated character type, so the individual characters will show up as strings of length 1, like 'a'.

### links
[guard-for-in](https://eslint.org/docs/rules/guard-for-in)

## Accessors in object literals
Note the new get syntax in the next example. This kind of property is called a "getter".

```javascript
const user = {
  get userName() { return 'Amir'; }
};
user.userName;
```
The getter function can compute anything that we want; it doesn't have to return a constant value.
Setters, for writing to objects. Normally, writing to an object's key replaces the value at that key.
```javascript
const user = {
  realName: 'Amir',
  set userName(newName) { this.realName = newName; }
};
```

If we try to read the value of a setter, we'll get undefined. The object has no value at that key, even though there is a setter for that key.
But behind the scenes, our user.userName setter can store a history of what happened.

One more small detail. The get and set keywords are required when creating getters and setters. If an object's keys are regular functions, then they won't be called like a getter or setter would. We'll get the old JavaScript behavior from before getters and setters even existed.

## Computed properties
We can also create objects with computed keys. The [square brackets] can contain any expression, not just simple variables. For example, we can use string concatenation to build the key dynamically.

## isNAN
1985, authors intended NaN to be used in rare cases. For example, 0/0 has no value, so they said that it should return NaN.
- any arithmetic on undefined returns NaN.
- undefined - 1
- `['a', 'b', 'c'].elngth;`

Any operation on a NaN returns another NaN. Unfortunately, that means that NaNs will propagate through the system.

NaN is the only value in JavaScript that isn't equal to itself. Even when compared using ===, NaN is never equal to NaN.

JavaScript does make the mistake of returning NaN in many situations where it didn't have to, compare to other languages like Ruby or Python.

so use `isNaN` `isNaN(Infinity) === false`

isNaN also converts its argument to a number before checking.

## Basic object destructuring
Check destructuring with getters. `const {name: newKey} = {name: 'Ala', ...}`

## Shorthand properties
In modern JavaScript, we can shorten this significantly. When the object's key refers to a variable of the same name, we only have to specify that name once. Instead of {name: name}, we can just write {name}

We can't use this to refer to a variable that doesn't exist. As with the older syntax, that will cause an error.

## Tagged template literals
It looks like replaceWithHello`the numbers ${1} and ${1 + 1}`. (replaceWithHello is the function being used as a template literal tag.)

```
returnsItsArguments`1${2}3`;
RESULT:
{firstArg: ['1', '3'], secondArg: [2]}
```
The first argument contains all of the literal strings in the template literal (everything not in a ${...}). The second argument contains all of the interpolated values (everything inside a ${...}). Literal strings are passed as an array argument; interpolated values are passed as rest parameters.

There will always be one more literal string than there are interpolated values. If there are 7 interpolated values, there will be 8 literal strings. If necessary, the last literal string will be an empty string, '', but it will still be there.

[common tags](https://www.npmjs.com/package/common-tags)

```
const obj = {a: 1}
`an object: ${obj}`;
RESULT:
ReferenceError: Cannot access 'obj' before initialization
```
JavaScript isn't parsing this code in the way we think it should. It thinks that the object {a: 1} is being used as a tag function for the template literal.

## Places where destructuring is allowed
Destructuring works in function definitions. The destructuring rules are the same as when we destructure in a const or let statement.

```
let userName = undefined;
try {
  throw {name: 'Amir'};
} catch ({name}) {
  userName = name;
}
```

```
function rest(_, ...rest) {
  return rest;
}
rest(1, 2, 3);
```
```
function rest([, ...rest]) {
  return rest;
}
rest([1, 2, 3]);
```

## Shorthand methods

```
const user = {
  name() { return 'Amir'; }
};
user.name();
```
Like one above.

Shorthand methods have a this that refers to the parent object. We can access its properties by doing this.somePropertyName.

## Bind
this refers to the object that a function belongs to. The rules get complex, but here's a simple example with shorthand methods.

Sometimes, when writing JavaScript code, we'll get backed into a corner where we need to force a function to have a certain this. We can do exactly that with the bind method.

bind is a method on functions themselves, so we say someFunction.bind(someNewThis). That gives us a new version of the function, leaving the original function unchanged. When we call the new function, this will be bound to our specified value.

Example:
```
const user = {name: 'Amir'};
function userName() {
  return this.name;
}
const userNameBound = userName.bind(user);
userNameBound();
```
## Concat

 we can combine arrays properly with concat. (It stands for concatenate, which means "link together".) It creates a new array containing all of the elements from the old arrays.

 concat takes multiple arguments, so we can combine many arrays if needed:


concat can also be used to add single elements to the end of an array. If its argument isn't an array, it will be added as a single element.

concat builds and returns a new array. The original arrays aren't changed.


## New and fill

The fill method fills an array with a given value. Any existing values will be overwritten by that value.

```
const size = 1 + 2;
new Array(size).length;
```
If we ask for its elements, we'll get undefined.

## Extending classes
JavaScript classes can extend (inherit from) other classes: class MySubclass extends MySuperclass. The subclass will have all of the properties and methods of the superclass, plus any properties and methods that it defines itself.

The superclass and subclass can define their own separate constructors. That lets us centralize shared setup code in the superclass, avoiding duplication in its subclasses. The subclass' constructor calls the superclass' constructor with super(), passing whatever arguments the superclass' constructor requires.

Calling super is mandatory: if the subclass has a constructor, it has to call super at some point during the constructor. Otherwise, newing the subclass will cause an error. This rule holds even when the superclass doesn't actually define a constructor; we still have to call super!

```javascript
class Animal { }
class Cat extends Animal {
  constructor(name) {
    this.name = name;
  }
}
new Cat('Ms. Fluff').name;
RESULT:
```
ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor

We can use instanceof to check for whether an object is an instance of a given class.

`instanceof` understands subclasses: x instanceof Y is true when x is an instance of any subclass of Y.

```javascript
class Animal { }
class Cat extends Animal { }
const cat = new Cat();
cat instanceof Animal;
```
Subclasses can define properties or methods that already exist on the superclass. When that happens, the subclass' version "overrides", or replaces, the superclass' version.

Some languages have "multiple inheritance": they allow a class to inherit from multiple other classes at once. Python and C++ are examples. In JavaScript, there is no syntax for multiple inheritance, so we won't discuss it here.

When inheritance is appropriate. Object-oriented programming was very popular in the 1990s, sometimes promoted with an almost religious fervor. That fervor has died down now. We recommend viewing classes, and especially inheritance, as just another tool. Like any tool, it's important not to reach for them when they're not needed. Here's an example from React JS, a popular JavaScript UI library.

## Function name property

`function f()`
Functions declared like this have a name property.

`f.name` is `'f'`
Functions don't have to have names, though. If a function is created without a name, its name will be the empty string, ''. These are called "anonymous" functions.

The function remembers its original name, even if it's assigned to a different variable.

Anonymous functions only get a name if they're assigned directly to a variable. If we put the function in an array, for example, it won't get the array's name; instead, it will have no name.

Arrow function syntax doesn't give us any place to specify the function's name. As a result, arrow functions are always anonymous. However, like normal functions, they do get a name if they're assigned directly to a variable.

## flat and flatMap

By default, flat only flattens one level of arrays. Any arrays nested more deeply than one level are left unmodified.
The default depth is 1.

The depth can be Infinity, in which case flat will flatten all arrays no matter how deeply nested they are.

flat only flattens arrays. Non-array values are left unmodified. For example, we might have an array of objects, where the objects contain more arrays. In that case, both the objects and the arrays inside the objects are left unchanged.

When you start using flat, you'll often find that you combine it with map.

This kind of flat-map combination is common enough that there's a method that does both operations together: flatMap. It's identical to calling map followed by flat.

```javascript
>
[
  {numbers: [1, 2]},
  {numbers: [3, 4]},
].flatMap(obj => obj.numbers);
RESULT:
[1, 2, 3, 4]
```
Both flat and flatMap build and return a new array. The original array remains unmodified.

## general links
[Execute program](https://www.executeprogram.com/)
