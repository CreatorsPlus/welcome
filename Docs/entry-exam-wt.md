# JavaScript Functions Entry Test - Study Guide & Walkthrough

## Prerequisites
Before taking the test, you should be familiar with:
- Basic JavaScript syntax
- Variables and data types
- Console.log statements
- Basic arithmetic operators

## Question 1: Function Return Values and String Concatenation

### Concept Explained
```javascript
function greet(name) {
    return "Hello, " + name;
}
console.log(greet("John"));
```

This question tests your understanding of:
1. Function parameters
2. String concatenation
3. Return statements
4. Function execution

### Walkthrough
- The function `greet` takes one parameter called `name`
- Inside the function, we concatenate (join) two strings:
  - The literal string `"Hello, "`
  - The value passed in the `name` parameter
- The `return` statement sends this concatenated string back
- When we call `greet("John")`, the function returns `"Hello, John"`
- The `console.log` then outputs this returned value

### Learning Resources
- [MDN: Functions - Returning Values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#return_values)
- [MDN: String Concatenation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Strings#concatenating_strings)

## Question 2: Writing a Basic Function

### Concept Explained
```javascript
function add(a, b) {
    // Answer: return a + b
}
```

This question tests your understanding of:
1. Function parameters
2. Arithmetic operations
3. Return statements
4. Function syntax

### Walkthrough
- The function should take two parameters: `a` and `b`
- Inside the function, we need to:
  1. Use the addition operator (`+`) to sum the parameters
  2. Use the `return` keyword to send back the result
- The complete solution is `return a + b`
- This allows us to use the function like: `add(5, 3)` which would return `8`

### Learning Resources
- [MDN: Function Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#function_parameters)
- [MDN: Arithmetic Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#arithmetic_operators)

## Question 3: Understanding Undefined Parameters

### Concept Explained
```javascript
function multiply(x, y) {
    return x * y;
}
console.log(multiply());
```

This question tests your understanding of:
1. Default parameter values
2. The `undefined` value
3. JavaScript type coercion
4. Function parameter handling

### Walkthrough
- When a function is called without arguments, the parameters get the value `undefined`
- In this case, `multiply()` runs with:
  - `x = undefined`
  - `y = undefined`
- When JavaScript tries to multiply `undefined * undefined`, it results in `NaN` (Not a Number)
- This is why the correct answer is `NaN`

### Learning Resources
- [MDN: undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)
- [MDN: NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)

## Best Practices for Writing Functions

1. Always use clear, descriptive function names
2. Keep functions focused on a single task
3. Use meaningful parameter names
4. Include return statements when functions need to provide values
5. Consider adding default parameters for optional values

## Practice Exercises

1. Try modifying the `greet` function to accept a second parameter for the time of day:
```javascript
function greet(name, timeOfDay) {
    return "Good " + timeOfDay + ", " + name;
}
```

2. Write a function that multiplies three numbers:
```javascript
function multiplyThree(x, y, z) {
    return x * y * z;
}
```

3. Create a function that returns a default greeting if no name is provided:
```javascript
function greetWithDefault(name = "friend") {
    return "Hello, " + name;
}
```

## Additional Resources
### Documentation
- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [JavaScript.info - Functions](https://javascript.info/function-basics)

### Video Tutorials
- [JavaScript Functions Playlist - Traversy Media](https://www.youtube.com/playlist?list=PLillGF-RfqbYE6Ik_EuXA2iZFcE082B3s)
