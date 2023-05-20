# Memoize

```js
"use strict";

const memoize = (fn) => {
  let cache = {};
  return (n, ...args) => {
    if (n in cache) {
      console.log("Fetching computed value from cache:", cache[n]);
      return cache[n];
    } else {
      let result = fn(n, ...args);
      cache[n] = result;
      console.log("Calculating intermediate result: ", result);
      return result;
    }
  };
};

const factorial = memoize((num) => {
  if (num === 0) {
    return 1;
  } else {
    return num * factorial(num - 1);
  }
});

console.log("Calculated factorial of 5: ", factorial(5)); // calculated
console.log("==============");
console.log("Partly cached/partly calculated factorial of 6: ", factorial(6)); // calculated for 6 and cached for 5
console.log("==============");

const factorialAcc = (num) => {
  const fac = (num, acc) => {
    if (num === 0) {
      return acc;
    } else {
      return fac(num - 1, num * acc);
    }
  };
  return fac(num, 1);
};

const memoizedFactorial = memoize(factorialAcc);

console.log("Factorial of 25 with accumulator calculated:");
console.log(memoizedFactorial(25)); // calculated
console.log("==============");
console.log("Factorial of 25 with accumulator cached:");
console.log(memoizedFactorial(25)); // cached
console.log("==============");
```
