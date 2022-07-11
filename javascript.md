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

## Includes
We can check for whether an array includes a given element.

## Slice with negative arguments
We can slice from the end of the array by using negative indexes. You can think of a negative index -2 as array.length - 2. Or you can think of it as "two away from the end".

```javascript
>
[10, 20].slice(-2);
RESULT:
[10, 20]
```
With negative indexes, we can also slice before the beginning of the array. The result will only include elements in the original array. It won't invent additional elements to satisfy our out-of-bounds index.

```javascript
[10, 20].slice(-100);
RESULT:
[10, 20]
```

Both begin and end can be negative. The end element isn't included in the slice.

## Some and every
The some method decides whether a function is true of any element in an array. For example: "are any of these numbers two?" Or "are any of these strings empty?"

some always returns false for an empty array. This might seem strange, but it makes some sense.

"Are some of these people named Amir?" If we ask that about a person named Amir, the answer is yes. If we ask about a person named Betty, the answer is no. If we ask it about no people at all, the answer is no; there's no Amir.

every is true if our function is true for every element in the array.

every always returns true for an empty array. One way to remember this is that every's behavior for empty lists is the opposite of some's behavior.

- `[].every(f)` is true, no matter what f is.
- `[].some(f)` is false, no matter what f is.

`!['a', 'bc', 'def'].some(string => string.length === 0);`
example to check some object

## Empty slots
When we use new Array, the array appears to be full of undefined.

However, the slot in this array is actually empty. Empty means that there's nothing in the slot, not even an undefined. But JavaScript has no empty value, so it returns undefined instead.


We can use the in operator to see the empty array slot. (For arrays, x in a asks whether the array has something in index x.)

```javascript
0 in [undefined];
RESULT: true
```
but
```javascript
0 in new Array(1);
RESULT:
false
```

```javascript
const array = [];
array[2] = 1;
array.length;
RESULT: 3
```
The 0 and 1 slots in this array remain empty. They'll return undefined when accessed.

fill will fill in those empty slots. That's why it's so often paired with new Array(). This is a good way to avoid arrays with empty slots.

Empty slots can cause confusing bugs. For example, the `forEach ` and `map` method will skip over empty slots. It won't even call our provided function for those slots.

However, undefined is an ordinary JavaScript value. Array methods work normally with arrays containing undefined.


`reduce`, `filter`, and some other methods also skip empty slots. Try to avoid arrays with empty slots:
- Always using fill after calling new Array(someSize).
- Not writing to indexes past the end of an array.

## Index of
We can ask an array for the index of a particular value. (Indexes start at 0, as usual.)

If the value occurs multiple times in the array, we'll get the index of the first occurrence.

If we ask for an element that isn't in the array, we get -1.

It's important to check your indexOf calls for that -1 return value! Otherwise you can introduce subtle bugs.

## Reduce

We're "reducing" our array of many numbers to a single number.

We pass two arguments to reduce. The first is a function that adds a new number to our running sum. The second argument is 0, the initial value for the sum.

function is called once for each number. Each time, it adds the number to the running sum. We can see this by instrumenting our function to store all of the sums. (The verb "instrument" means "attach measurement instruments to". It's a great way to learn how unfamiliar systems work!)

We can make our reduce call shorter by omitting the second argument. Then array element 0 will be used as the sum. For many uses of reduce, including computing sums, that's OK.


With no second argument, our function is never called for array element 0. To sum [1, 20, 300], this happens:

- sum is set to element 0 of the array, which is 1.
- callback(1, 20) is called, returning 21 as the new sum.
- callback(21, 300) is called, returning 321 as the new sum.
- There are no more array elements, so reduce returns 321.

What happens if we try to reduce an empty array of numbers? If we provide an initial value as the second argument to reduce, then reduce can simply return that number. If the initial value is 0, we'll get 0 out.


When empty array and no second argument
```javascript
[].reduce(
  (sum, current) => sum + current,
);
RESULT:
TypeError: Reduce of empty array with no initial value
```
When you're using reduce, it's important to think about what happens when the array is empty. Otherwise, you may find yourself surprised if you see the error shown above.

Reduce is a very abstract method: it can do many different things. The ways to use abstract methods aren't always obvious at first. But once you're comfortable with them, you see applications everywhere.

acc stands for "accumulator", because it's accumulating the result.

Don't be afraid to use reduce in simple cases. But sometimes you'll struggle to read or write a complex reduce. In those cases, it's best to give up on the reduce and use a loop. Six easy lines of loop code are better than one confusing reduce line!

## Filter
In procedural languages, we often make decisions inside loops. JavaScript is a procedural language.

filter calls a function on each element in an array. If the function returns true, then filter keeps that element. Otherwise, it discards the element.

filter builds a new array. The original array isn't changed.

## Reduece right
reduce processes array items from left to right. There's also a less-common variant called reduceRight. With reduceRight, the array is processed from right to left.

However, reduceRight does matter when the order of operations matters.

##Shift
shift and unshift do the same, but for the beginning of the array. shift removes the first element of the array and returns it.

unshift adds an element to the beginning of an array.

unshift returns the array's length, including the newly-added element. This matches push, which also returns the array's length.

shift and unshift have somewhat confusing names. Here's one way to remember them. shift "shifts" all of the elements down by one. Index 2 becomes index 1; index 1 becomes index 0; etc. unshift does the opposite.

Like pop and push, shift and unshift change the array itself.

## Find index
The indexOf method gives us the index of an element.

Sometimes, we don't know the complete value of the element that we want. For example, maybe we want to find the first non-empty string. For that, we can use findIndex.

```javascript
['', 'a'].findIndex(
  string => string.length !== 0
);
```
It's OK if multiple elements match our provided function. findIndex will find the first matching element.

The callback function passed to findIndex gets three arguments. Usually you only need the first, which is the current array element. But sometimes the others are useful too. The second argument is the element's index in the array.

The whole array is passed to our callback as its third argument. This is rarely needed, but it's there just in case.

If our function doesn't match any elements, findIndex returns -1. This is like indexOf, which returns -1 when nothing is found. As with indexOf, this can be a source of bugs. Remember to check for -1!

## Short

The sort method puts elements in order. It changes the array that it's called on. In the example below, the array will be sorted alphabetically.

Often, we want a sorted copy of an array without changing the original. We can use slice() to copy the array, then sort the copy.

JavaScript often converts values in surprising ways. For example, 10 > 3 is true, but '10' < '3' is also true. This is because strings are compared character by character. The comparison ends as soon as two characters differ. '1' < '3', so '10' < '3'. The '0' in '10' is never even examined.

sort converts the array's elements to strings, then compares them. Because it compares strings, it inherits the comparison problem above.

This makes JavaScript's sort unsafe for numbers and most other data. Most other programming languages don't have this problem, so be careful!

```javascript
[3, 10].sort();
RESULT:
[10, 3]
```
There's a way to fix this problem. We can write our own comparison function, then give it to sort. Our function takes two array elements (a, b) as arguments and returns:

- If a == b, then a - b == 0.
- If a > b, then a - b > 0.
- If a < b, then a - b < 0.

If you can remember the a - b part, you can probably remember this trick. However, you'll probably also forget the order of the a and b. Sometimes, you'll write (a, b) => b - a. It's fine; everyone forgets the order. Just check it in the console when the time comes.

## general links
[Execute program](https://www.executeprogram.com/)
