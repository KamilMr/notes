## Basic
Unlike JavaScript, variables in TypeScript have static types. Types come after a :.


```
let anything: string = 'any' + 'thing';
anything;
```
The compiler forces us to use types correctly. If we use them incorrectly, it's a type error and the program won't compile.


error: type error: Type 'string' is not assignable to type 'number'.

Types always have to match. Every variable has a type. Every value we assign must match the variable's type.

We can't assign a variable of one type to a variable of another type. That causes a type error.

### What bugs and problems does TypeScript prevent?

-passing the wrong arguments to a function
-passing a number where a string was expected
-passing an object where an array was expected
-TypeScript compiler also catches mistakes like "undefined is not a function" and "Cannot read property 'someProperty' of undefined" before the code even begins executing.

## Operators

Operators like + and * can only be used on types that make sense. For example, we can add numbers with + and multiply with *.
We can also use + to concatenate strings. However, we can't use * on strings. That's a type error.

In JavaScript, 'a' * 'b' is NaN. If that happens in a real system. TypeScrip prevent from doing this.

However, TypeScript will still allow some questionable combinations. For example, 1 + '1' gives '11', as in JavaScript.

## JavaScript builtins
TypeScript knows the types of built-in JavaScript functions and methods.

## Inference
TypeScript infers types - Adding types to every variable would get tiresome. Fortunately, we can often avoid writing the types. TypeScript will determine them for us. We call this type inference.

Coins: With type inference, the types are still enforced! It frees us from writing the types out, but it doesn't reduce safety.
Types aren't only for correctness! Experienced static language users use types for clarity as well.

## Functions
```
function add1(n: number): number {
  return n + true;
}
add1(2);
```

`1 + true` isn't a legal TypeScript program at all. It can never even begin executing.

## Arrays
Array types are marked with []. An array of numbers is number[], string[].

## Type keyword
We can declare our own names for types using the type keyword. It looks similar to declaring a variable with let. By convention, user-defined type names are UpperCamelCased.

```
type MyStringType = string; // TypeScript syntax only
let s: MyStringType = 'hello';
```
Each TypeScript program is a valid JavaScript program, but with extra annotations: the types. After checking types, the TypeScript compiler generates JavaScript by removing all TypeScript-specific syntax from a program. Then, the result is run as JavaScript.

TypeScript compiler throws the types away is important. Most notably, it means that there's no way to inspect types at runtime. Types are only used during type checking, then they're thrown away.

*type erasure* the types are used for type checking

### errors
-type error: The left-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type.


## Return type inference
Inference only means that the compiler can determine the types for us.

## Syntax errors vs type errors

Difference js ts => In JavaScript, any code with valid syntax will run. In TypeScript, code must have valid syntax and must type check. Only then will it run.
What's the difference between a syntax error and a type error? We can think of it by analogy to English. "Vase triangle avocado cat grape" is not valid English syntax. Each of those words is part of English, but they can't be in that order. No English sentence can be made of five nouns in a row.

Likewise, function return class if var is invalid TypeScript syntax. Each of those words is part of TypeScript, but they can't be in that order. If we try to compile that "code", the compiler rejects its syntax. The type checker never even runs.

When our syntax is correct, the compiler checks semantics (types). "That tree is angry" is valid English syntax, but doesn't "type check". Trees can't be angry (outside of fantasy novels).

In TypeScript, a + b is valid syntax. But if a is a number and b is a boolean, then a + b won't type check.

## Object types
myObject.someProperty will return undefined if someProperty doesn't exist.
The most common symptom is the "undefined is not a function" error when we do myObject.someProperty().

we can't use expressions like 1 + 1 or true || false in a type. That would be a syntax error because expressions are never allowed in types.

```JavaScript
type User = {
  email: string
  admin: boolean
};
let amir: User = {
  email: 'amir@example.com',
  admin: true,
};
```

## Tuples
TypeScript supports tuples, which are arrays of fixed length. For example, [number, number] is a tuple of two numbers. It must be exactly two numbers; not one and not three. If the length doesn't match, it's a type error.

Tuples can have different types in each index. This is different from arrays, where every element must have the same type.

## Generic Arrays
`Array<number>` Array types like Array<number> are an example of generics. We can think of Array as a type with a "hole" in it. An array of numbers, Array<number>, fills the hole with the number type. An array of strings, Array<string>, fills the hole with the string type.

