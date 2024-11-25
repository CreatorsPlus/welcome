# TypeScript Calculator: Comprehensive Guide for Beginners

## ⌚ READING TIME
- 1 hour

## 📝 Setup (Break Point 1)

### Step 1: Create Project Structure
```bash
# Create a new folder for your project
mkdir typescript-calc
cd typescript-calc
```
This creates a folder named 'typescript-calc' and moves you into it.

### Step 2: Initialize Project
```bash
# Initialize npm project
npm init -y

# Install required packages
npm install --save-dev typescript @types/node
```

`npm init -y` creates a package.json file with default settings.
The `-y` flag means "yes to all questions".

💡 **Pro Tip**: If you see any errors in red, read them carefully and don't panic. Most errors tell you exactly what's missing.

### Step 3: Create Source File
```bash
# Create the main TypeScript file
touch calculator.ts
```
This creates an empty file named 'calculator.ts'.

---
⏰ **Break Point**: Good time for a 2-minute stretch!
---

## 📚 Building the Code (Break Point 2)

### Step 1: Basic Setup
Open calculator.ts and add:
```typescript
// Import readline for user input
import * as readline from "readline";

// Create readline interface
const rl = readline.createInterface({
    input: process.stdin,    // Read from standard input (keyboard)
    output: process.stdout   // Write to standard output (console)
});
```

💡 **Pro Tip**: Comments help you remember what each part does. Add them as you code!

<details>
<summary> 💊 Confused? Click to see a full explanation
</summary>

> **Full code walkthrough** [here](1-w1-project-01-commandline-claculator-code-wt.md)

</details>

### Step 2: Calculator Class
Add this after the readline setup:
```typescript
class Calculator {
    // Store the last calculation result
    private lastResult: number | null = null;

    // Addition method
    add(a: number, b: number): number {
        this.lastResult = a + b;
        return this.lastResult;
    }

    // Subtraction method
    subtract(a: number, b: number): number {
        this.lastResult = a - b;
        return this.lastResult;
    }

    // Multiplication method
    multiply(a: number, b: number): number {
        this.lastResult = a * b;
        return this.lastResult;
    }

    // Division method with error checking
    divide(a: number, b: number): string | number {
        if (b === 0) {
            return "Error: Division by zero is not allowed.";
        }
        this.lastResult = a / b;
        return this.lastResult;
    }

    // Get the last calculated result
    getLastResult(): number | null {
        return this.lastResult;
    }
}
```

Let's break down what each part does:
- `private lastResult`: Stores last calculation, only accessible inside class
- Each method (add, subtract, etc.):
  - Takes two numbers as input
  - Performs calculation
  - Saves result
  - Returns result

---
⏰ **Break Point**: Good time for a 5-minute break!
---

## 🔄 Input Handling (Break Point 3)

### Step 1: Question Helper
Add this after the Calculator class:
```typescript
// Helper function to handle user input
function question(query: string): Promise<string> {
    return new Promise((resolve) => {
        rl.question(query, resolve);
    });
}
```
This wraps readline's question in a Promise for easier async/await usage.

### Step 2: Validation Functions
Add these validation helpers:
```typescript
// Check if input is a valid number
function isValidNumber(value: string): boolean {
    return !isNaN(parseFloat(value)) && isFinite(Number(value));
}

// Check if operation is valid
function isValidOperation(operation: string): boolean {
    return ['+', '-', '*', '/'].includes(operation);
}
```

💡 **Pro Tip**: Always validate user input! Never trust it to be correct.

---
⏰ **Break Point**: Take a short break if needed!
---

## 🎮 Main Program Logic (Break Point 4)

### Step 1: Calculate Function
```typescript
async function calculate(): Promise<boolean> {
    // Get first number
    let num1: string = await question("Enter first number: ");
    while (!isValidNumber(num1)) {
        console.log("Invalid input. Please enter a valid number.");
        num1 = await question("Enter first number: ");
    }

    // Get second number
    let num2: string = await question("Enter second number: ");
    while (!isValidNumber(num2)) {
        console.log("Invalid input. Please enter a valid number.");
        num2 = await question("Enter second number: ");
    }

    // Get operation
    let operation: string = await question("Choose an operation (+, -, *, /): ");
    while (!isValidOperation(operation)) {
        console.log("Invalid operation. Please use +, -, *, or /");
        operation = await question("Choose an operation (+, -, *, /): ");
    }

    // Do calculation
    await performCalculation(parseFloat(num1), parseFloat(num2), operation);

    // Ask to continue
    const answer = await question("\nWould you like to perform another calculation? (y/n): ");
    return answer.toLowerCase() === 'y';
}
```

### Step 2: Calculation Function
```typescript
async function performCalculation(num1: number, num2: number, operation: string): Promise<void> {
    const calc = new Calculator();
    let result: string | number;

    try {
        // Choose operation based on input
        switch (operation) {
            case "+":
                result = calc.add(num1, num2);
                break;
            case "-":
                result = calc.subtract(num1, num2);
                break;
            case "*":
                result = calc.multiply(num1, num2);
                break;
            case "/":
                result = calc.divide(num1, num2);
                break;
            default:
                throw new Error("Invalid operation");
        }

        // Show result
        console.log("\nCalculation Result:");
        console.log(`${num1} ${operation} ${num2} = ${result}`);

    } catch (error) {
        console.error("Calculation error:", error.message);
    }
}
```

---
⏰ **Break Point**: Good time for another break!
---

## 🏁 Final Steps (Break Point 5)

### Step 1: Main Function
Add at the end:
```typescript
async function main() {
    try {
        console.log("Welcome to TypeScript Calculator!");
        console.log("=================================");
        
        let continueCalculating = true;
        while (continueCalculating) {
            continueCalculating = await calculate();
        }
        
        console.log("\nThank you for using TypeScript Calculator!");
    } catch (error) {
        console.error("An error occurred:", error);
    } finally {
        rl.close();
    }
}

// Start the program
main();
```

### Step 2: Run the Program
1. Compile the TypeScript:
```bash
npx tsc calculator.ts --target ES2016
```

2. Run the program:
```bash
node calculator.js
```

## 🐛 Troubleshooting Common Issues

1. "Cannot find name 'process'":
   - Run: `npm install --save-dev @types/node`

2. "Promise" related errors:
   - Add `--target ES2016` to compilation command

3. Program exits too early:
   - Check that readline.close() is only in main's finally block

## 🌟 Success Tips
- Take frequent short breaks (every 20-30 minutes)
- Test each part after writing it
- Keep your terminal and code editor visible at the same time
- Use descriptive variable names
- Add comments as you write code
- If stuck, read error messages from top to bottom
