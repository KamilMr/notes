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


## general links
[Execute program](executeprogram.com)
