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

## general links
[Execute program](https://www.executeprogram.com/)
