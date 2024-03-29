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

## Anonymous and inline classes

```javascript
class Cat { }
Cat.name;
RESULT:
'Cat'
```

```javascript
const cat = new (
  class {
    speak() {
      return 'yaong';
    }
  }
)();
cat.speak();
RESULT:
'yaong'
```
When we try to inspect the name of an anonymous class, we'll get the empty string ('').

If we immediately assign the class to a variable, that variable's name will become the class' name. This is the same behavior that we saw for anonymous functions.

```javascript
const Cat = class { };
Cat.name;
RESULT:
'Cat'
```

```javascript
const classes = [class { }];
classes[0].name;
RESULT:
''
```

Craze example:
```javascript
onst classes = [];
classes.push(class { });
classes.push(class extends classes[0] { });
const ParentClass = classes[0];
const ChildClass = classes[1];
new ChildClass() instanceof ParentClass;
RESULT: true
```
We've seen classes and functions behave similarly with regards to the name property. Here's why they're so similar:

```javascript
typeof (class Cat { });
RESULT: 'function'
```
Internally, JavaScript classes are just functions. The implications of that are complex and, to be honest about it, pretty confusing. But we just saw one implication: when we assign an anonymous class directly to a variable, that variable's name becomes the class' name. That's not because classes and functions follow the same rule; it's because classes ARE functions!

Classes can be anonymous (have no name), and they can be inline (the class definition itself is used as an expression). Both of those are uncommon. You certainly won't use them in most of the modules that you write. But they are used in real systems, so you'll encounter them eventually!

## Modern JavaScript: JSON stringify and parse

In the past, we had to use third-party libraries to read and write JSON. Fortunately, modern versions of JavaScript include built-in JSON support.

The stringify method turns an object into a JSON string. By default, it will pack the JSON tightly. For example, there's no space after the : in the stringified object above. The parse method turns a JSON string back into an object.

If we try to parse a string that isn't valid JSON, we'll get an error.

JSON stands for "JavaScript object notation". However, not all JavaScript object syntax is valid JSON.

[Details|https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON]

The full details of JSON's syntax are out of scope for this course, but we'll examine one quick example to make the point. JavaScript object keys don't have to be quoted, but JSON keys do require quotes. If we try to parse a JSON string with unquoted object keys, we'll get an error.

The JSON methods will parse and stringify any JSON-compatible value, not just objects. They work on arrays, strings, numbers, etc.

```javascript
JSON.parse(JSON.stringify([true, null]));
RESULT: [true, null]
```
undefined is an important special case because it's not allowed in JSON. When we call stringify, any undefineds in the original object will be turned into nulls. If we then parse the resulting JSON, we'll get a null out. The JSON contains no hints that there ever was an undefined.

JSON can't represent circular objects (objects that reference themselves). Here's an example of a circular object.

Sometimes, we'll want an object to specify how it should be serialized to JSON. We can do that by putting a function in its toJSON property. JSON.stringify will call that function and use its result rather than the original object.

```javascript
const user = {
  name: 'Amir',
  toJSON: () => 'This is Amir!'
};
JSON.parse(JSON.stringify(user));
RESULT: 'This is Amir!'
```
The toJSON function isn't responsible for actually converting to JSON; stringify will still do that part. Instead, toJSON returns a new JavaScript object to be serialized in place of the original.

## Modern JavaScript: String keyed methods
However, if we put quotes around the method's name, then it can contain spaces and even punctuation!

If a method name contains spaces or punctuation, then we can't call it with the usual someObject.methodName syntax. We'll have to use someObject['methodName'].

```javascript
const user = {
  'name of the ~user~'() { return 'Betty'; }
};
user['name of the ~user~']();
RESULT: 'Betty'
```
This method definition syntax is called "string keyed methods" because we're using the normal JavaScript string syntax to define the method's name (its key in the object).

Modern JavaScript has good Unicode support, so ordinary methods work with non-English characters as well. For example, we can name our method "名前", the Japanese word for "name".

However, we can't use normal syntax to name the method 名前。. The "。" character is a Japanese period, which is punctuation, and punctuation isn't allowed in JavaScript identifiers. Including that character will result in an error.

