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
## Sets

Sometimes, we want to know whether a value is in a list of other values. We can use an array.
The includes method loops through the entire array, checking each element. If there are 10,000 elements, it will loop up to 10,000 times.
`includes: 0(n)` so ex what if element is at the end of an Array?

JavaScript's Set data type is a better solution to this problem. A JavaScript set is a collection, it's ordered, and it contains only unique values. We'll look at each of those in order.

### First
First, sets are collections: they contain a bunch of JavaScript values. We can give a set an initial set of values in its constructor. Then we can add() more values later. We can ask a set whether it has() a given value.


### Second
JavaScript sets are ordered. If we examine the elements in the set, they'll always come back in the order that they were inserted.
To get the elements out of the set, we can use the values method. It returns an iterator, which we haven't covered yet. We can ignore the iterator for now by converting it into an array with Array.from().

```
const names = new Set(['Amir', 'Betty']);
Array.from(names.values());
```

Sets are mathematical objects studied in set theory, the modern form of which dates to the 1870s. Most programming languages, including JavaScript, provide a set type with operations that would've been familiar to the set theorist Georg Cantor (1845 - 1918).

JavaScript's sets are ordered, as we saw above. This isn't a case of JavaScript being weird in a way that's confusing. If anything, preserving order is desirable; it's one less uncertainty to track in our code.

In JavaScript, you can count on a set to remember the elements' insertion order.

### The third
Property of sets is: they contain only unique values. If we add a value that already exists in the set, nothing happens; the set is unchanged.

The set has: size property, can be deleted() clear()

The main power of sets isn't in converting them back into arrays; it's that calling has is very fast.

An array's includes method slows down as the array gets larger. But sets don't have that problem! A set's has() method is O(1): it always takes the same amount of time regardless of how many elements there are.


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

## Map
It returns a new array of the values returned from those function calls.

## Arrays are objects
Most programming languages have an array data type that's separate from the language's other data types. JavaScript is unusual here: in JavaScript, arrays are a special type of object. We can see this by looking at typeof someArray, which will return 'object', just like it does for regular objects.

```
const arr = ['a', 'b', 'c'];
arr['five'] = 5;
arr.length;
```
A couple more details about extra properties on arrays. First, looping with forEach will ignore extra array properties.


## Slice
Sometimes we want to access a subsection of an array. For that, we use the slice method. It takes an argument begin, which is the index to start from.

 It slices all elements from begin up to end, but not including end.

 We can slice beyond the end of the array. It gives the same result as slicing right up to the last element.

If our begin index is past the end of the array, we get an empty result.

With no arguments, slice will slice all elements of the array. This effectively copies the array. If we change the original, it won't affect the copy. Likewise, if we change the copy, it won't affect the original.

Slice is quite complex, but copying arrays is its most common use.

## Classes
JavaScript gained a new class syntax in 2015, making it more familiar to programmers who already know common object-oriented languages like Java, C#, Python, or Ruby.

If you already know an object-oriented language, this first lesson on classes might be very easy. But we'll soon turn to issues that are specific to JavaScript's version of classes.

Classes describe the shape of an object: what properties and methods (functions) it has. Class method definitions look like the shorthand method syntax that we already saw in literal objects: methodName() { ... }.

We construct an instance of a class with new: new MyClass(). The instance is an object with all of the properties and methods (functions) specified by the class.

The new keyword is required when instantiating classes: new Cat(...). If we try to create a Cat by calling the class like a function, we'll get an error.

JavaScript's native object system is prototype-based, which is unusual and therefore unfamiliar to a lot of programmers. We haven't mentioned that object system here precisely because it's so unusual. Prototypes are better viewed as an advanced topic, to be studied once the more "normal" parts of modern JavaScript are familiar. However, the class-based syntax in this lesson is only "syntactic sugar": it's a new syntax layered over the older prototype-based object system.

When possible, we recommend using classes rather than prototypes because they're more widely understood. Occasionally, you'll be forced to dig down into the prototype system, especially when dealing with older JavaScript code or very unusual kinds of objects.

## general links
[Execute program](https://www.executeprogram.com/)
