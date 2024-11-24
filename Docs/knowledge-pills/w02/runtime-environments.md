# Understanding Runtime Environments in TypeScript
<!-- Doc type - Knowledge Pill 💊 -->

## A Quick Note About Terminals 🖥️

A terminal (also called command line or console) is a text-based interface where you can:
- Run commands
- Execute programs
- Navigate your filesystem

Common terminal programs:
- Windows: Command Prompt, PowerShell, Git Bash
- macOS/Linux: Terminal, iTerm

```bash
# Example terminal commands
ls          # List files (macOS/Linux)
dir         # List files (Windows)
cd folder   # Change directory
```

## How to Run the Examples 🏃‍♂️

### Browser Examples

1. **Using Browser Console:**
   - Open your browser (Chrome, Firefox, etc.)
   - Right-click anywhere on a page
   - Select "Inspect" or press F12
   - Go to "Console" tab
   ```typescript
   // Try these in your browser console
   window.innerWidth;  // Shows browser width
   document.title;     // Shows page title
   ```

2. **Using HTML File:**
   ```html
   <!-- Create index.html -->
   <!DOCTYPE html>
   <html>
   <head>
       <title>TypeScript Browser Example</title>
       <!-- Important: use .js file, not .ts -->
       <script src="app.js" defer></script>
   </head>
   <body>
       <button id="myButton">Click me!</button>
   </body>
   </html>
   ```

   ```typescript
   // Create app.ts
   const button = document.querySelector("#myButton");
   button?.addEventListener("click", () => {
       console.log("Button clicked!");
   });
   ```

   To run:
   ```bash
   # In your terminal
   tsc app.ts         # Compile TypeScript to JavaScript
   # Open index.html in your browser
   ```

### Node.js Examples

1. **Create a Node.js Script:**
   ```typescript
   // Create script.ts
   console.log("Current directory:", process.cwd());
   console.log("Node.js version:", process.version);
   ```

2. **Run in Terminal:**
   ```bash
   # Compile and run
   tsc script.ts
   node script.js

   # Or use ts-node to run directly
   npm install -g ts-node
   ts-node script.ts
   ```

## Setting Up Development Environments 🛠️

### Browser Development Setup
```bash
# Create project
mkdir ts-browser-demo
cd ts-browser-demo

# Initialize TypeScript
tsc --init

# Create files
touch index.html
touch app.ts
```

### Node.js Development Setup
```bash
# Create project
mkdir ts-node-demo
cd ts-node-demo

# Initialize npm and TypeScript
npm init -y
tsc --init

# Install dependencies
npm install @types/node --save-dev

# Create source file
touch script.ts
```

## Common Development Tools 🔧

1. **Browser Development:**
   - Live Server (VS Code extension)
   - Browser Developer Tools
   - TypeScript compiler in watch mode
   ```bash
   tsc --watch
   ```

2. **Node.js Development:**
   - ts-node (Run TypeScript directly)
   - nodemon (Auto-restart on changes)
   ```bash
   npm install -g ts-node nodemon
   nodemon --exec ts-node script.ts
   ```

## Practical Examples with Setup Instructions 📝

### Browser Example
```bash
# Setup
mkdir browser-demo
cd browser-demo
tsc --init
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<head>
    <script src="app.js" defer></script>
</head>
<body>
    <div id="output"></div>
    <button id="btn">Click me</button>
</body>
</html>
```

```typescript
// app.ts
const output = document.getElementById("output");
const button = document.getElementById("btn");

button?.addEventListener("click", () => {
    if (output) {
        output.textContent = "Button clicked at: " + new Date().toLocaleTimeString();
    }
});
```

To run:
```bash
tsc app.ts
# Open index.html in browser
# Or use VS Code's Live Server extension
```

### Node.js Example
```bash
# Setup
mkdir node-demo
cd node-demo
npm init -y
tsc --init
npm install @types/node --save-dev
```

```typescript
// script.ts
import * as fs from 'fs';

// Read a file
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error reading file:', err);
        return;
    }
    console.log('File contents:', data);
});
```

To run:
```bash
# Method 1: Compile and run
tsc script.ts
node script.js

# Method 2: Using ts-node
ts-node script.ts
```

## Environment-Specific Debugging 🐛

### Browser Debugging
- Use browser DevTools (F12)
- Set breakpoints in Sources panel
- Monitor console.log outputs
- Inspect network requests

### Node.js Debugging
- Use VS Code debugger
- Use --inspect flag with Node.js
- Console.log to terminal
- Use debugging tools like ndb

---
<details>
<summary>💡 Pro Tip: Development Workflow</summary>

1. Use separate terminal windows for:
   - Running TypeScript compiler (tsc --watch)
   - Running your application
   - Git commands
2. Keep browser DevTools open while developing
3. Use appropriate environment-specific debugging tools
</details>

---

Now that you understand how to run examples in different environments, let's look at the previous code samples in context...

[Rest of the original content continues...]