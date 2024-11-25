# TypeScript Calculator: Line-by-Line Explanation

## 📚 Import Section
```typescript
import * as readline from "readline";
```
- This line imports Node.js's readline module
- `*` means import everything
- `as readline` gives us a nickname to use the module
- We need this to get user input from the terminal

💡 **Pro Tip**: Always put imports at the top of your file

## 🧮 Calculator Class
```typescript
class Calculator {
    private lastResult: number | null = null;
```
- `class` creates a blueprint for our calculator
- `private` means only the Calculator class can access lastResult
- `number | null` means it can be a number or null
- `= null` sets the initial value

### Addition Method
```typescript
    add(a: number, b: number): number {
        this.lastResult = a + b;
        return this.lastResult;
    }
```
- `add` is the method name
- `(a: number, b: number)` means it takes two numbers as input
- `: number` means it returns a number
- `this.lastResult = a + b` stores the result
- `return this.lastResult` sends back the answer

💡 **Pro Tip**: The other arithmetic methods (subtract, multiply, divide) follow the same pattern!

### Division Method (Special Case)
```typescript
    divide(a: number, b: number): string | number {
        if (b === 0) {
            return "Error: Division by zero is not allowed.";
        }
        this.lastResult = a / b;
        return this.lastResult;
    }
```
- Returns either a string (error) or number (result)
- Checks for division by zero
- Returns error message if b is zero

---
⏰ **Break Point**: Good time for a 2-minute stretch!
---

## 📥 Input Setup
```typescript
const rl = readline.createInterface({
    input: process.stdin,    // Keyboard input
    output: process.stdout   // Screen output
});
```
- Creates our input/output system
- `process.stdin` reads from keyboard
- `process.stdout` writes to screen

### Question Helper
```typescript
function question(query: string): Promise<string> {
    return new Promise((resolve) => {
        rl.question(query, resolve);
    });
}
```
- Makes asking questions easier
- Returns a Promise (lets us use await)
- `query` is what we want to ask the user
- `resolve` sends back the user's answer

## ✅ Validation Functions
```typescript
function isValidNumber(value: string): boolean {
    return !isNaN(parseFloat(value)) && isFinite(Number(value));
}
```
- Checks if input is a valid number
- `parseFloat` converts string to number
- `isFinite` makes sure it's not Infinity
- Returns true/false

```typescript
function isValidOperation(operation: string): boolean {
    return ['+', '-', '*', '/'].includes(operation);
}
```
- Checks if operation is +, -, *, or /
- `.includes()` looks for the operation in the list
- Returns true/false

---
⏰ **Break Point**: Take a short break if needed!
---

## 🔄 Calculation Functions
```typescript
async function performCalculation(num1: number, num2: number, operation: string): Promise<void> {
    const calc = new Calculator();
    let result: string | number;
```
- `async` means it can wait for things
- Creates new Calculator instance
- `result` can be either string or number

### Switch Statement
```typescript
    try {
        switch (operation) {
            case "+":
                result = calc.add(num1, num2);
                break;
```
- `try` catches any errors that might happen
- `switch` chooses the right operation
- `case "+"` handles addition
- `break` stops after doing the operation

## 🎯 Main Program Flow
```typescript
async function calculate(): Promise<boolean> {
    let num1: string = await question("Enter first number: ");
    while (!isValidNumber(num1)) {
        console.log("Invalid input. Please enter a valid number.");
        num1 = await question("Enter first number: ");
    }
```
- Gets first number from user
- Keeps asking until input is valid
- `await` waits for user's answer
- Uses our validation functions

### Main Function
```typescript
async function main() {
    try {
        console.log("Welcome to TypeScript Calculator!");
        let continueCalculating = true;
        while (continueCalculating) {
            continueCalculating = await calculate();
        }
    } finally {
        rl.close();
    }
}
```
- Main program entry point
- Shows welcome message
- Keeps calculating until user says stop
- Always closes input/output when done

💡 **Pro Tip**: The `finally` block runs no matter what happens - success or error!

## 🚀 Program Start
```typescript
main();
```
- This single line starts everything!