String keyed methods also work in class definitions. This is a recurring theme: syntax that works in object literal methods will generally work inside class definitions as well.

## Modern JavaScript: Set operations

Sets in every programming language provide a range of useful operations that are missing in JavaScript. Normally, sets have at least the three most common operations: union, intersection, and difference. It's OK if those aren't familiar; in this lesson, we'll define them and see how to implement them in JavaScript.

First: we sometimes want to find a set union, which is every element that's in either set1 or set2. The closest array equivalent is concat.

Set union is the same thing, but it respects the constraint that a set only contains unique values. If the concat operation above were a set union, we'd expect a result of [1, 2, 3, 4].

```javascript
const set1 = new Set([1, 2, 3]);
const set2 = new Set([2, 3, 4]);
const unionSet = new Set([...set1, ...set2]);
[unionSet.has(1), unionSet.has(4)];
```
Second: we sometimes want to find a set intersection, which is every element that's in both set1 and set2. With arrays, we can use filter to do that. (filter takes a function f, calls it on every array element, and returns an array with all of the elements where f(element) was true.)

"set difference" means "all items that are in the first set, but aren't in the second set."

Set union is different from array concatenation because it results in a set, which has no duplicates. Set intersection and difference both do the same things as the array versions. But they're better than our array versions because they're much faster. (Using the technical terminology: all of the set operations implemented here are O(n), but our array equivalents are O(n^2).)

## Modern JavaScript: Accessor properties on classes

We can also use accessors in classes. As with object literals, a getter's function will be called when we access the property.

```javascript
class User {
  constructor(name) {
    this.actualName = name;
  }

  get name() {
    return `${this.actualName} the user`;
  }
}
new User('Betty').name;

class User {
  constructor(name) {
    this.actualName = name;
  }

  set name(newName) {
    this.actualName = newName;
  }
}
const user = new User('Amir');
user.name = 'Betty';
user.actualName;
```

When we extend a class, the child inherits any getters and setters from the parent.

## Modern JavaScript: Spread
There, ... means "include that array's elements into this array".

We can spread multiple arrays in a single expression. The elements will occur in the order they were specified.

Order matters when setting object keys. When defining an object literal, the last value assigned to a key wins:

Order of object keys also matters with spread. The last instance of a key wins, even if it comes from a spread.

## Modern JavaScript: Default parameters
If we call a JavaScript function with an argument missing, the corresponding parameter will get the value undefined.

Modern JavaScript has native support for default function arguments, so we don't need to do that trick any more. Defaults are declared using an = inside the function parameter list.

Defaults are evaluated when the function is called, not when it's defined. They can even reference other arguments.

Some other programming languages handle defaults differently. Python is a notable example: in Python, the default value is evaluated only once, when the function is defined. The above example would be illegal in Python because the value of x can't be known when the function is defined. If you know Python, be very careful because this difference can lead you to introduce subtle bugs!

Default parameters also work in methods on classes.

Any value can be used as a default. For example, we can use an object as a default value.

When we say "any value", we mean it! For example, we can even use an inline anonymous class as the default value.

We can use destructuring together with defaults. The default can even refer to a value that we get by destructuring another argument.

```javascript
addObjects({x: 1});
RESULT: 2
```

## Modern JavaScript: Class scoping

We usually define classes at the top level of a module. However, classes follow the same scoping rules as regular variables. We can define them inside a function, or even inside a conditional.

Just to be clear: there are very few cases where a class should be defined in a function. There are even fewer (and maybe none) where a class should be defined inside a conditional. But JavaScript allows us to do these things!

When classes are defined dynamically, like inside a function, the class definition itself can see all of the variables that are currently in scope. For example, a class defined inside a function can reference the function's arguments.

we can't define a class inside another class. That will cause an error, whether we use the class or not.

## Modern JavaScript: Static methods

It's also possible to define methods on classes themselves, which are called "static methods".

```javascript
>
class User {
  constructor(name) {
    this.name = name;
  }

  static defaultNames() {
    return ['Amir', 'Betty', 'Cindy'];
  }
}
```

The difference here is that the method exists on the User variable itself, rather than on an object created with const user = new User();

