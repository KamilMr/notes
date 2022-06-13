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

