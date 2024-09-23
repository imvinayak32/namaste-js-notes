# Episode 18 : Higher-Order Functions ft. Functional Programming

### Q: What is Higher Order Function?
**Ans**: Higher-order functions are regular functions that take one or more functions as arguments and/or return functions as a value from it. Eg: 
```js
function x() {
    console.log("Hi");
};
function y(x) {
    x();
};
y(x); // Hi
// y is a higher order function
// x is a callback function
```

## Let's try to understand how we should approach solution in interview.
> Using few concepts of "Functional Programming"
>
> Think logic in terms of functions and use generic type functions as well.
1. I have an array of radius and I have to calculate area using these radius and store in an array.

```js
const radius = [1, 2, 3, 4];
const calculateArea = function(radius) {
    const output = [];
    for (let i = 0; i < radius.length; i++) {
        output.push(Math.PI * radius[i] * radius[i]);
    } 
    return output;
}
console.log(calculateArea(radius));
```

2. We have to calculate array of circumference more.
```js
const radius = [1, 2, 3, 4];
const calculateCircumference = function(radius) {
    const output = [];
    for (let i = 0; i < radius.length; i++) {
        output.push(2 * Math.PI * radius[i]);
    } 
    return output;
}
console.log(calculateCircumference(radius));
```

3. We have to calculate array of diameter more.
```js
const radius = [1, 2, 3, 4];
const calculateDiameter = function(radius) {
    const output = [];
    for (let i = 0; i < radius.length; i++) {
        output.push(2 * radius[i]);
    } 
    return output;
}
console.log(calculateDiameter(radius));
```

> But over here we are violating some principle like DRY Principle !!!

### Let's observe the better approach
```js
const radiusArr = [1, 2, 3, 4];

// logic to calculate area
const area = function (radius) {
    return Math.PI * radius * radius;
}
// logic to calculate circumference
const circumference = function (radius) {
    return 2 * Math.PI * radius;
}
// logic to calculate diameter
const diameter = function (radius) {
    return 2 * radius;
}

// Generic Function - by passing logic, we can extract different results out of it!
const calculate = function(radiusArr, logic) {
    const output = [];
    for (let i = 0; i < radiusArr.length; i++) {
        output.push(logic(radiusArr[i]));
    } 
    return output;
}
console.log(calculate(radiusArr, area));
console.log(calculate(radiusArr, circumference));
console.log(calculate(radiusArr, diameter));
```
* Over here calculate() is HOF
* Over here we have extracted logic into separate functions. This is the beauty of functional programming.

### Another way - map
  
```js
  console.log(radiusArr.map(area)) == console.log(calculate(radiusArr, area));
  // map will iterate through radiusArr and uses area() for each of it's value
```

### Polyfill of map
* Over here calculate is nothing but polyfill of map function
* Let's convert above calculate function as map function
```js
Array.prototype.calculate = function(operation) {
    const output = [];
    for (let i = 0; i < this.length; i++) {
        output.push(operation(this[i]));
    } 
    return output;
}
console.log(radiusArr.calculate(area))
```