Sometimes, we'll want multiple ways to create instances of a class. For example, we might want to have a separate function for creating administrator users (as opposed to regular, non-admin users). A JavaScript class can only have one constructor, so we can't do it that way. But we can use static methods as a substitute.

```javascript
class User {
  constructor(name, isAdmin=false) {
    this.name = name;
    this.isAdmin = isAdmin;
  }

  static newAdmin(name) {
    return new User(name, true);
  }
}

[new User('Amir').isAdmin, User.newAdmin('Betty').isAdmin];
RESULT:
[false, true]
```
Accessors (getters and setters) can also be static. That means that the getter or setter is accessible on the class itself, not on instances.

If we try to access a static accessor on an instance, it won't be there. But we won't get an error; we'll just get undefined. That's because accessing an object property that doesn't exist always gives us undefined, regardless of the object.

Inside of a static method or accessor, this refers to the class itself.

The name "static" doesn't mean that these methods and properties always return the same value. They can return any value that we like, even if it changes over time. For example, we can define a static setter and getter pair.

## Modern JavaScript: Property order
In many languages, properties in objects don't have a guaranteed order. (Some languages call their object-like data structures "hashes" or "dictionaries", but for our purposes here these are all the same thing.)

Consistent ordering is nice; it's one less thing to think about. Fortunately, modern versions of JavaScript guarantee object key ordering!

An object's keys will be in the order that they were defined in the object.

If we add more keys to the object after it exists, the ordering is preserved there too.

Object key order is even preserved when we deserialize JSON with JSON.parse.

JSON.stringify preserves that order as well, so round-tripping an object through JSON won't change its keys' order.

There's one exception to the property order rule. It comes from an unusual part of JavaScript objects: they can have numbers as keys, and we can mix number keys with strings keys in the same object.

When an object has number keys, (1) they always come first in the key list, (2) they're always sorted numerically, and (3) they're always converted into strings (1 becomes '1'). The string keys come next, in the order that they were inserted into the object, as we've already seen in this lesson.


```javascript
Object.keys({2: 'two', 1: 'one'});
RESULT:
['1', '2']
>
Object.keys({b: 'b', 1: 'one', a: 'a'});
RESULT:
['1', 'b', 'a']
```
This number-vs-string issue is an unfortunate complication. However, the good news is that objects with mixed number and string keys are uncommon, so this doesn't come up much. For normal objects with string keys, you can trust that they'll stay in insertion order.

## Modern JavaScript: Customizing JSON serialization

JSON.stringify allows us to customize its output by passing a second argument, replacer. If we give it an array of strings, then only those keys will be included in the resulting object.

```javascript
JSON.parse(
  JSON.stringify(
    {age: 36, city: 'Paris', name: 'Amir'},
    ['name', 'city']
  )
);
RESULT: {city: 'Paris', name: 'Amir'}
```

The replacer can also be a callback function taking two arguments, key and value. During stringification, our replacer is called with the key and value for each object, array, string, etc. We can replace any value by simply returning the new value that should take its place.

```javascript
SON.stringify(
  {age: 36, name: 'Amir', cat: {name: 'Ms. Fluff'}},
  (key, value) => {
    console.log(`Key: ${JSON.stringify(key)}, value: ${JSON.stringify(value)}`);
    return value;
  }
);
console output
  17 ms  Key: "", value: {"age":36,"name":"Amir","cat":{"name":"Ms. Fluff"}}
  18 ms  Key: "age", value: 36
  19 ms  Key: "name", value: "Amir"
  20 ms  Key: "cat", value: {"name":"Ms. Fluff"}
  21 ms  Key: "name", value: "Ms. Fluff"
```

The first replacer call gets the entire object. The key is "" because we're not inside of an object yet. Then we see separate calls for the age, name, and cat keys. Finally, stringify descends into the cat object, so we get a final call for its name key. We didn't replace any data in this example, but we could've replaced the data in any of these steps, from the entire object down to a single deeply nested property.

At each step, our replacer function can do three things:

  - Return the value argument unmodified, which won't change anything.
  - Return some other value, which will replace the original value in the stringified JSON.
  - Return undefined, which will remove the key from the stringified JSON.

