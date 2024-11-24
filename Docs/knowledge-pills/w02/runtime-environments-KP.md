# Runtime Environments Made Simple! 🚀
<!-- Doc type - Knowledge Pill 💊 -->

## What You'll Learn 🎯
- Where your code runs (browser vs Node.js)
- How to check where you are
- How to write code that works everywhere

## Quick Win! 🌟
Run this in your browser console (press F12):
```typescript
console.log("I'm in a browser!");
console.log("Window width:", window.innerWidth);
```
<img width="921" alt="Screenshot 2024-11-24 at 9 36 04 PM" src="https://github.com/user-attachments/assets/fce1fa79-2792-465b-9165-eaef57ceb2fd">

✅ If it works - You're in a browser!
❌ If it fails - You're probably in Node.js!

## Browser vs Node.js: The Basics 🔄

### Browser Has:
```typescript
// ✨ These work in browser
window.innerWidth     // Screen width
document.title        // Page title
localStorage          // Save data

// 🎨 Try this!
document.body.style.backgroundColor = 'pink';
```

### Node.js Has:
<details>
    <summary>
      💡 Where to type this?
    </summary>

> In your terminal start the node REPL by typing `node` and then type the following code. like this:
> <img width="686" alt="Screenshot 2024-11-24 at 9 39 27 PM" src="https://github.com/user-attachments/assets/240a3a4b-4b74-481a-93c0-f590cc98f28e">

</details>

```typescript
// 🛠️ These work in Node.js
process.version      // Node version
require('fs')        // File system
__dirname           // Current folder
```


## Quick Check! ✋
Before writing code, ask:
1. Am I in a browser?
2. Am I in Node.js?
3. Do I need to support both?

---
⭐ **CHECKPOINT 1** ⭐
- [x] You know about browsers
- [x] You know about Node.js
- [ ] Let's write safe code!

## Writing Safe Code! 🛡️

### Safe Check Pattern
```typescript
// 🔍 Safe way to check environment
if (typeof window !== 'undefined') {
    // Browser stuff here!
    console.log("I'm in a browser!");
} else {
    // Node.js stuff here!
    console.log("I'm in Node.js!");
}
```

Try it! ▶️
1. Copy the code
2. Try in browser console
3. Try in Node.js
4. See what happens!

---
⭐ **CHECKPOINT 2** ⭐
- [x] You can check your environment
- [x] You can write safe code
- [ ] Let's practice!

## Practice Time! 🎮

### Mini-Challenge 1:
Make a function that says "Hello" differently in browser and Node:
```typescript
function sayHello(): void {
    if (typeof window !== 'undefined') {
        // Your browser code here!
        
    } else {
        // Your Node.js code here!
        
    }
}
```

### Mini-Challenge 2:
What will this log?
```typescript
console.log(typeof window);
console.log(typeof process);
```

---
🎉 **YOU DID IT!** 🎉
- [x] You understand environments
- [x] You can write safe code
- [x] You're ready for more!

## Remember! 🧠
- Browser = Website stuff
- Node.js = Server stuff
- Always check where you are!

Need a break? Take one! 🎮
Ready for more? Let's go! 🚀
