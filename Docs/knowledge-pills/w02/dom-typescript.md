# DOM Types: Your Browser Playground! 🎮
<!-- Doc type - Knowledge Pill 💊 -->

## Your Mission 🎯
Learn to:
- Find elements on the page
- Change stuff safely
- Make things happen!

## Quick Win! 🌟
Open your browser console (F12) and try:
```typescript
// Change page title - instant result!
document.title = "I did it! 🎉";
```

## Finding Elements - Level 1 🎯

### Button Quest
```typescript
// Find ONE button
const button = document.querySelector<HTMLButtonElement>('button');

// Did you find it? Check!
if (button) {
    button.style.backgroundColor = 'purple';  // Magic! ✨
    button.textContent = 'Click me!';         // New text! 📝
}
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Found an element
- [x] Changed its style
- [ ] Ready for more!

## Element Types - Level 2 🎨

### Quick Reference
```typescript
// 🎯 Common element types:
const button: HTMLButtonElement    // Buttons
const input: HTMLInputElement      // Text boxes
const div: HTMLDivElement         // Containers
const img: HTMLImageElement       // Pictures
```

### Try It! 
```typescript
// 🎮 Get input value
const input = document.querySelector<HTMLInputElement>('#username');
if (input) {
    console.log('Input says:', input.value);
}
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Know basic types
- [x] Can check values
- [ ] Let's make stuff happen!

## Making Changes - Level 3 🔄

### Super Safety Pattern™
```typescript
// 🛡️ Safe way to change elements
function changeElement(id: string, newText: string): void {
    // Find it
    const element = document.getElementById(id);
    
    // Check it
    if (element) {
        // Change it! ✨
        element.textContent = newText;
    }
}

// Use it!
changeElement('message', 'Hello! 👋');
```

## Mini Game: Element Hunter! 🎮

### Level 1: Find Elements
```typescript
// Your mission: Find these elements!
const title = /* find h1 element */
const button = /* find button element */
const input = /* find input element */

// Check your score:
console.log({
    title: !!title,
    button: !!button,
    input: !!input
});
```

### Level 2: Change Elements
```typescript
// Your mission: Make these changes!
if (title) {
    // 1. Change title color
}

if (button) {
    // 2. Add click message
}

if (input) {
    // 3. Add placeholder
}
```

---
🎉 **POWER-UPS** 🎉

### Quick Type Check
```typescript
// 🔍 Is it an input?
function isInput(element: Element): element is HTMLInputElement {
    return element instanceof HTMLInputElement;
}

// Try it!
const mystery = document.querySelector('.unknown');
if (isInput(mystery)) {
    console.log('Found input value:', mystery.value);
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Find elements
- [x] Change elements safely
- [x] Check element types
- [ ] Ready for practice!

## Practice Arena! 🏟️

### Challenge 1: Color Changer
Make a button that changes its color when clicked:
```typescript
// Your code here!
const button = document.querySelector<HTMLButtonElement>('button');

// Hint: use button?.addEventListener('click', () => {
//    Change color here!
// });
```

### Challenge 2: Input Echo
Show what user types in real-time:
```typescript
// Your code here!
const input = document.querySelector<HTMLInputElement>('input');
const display = document.querySelector<HTMLDivElement>('#display');

// Hint: use input?.addEventListener('input', () => {
//    Show the text!
// });
```

## Remember! 🧠
- Always check if element exists (`if (element)`)
- Use proper types (`HTMLButtonElement`, etc.)
- Test your changes!

---
🎮 **NEED A BREAK?**
- Take 5 minutes
- Stretch
- Come back refreshed!

Ready for the next level? You've got this! 💪