There are some more details of the replacer function, but we won't cover them here. If you need to write a JSON.stringify replacer, you should definitely have the [documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)open anyway! The important thing to know is that it exists, and that the replacer function gets a chance to modify every part of the object as it's stringified. That's enough to know when this tool is appropriate.

Finally, JSON.parse has a similar feature called reviver. Conceptually, it's the opposite of JSON.stringify's replacer argument. As the JSON is decoded, the reviver can replace any value with a new value.

```javascript
/* Note that the "reviver" function here replaces all property values in
 * the object! */
JSON.parse(
  '{"name": "Amir", "age": 36}',
  (key, value) => {
    if (key === '') {
      return value;
    } else {
      return 'nevermind';
    }
  }
);
RESULT:
{age: 'nevermind', name: 'nevermind'}
```

## Modern JavaScript: Computed methods and accessors

As usual, this feature exists on classes as well. We can create methods, static methods, accessors, and static accessors, all with computed names. Those names can be built up using any JavaScript expression.

```javascript

class User {
  constructor(name) {
    this.name = name;
  }

  static [['get', 'User', 'Name'].join('')](user) {
    return user.name;
  }
}

User.getUserName(new User('Cindy'));
RESULT: 'Cindy'
```

What if we define the class, then change the value that was used to compute a method name? For example, if a method name comes from a variable, we might give that variable a new value.

That won't have any effect: once the class is defined, the computed method names aren't re-evaluated. There are ways to change methods after a class is defined, but computed method names aren't one of them!

