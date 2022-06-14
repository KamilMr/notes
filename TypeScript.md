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

### errors
-type error: The left-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type.

