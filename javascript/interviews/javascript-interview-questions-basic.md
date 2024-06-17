Here's a rephrased and reordered version of your questions to make them easier to understand and ordered by difficulty and similarity:

### Basic Questions

## Question 1. What will be the output of the following code?

```javascript
var output = (function(x) {
  delete x;
  return x;
})(0);

console.log(output);
```

<details><summary><b>Answer</b></summary>

The output will be `0`. The `delete` operator is used to remove properties from objects. Here, `x` is a local variable, not an object property, so the `delete` operator has no effect on it.

</details>

## Question 2. What will be the output of the following code?

```javascript
var x = 1;
var output = (function() {
  delete x;
  return x;
})();

console.log(output);
```

<details><summary><b>Answer</b></summary>

The output will be `1`. The `delete` operator is used to remove properties from objects. Here, `x` is a global variable of type `number`, not an object property, so the `delete` operator has no effect on it.

</details>

## Question 3. What will be the output of the following code?

```javascript
var x = { foo : 1 };
var output = (function() {
  delete x.foo;
  return x.foo;
})();

console.log(output);
```

<details><summary><b>Answer</b></summary>

The output will be `undefined`. The `delete` operator removes the `foo` property from the `x` object. After deletion, `x.foo` no longer exists, so it returns `undefined`.

</details>

### Intermediate Questions

## Question 4. How can you check if an object is an array in JavaScript?

<details><summary><b>Answer</b></summary>

You can check if an object is an array using several methods:

1. Using `Array.isArray`:
```javascript
Array.isArray(arrayList);
```

2. Using `Object.prototype.toString`:
```javascript
if(Object.prototype.toString.call(arrayList) === '[object Array]') {
  console.log('Array!');
}
```

3. Using jQuery (if available):
```javascript
if($.isArray(arrayList)) {
  console.log('Array');
} else {
  console.log('Not an array');
}
```

</details>

## Question 5. How can you empty an array in JavaScript?

<details><summary><b>Answer</b></summary>

There are several ways to empty an array:

1. Assigning a new empty array:
```javascript
arrayList = [];
```
Be careful as this does not affect references to the original array.

2. Setting the length to 0:
```javascript
arrayList.length = 0;
```
This method clears the array and affects all references to it.

3. Using `splice`:
```javascript
arrayList.splice(0, arrayList.length);
```
This method clears the array and affects all references to it.

4. Using a loop:
```javascript
while(arrayList.length) {
  arrayList.pop();
}
```
This method is less common and not recommended for frequent use.

</details>

## Question 6. What is the difference between `undefined` and `not defined` in JavaScript?

<details><summary><b>Answer</b></summary>

- `undefined`: A variable is declared but not assigned a value.
  ```javascript
  var x;
  console.log(x); // output: undefined
  ```
  
- `not defined`: A variable is neither declared nor assigned a value.
  ```javascript
  console.log(y); // Output: ReferenceError: y is not defined
  ```

Using `typeof` on an undeclared variable returns `undefined`:
```javascript
typeof undeclared_variable; // Output: undefined
```

</details>

## Question 7. For which value of `x` will the following statements not be the same?

```javascript
if(x <= 100) {...}
if(!(x > 100)) {...}
```

<details><summary><b>Answer</b></summary>

For `NaN` and any value that converts to `NaN`, the statements will not be the same. 

- `NaN <= 100` is `false`
- `NaN > 100` is also `false`

Use `isNaN()` to check for `NaN` values:
```javascript
isNaN(x); // returns true if x is NaN
```

</details>

### Advanced Questions

## Question 8. What is a closure in JavaScript? Can you provide an example?

<details><summary><b>Answer</b></summary>

A closure is a function defined inside another function, allowing it to access variables from its parent function's scope.

Example:
```javascript
var globalVar = "abc"; // Global variable

(function outerFunction(outerArg) {
  var outerFuncVar = 'x'; // Variable in outerFunction's scope
  
  (function innerFunction(innerArg) {
    var innerFuncVar = "y"; // Variable in innerFunction's scope
    console.log(
      "outerArg = " + outerArg + "\n" +
      "outerFuncVar = " + outerFuncVar + "\n" +
      "innerArg = " + innerArg + "\n" +
      "innerFuncVar = " + innerFuncVar + "\n" +
      "globalVar = " + globalVar
    );
  })(5); // innerFunction invoked with 5
})(7); // outerFunction invoked with 7
```

Output:
```javascript
outerArg = 7
outerFuncVar = x
innerArg = 5
innerFuncVar = y
globalVar = abc
```

</details>

## Question 9. What is the drawback of declaring methods directly in JavaScript objects?

<details><summary><b>Answer</b></summary>

Declaring methods directly in objects is memory inefficient because each instance of the object creates a new copy of the method.

Example:
```javascript
var Employee = function (name, company, salary) {
  this.name = name || "";
  this.company = company || "";
  this.salary = salary || 5000;

  // Method declared directly
  this.formatSalary = function () {
    return "$ " + this.salary;
  };
};

// Method added to prototype
Employee.prototype.formatSalary2 = function() {
  return "$ " + this.salary;
};

// Creating objects
var emp1 = new Employee('Yuri Gagarin', 'Company 1', 1000000);
var emp2 = new Employee('Dinesh Gupta', 'Company 2', 1039999);
var emp3 = new Employee('Erich Fromm', 'Company 3', 1299483);
```

Each instance (`emp1`, `emp2`, `emp3`) has its own copy of `formatSalary`, but shares `formatSalary2` from `Employee.prototype`.

</details>

## Question 10. Write a `mul` function which works with the following syntax:

```javascript
console.log(mul(2)(3)(4)); // Output: 24
console.log(mul(4)(3)(4)); // Output: 48
```

<details><summary><b>Answer</b></summary>

```javascript
function mul(x) {
  return function(y) { // Anonymous function
    return function(z) { // Anonymous function
      return x * y * z;
    };
  };
}
```

The `mul` function returns nested functions that take the next argument and finally multiply all arguments together.

</details>