(Remember that accessing an object property that doesn't exist will return undefined.)

If the class is created dynamically inside a function, we can use the function's arguments to name the class's accessors and methods.

Computed method names are confusing because they break one of our assumptions: "I can look at the class to see what methods it has". Fortunately, they're not used very often!

Computed method names are confusing because they break one of our assumptions: "I can look at the class to see what methods it has". Fortunately, they're not used very often!

However, you'll encounter computed methods and accessors eventually, especially in library or framework code that needs to be very generic. When you do encounter them, the rule is relatively simple: when the class is being constructed, the virtual machine evaluates the string to get the method or accessor name. After the class is defined, those names won't change.

## Modern JavaScript: Symbol basics
Most JavaScript data types can't be used as object keys. For example, if we try to use true as a key, it gets converted into the string 'true'.

If an object already has the key 'true', and we try to add true as a key, we'll only end up overwriting the value that already exists at true. The object will still have only one key at the end: 'true'.

Modern versions of JavaScript have alleviated this limitation somewhat by adding symbols. Symbols are a new data type that can be used in object keys. We'll begin by exploring the basics of how symbols work, then move on to using them as keys.

We can define a symbol by giving it a description: Symbol('name') or Symbol('dataIsSynced'). The description should say what the symbol is used for.

Symbol equality works like array equality. A given array is always equal to itself. Likewise, a given symbol is always equal to itself.

Two arrays are never equal to each other, even if they contain the same elements. Likewise, two symbols are never equal to each other, even if they have the same description.

Now that we've seen the basics of symbols, we can start using them as object keys. But how exactly do we get a symbol key into an object? If we store it in a nameSymbol variable, and then say {nameSymbol: 1}, then the unquoted nameSymbol key is just a string. The key will be 'nameSymbol' and the nameSymbol variable won't be referenced at all.

To use the symbol itself as a key, we can use computed property syntax: {[nameSymbol]: ...}. Then, to access a symbol key, we can do user[nameSymbol]. (Trying to access it with user.nameSymbol would have the same problem as before: it would look up the value at the string key 'nameSymbol'.

Symbol descriptions are usually strings, so it's tempting to think of symbols as just a special kind of string. But that's a mistake! Here's an example of why:

We can use the string `name` as an object key. We can also use the symbol Symbol('name') as an object key. An object can have both of those keys at once, with each holding a different value!

```javascript
const nameString = 'name';
const nameSymbol = Symbol('name');
const user = {
  [nameString]: 'Amir',
  [nameSymbol]: 'Betty'
};
[user['name'], user[nameSymbol]];
RESULT:
['Amir', 'Betty']
```

## Modern JavaScript: Builtin Symbols

JavaScript defines several symbols for us. These are used for metaprogramming, which means "changing the behavior of a program using code". Using these built-in symbols, we can modify how JavaScript runs our code. Here's one example:

```javascript
const user = {name: 'Dalili'};
user.toString();
RESULT:
'[object Object]'
```
The string '[object Object]' isn't very informative, but we can change this behavior if we like.

When we call .toString() on an object, the JavaScript runtime looks for a property on that object named Symbol.toStringTag. If that property exists, the runtime puts it inside the '[object ...]' string.

## Modern JavaScript: Problems with object keys

JavaScript object keys must be strings, numbers, or symbols.

When object is a key then  it's automatically converted into a string via its .toString() method. But the default .toString() method always returns '[object Object]'. All five cities are converted into that string, so the object only has that one string as a key!

This is a big problem: it significantly limits our ability to model complex relationships between data. Fortunately, JavaScript has a solution: the map data type, which we'll see in another lesson coming up soon!

## Modern JavaScript: Symbols are metadata

Before symbols, object property names were always strings, which was nice and simple. Now they can be strings or symbols. Why bother adding this complication?

The answer is that Symbols let us draw an important distinction: symbols are "out of band data", or "metadata". They're not a normal part of the object.

For example, when we serialize an object with JSON.stringify, symbol properties are ignored completely. Only the regular string properties are serialized. After round-tripping an object into JSON and back, none of the symbol properties remain.

This is a very convenient part of symbols. If implementation details like Symbol.toStringTag did show up in JSON, that could cause our API responses to be excessively large, hurting performance. Worse, if we happen to store any sensitive information in symbol properties, then including them in API responses could cause security problems.

Fortunately, neither of those problems occurs because JSON.stringify ignores symbol properties. Other well-behaved data serialization tools will also ignore symbol properties.

## Modern JavaScript: Defining iterators

At a glance, it seems like for-of loops have specific knowledge about arrays and strings. But they don't! Instead, JavaScript defines a more general way to access the elements of a datatype in a particular order. Arrays, strings, and some other data types are "iterables": loops (and other constructs) can iterate over them. ("Iterate" means "perform repeatedly".)

There are rules about how iteration works. The thing being iterated over (like an array, a string, or a custom object that we define) exposes certain methods. Then, the thing doing the iteration (like a for-of loop) calls those methods. As long as both sides agree on what the methods are, the iteration works.

There are rules about how iteration works. The thing being iterated over (like an array, a string, or a custom object that we define) exposes certain methods. Then, the thing doing the iteration (like a for-of loop) calls those methods. As long as both sides agree on what the methods are, the iteration works.

There are rules about how iteration works. The thing being iterated over (like an array, a string, or a custom object that we define) exposes certain methods. Then, the thing doing the iteration (like a for-of loop) calls those methods. As long as both sides agree on what the methods are, the iteration works.

There are rules about how iteration works. The thing being iterated over (like an array, a string, or a custom object that we define) exposes certain methods. Then, the thing doing the iteration (like a for-of loop) calls those methods. As long as both sides agree on what the methods are, the iteration works.

First, we get an iterator from the letters array by calling the Symbol.iterator method. (Symbol.iterator is a special symbol defined by the language itself, used only for this purpose.)

The iterator object has a next method. Calling that will give us one element of the array. The element is wrapped up in an object that provides both the element value and a done flag to tell us whether there's more data remaining.

Get an iterator by calling letters[Symbol.iterator]().
Call the iterator's next method repeatedly.
When next().done is true, stop and throw the iterator away.

```javascript
class NumbersBelowThree {
  [Symbol.iterator]() {
    return new NumberIterator();
  }
}

class NumberIterator {
  constructor() {
    this.value = 0;
  }

  next() {
    if (this.value < 3) {
      const value = this.value;
      this.value += 1;
      return {value, done: false};
    } else {
      return {value: undefined, done: true};
    }
  }
}

const numbers = [];
for (const n of new NumbersBelowThree()) {
  numbers.push(n);
}
numbers;
RESULT:
[0, 1, 2]
```

The class approach and the object approach are both fine. In some situations, one will be a better match than the other. But in many cases, it's a matter of preference, or of choosing what you're more familiar with. Or, if you're updating existing code, it's probably best to work within the existing design, whether it's class-based or object-based.

Generators can be used here.

The entire process of iterating is governed by the two "iteration protocols". ("Protocol" means "an agreed-upon procedure".)

Protocol 1 is the "iterable protocol". That means that an object has a Symbol.iterator method. Arrays, strings, and our custom objects above follow the iterable protocol.

Protocol 2 is the "iterator protocol". That means that an object has a next method, which in turn returns an object {value, done}. Our NumberIterator class and the object returned by our makeIterator function both follow the iteration protocol. So do the iterators that we get by doing someArray[Symbol.iterator]().

We can think of a for-of loop in terms of the two protocols:

It uses the iterable protocol to get a fresh iterator.
It uses the iterator protocol to consume that iterator.
It discards the iterator because it's now used up.

These terms are all confusingly similar: the iterable protocol and iterator protocol combine to make up the iteration protocols. You'll probably mix them up; we definitely mix them up. They're only correct in this lesson because we checked and re-checked the docs many times. This is fine; the important part is how they work, not what they're called!

## Values and variables
Variables are not values.
Variables point to values.
Rules of Assignment
1. left must be variable
2. The right side of an assignment must be an expression, so it always results in a value. Our expression can be something simple, like 2 or 'hello'. It can also be a more complicated expression

expresion is a question to JavaScript. 2 is expresion and is called literals.

We can’t really pass variables to functions. We pass the current value of the variable, for example `'pet'`.
It turns out that a variable name like pet can serve as an expression too! When we write pet, we’re asking JavaScript a question: “What is the current value of pet?” To answer our question, JavaScript follows pet “wire,” and gives us back the value at the end of this “wire.”

You need to have clarity on what you can do with each JavaScript concept in your head.

We can’t point variables to each other! Variables always point to values.

   - Primitive values are immutable. They’re a permanent part of our JavaScript universe—we can’t create, destroy, or change them. For example, we can’t set a property on a string value because it is a primitive value. Arrays are not primitive, so we can set their properties.

   - Variables are not values. Each variable points to a particular value. We can change which value it points to by using the = assignment operator.

   - Variables are like wires. A “wire” is not a JavaScript concept—but it helps us imagine how variables point to values. When we do an assignment, there’s always a wire on the left, and an expression (resulting in a value) on the right.

   - Look out for contradictions. If two things that you learned seem to contradict each other, don’t get discouraged. Usually it’s a sign that there’s a deeper truth lurking underneath.

   - Language matters. We’re building a mental model so that we can be confident in what can or cannot happen in our universe. We might speak about these ideas in a casual way (and nitpicking is often counterproductive) but our understanding of the meaning behind the terms needs to be precise.

## BigInts
In our JavaScript universe, there is an infinite number of BigInts—one for each integer in math.

BigInts are great for financial calculations where precision is especially important.

## Strings
Primitive, immutable.

## Symbols
Symbols like door keys: they hide away some information inside an object and control which parts of code can access it.

## Primitives some facts:
- Not all numbers can be perfectly represented in JavaScript. Their decimal part offers more precision closer to 0, and less precision further away from it.
- Numbers from invalid math operations like 1 / 0 or 0 / 0 are special. NaN is one of such numbers. They may appear due to coding mistakes.
- `typeof(NaN)` is a number because NaN is a numeric value. It’s called “Not a Number” because it represents the idea of an “invalid” number.

## Garbage collector
JavaScript doesn’t offer guarantees about when garbage collection happens.

## Equality of values
`Object.is` same value equality. Points to same value? `==>` `true`.

`NaN` is the only value that’s not Strict Equal to itself.

```javascript
NaN === NaN // false
-0 === 0 && 0 === -= // true
Object.is(0, -0) // false
```
BUT `Object.is(NaN, NaN) // true`

How to check if `const size` is `NaN`?
```javascript
Number.isNaN(size)
Object.is(size, NaN)
size !== size
```

[More here](https://stackoverflow.com/a/1573715/458193)

### Recap
- JavaScript has several kinds of equality. They include same value equality, strict equality, and loose equality.

## General links
[Execute program](https://www.executeprogram.com/)
