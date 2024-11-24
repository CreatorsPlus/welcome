# Understanding Runtime Environments in TypeScript
<!-- Doc type - Knowledge Pill 💊 -->

## Goal
Understand different JavaScript/TypeScript runtime environments and how to work with them effectively.

## Step 1: What is a Runtime Environment?

A runtime environment is where your code executes. Different environments provide different:
* Global objects (window, document, process)
* Available APIs (DOM API, File System API)
* Default behaviors

## Step 2: Browser Environment

```typescript
// Browser-specific features
const width = window.innerWidth;
const button = document.querySelector('button');
localStorage.setItem('key', 'value');

button?.addEventListener('click', () => {
    console.log('Clicked!');  // Outputs to browser console
});
```

## Step 3: Node.js Environment

```typescript
// Node.js specific features
const path = require('path');
console.log(process.env.NODE_ENV);  // Environment variables
console.log(__dirname);            // Current directory

// File system operations
import * as fs from 'fs';
fs.readFileSync('file.txt');
```

## Step 4: Running Code in Different Environments

### Browser Code
Save in `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <script src="app.js"></script>
</head>
<body>
    <button id="myButton">Click me</button>
</body>
</html>
```

Save in `app.ts`:
```typescript
document.getElementById('myButton')?.addEventListener('click', () => {
    console.log('Button clicked!');
});
```

Run with:
1. Compile: `tsc app.ts`
2. Open `index.html` in browser

### Node.js Code
Save in `script.ts`:
```typescript
console.log('Current directory:', process.cwd());
```

Run with:
```bash
tsc script.ts
node script.js
```

## Step 5: Environment Detection

```typescript
const isBrowser = typeof window !== 'undefined';
const isNode = typeof process !== 'undefined';

if (isBrowser) {
    // Browser-only code
    window.localStorage.getItem('key');
} else if (isNode) {
    // Node.js-only code
    process.exit(0);
}
```

## Step 6: Practice Exercise

1. Create a function that works in both environments:
```typescript
function getEnvironmentInfo(): string {
    if (typeof window !== 'undefined') {
        return `Browser: ${window.innerWidth}x${window.innerHeight}`;
    } else {
        return `Node.js: ${process.version}`;
    }
}
```

2. Test in both environments to see different outputs.

---
<details>
<summary>💡 Pro Tip: Cross-Environment Development</summary>

When developing for multiple environments:
1. Use environment checks before accessing specific APIs
2. Create abstraction layers for environment-specific code
3. Test your code in all target environments
</details>