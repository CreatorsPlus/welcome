# Understanding Runtime Environments in TypeScript
<!-- Doc type - Knowledge Pill 💊 -->

## What are Runtime Environments? 🎯

A runtime environment is where your code actually executes. Each environment provides different:
- Global objects
- Built-in APIs
- Features and limitations

## Common Runtime Environments 🌍

### 1. Browser Environment
```typescript
// Browser-specific globals
window.innerWidth;     // Browser window width
document.querySelector("div");  // DOM API
localStorage.setItem("key", "value");  // Web Storage API

// These are automatically typed in TypeScript!
const button = document.querySelector("button");
button?.addEventListener("click", () => {
    console.log("Clicked!"); // Outputs to browser console
});
```

### 2. Node.js Environment
```typescript
// Node.js specific globals
process.env.NODE_ENV;  // Environment variables
require("path");       // CommonJS modules
__dirname;            // Current directory path

// Node.js built-in modules
import * as fs from 'fs';
fs.readFileSync('file.txt'); // File system operations
```

## Environment Detection 🔍

```typescript
// Checking the current environment
const isBrowser = typeof window !== 'undefined';
const isNode = typeof process !== 'undefined' && process.versions?.node;

// Safe environment-specific code
if (isBrowser) {
    // Browser-only code
    window.localStorage.getItem("key");
} else if (isNode) {
    // Node.js-only code
    process.exit(0);
}
```

## TypeScript Configuration for Different Environments 🛠️

### Browser Configuration
```json
{
    "compilerOptions": {
        "lib": ["ES2020", "DOM", "DOM.Iterable"],
        "module": "ES2020",
        "target": "ES2020",
        "moduleResolution": "bundler"
    }
}
```

### Node.js Configuration
```json
{
    "compilerOptions": {
        "lib": ["ES2020"],
        "module": "CommonJS",
        "target": "ES2020",
        "moduleResolution": "node"
    }
}
```

## Common Pitfalls ⚠️

1. **Cross-Environment Code**
   ```typescript
   // This might fail in Node.js
   const width = window.innerWidth;  // ❌

   // Better approach
   const width = typeof window !== 'undefined' 
       ? window.innerWidth 
       : null;  // ✅
   ```

2. **Module Systems**
   ```typescript
   // Browser (ES Modules)
   import { something } from './module.js';  // ✅

   // Node.js (CommonJS)
   const something = require('./module');    // Only with appropriate config
   ```

## Best Practices 💡

1. **Use Environment Abstractions**
```typescript
// storage-service.ts
export class StorageService {
    static set(key: string, value: string): void {
        if (typeof window !== 'undefined') {
            localStorage.setItem(key, value);
        } else {
            // Node.js alternative storage
            // e.g., file system or in-memory storage
        }
    }
}
```

2. **Type Definitions**
```typescript
// Declare environment-specific types
declare global {
    interface Window {
        customProperty?: string;
    }
}
```

## Environment-Specific Features 🔋

### Browser-Only Features
- DOM manipulation
- Browser APIs (localStorage, fetch, etc.)
- Window and document objects
- Browser events

### Node.js-Only Features
- File system operations
- Process management
- Network servers
- System information

---
<details>
<summary>💡 Pro Tip: Cross-Environment Development</summary>

When developing applications that need to run in multiple environments:
1. Use environment detection
2. Create abstraction layers
3. Test in all target environments
4. Use appropriate TypeScript configurations
</details>

---

## Next Steps 🚀
1. Review your project's runtime requirements
2. Configure TypeScript appropriately
3. Implement environment-specific checks
4. Create abstraction layers when needed