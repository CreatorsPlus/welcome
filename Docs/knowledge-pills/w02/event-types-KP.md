# Make Things Happen: Fun with Events! 🎪
<!-- Doc type - Knowledge Pill 💊 -->

## Level Up Your Skills! 🎯
Learn to:
- Make buttons do stuff
- React to clicks
- Handle typing
- Make magic happen!

## Instant Magic! ⚡
Copy this to your console (F12):
```typescript
// Make anything clickable!
document.body.addEventListener('click', () => {
    console.log('🎉 CLICKED! 🎉');
});
```
Click anywhere... See the magic! ✨

## Level 1: Click Events 🖱️

### Button Magic
```typescript
// Find a button
const button = document.querySelector<HTMLButtonElement>('button');

// Make it do something!
button?.addEventListener('click', () => {
    // Change button color
    button.style.backgroundColor = 'purple';
    button.textContent = 'Clicked! 🎉';
});
```

Try it! Create a button and paste this code ▶️

---
⭐ **CHECKPOINT 1** ⭐
- [x] Made first event
- [x] Changed button
- [ ] Ready for more!

## Level 2: Mouse Events 🎮

### Mouse Position Tracker
```typescript
// Track the mouse!
document.addEventListener('mousemove', (e) => {
    console.log(`
        Mouse at: 
        X: ${e.clientX} 
        Y: ${e.clientY}
    `);
});
```

### Fun with Mouse Events
```typescript
const box = document.querySelector('.box');

// Hover effects!
box?.addEventListener('mouseenter', () => {
    console.log('🐭 Mouse in!');
});

box?.addEventListener('mouseleave', () => {
    console.log('🐭 Mouse out!');
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Track mouse
- [x] Handle hover
- [ ] Level up to keyboards!

## Level 3: Keyboard Magic ⌨️

### Key Logger
```typescript
// Watch for typing!
document.addEventListener('keydown', (e) => {
    console.log(`
        Key pressed: ${e.key}
        Was it Shift? ${e.shiftKey ? 'Yes! 👍' : 'No 👎'}
        Was it Ctrl? ${e.ctrlKey ? 'Yes! 👍' : 'No 👎'}
    `);
});
```

### Input Tracker
```typescript
const input = document.querySelector<HTMLInputElement>('input');

input?.addEventListener('input', (e) => {
    const value = (e.target as HTMLInputElement).value;
    console.log('Typing:', value);
});
```

## Mini Games! 🎮

### Game 1: Color Changer
```typescript
// Make a button change colors on click!
const colorButton = document.querySelector<HTMLButtonElement>('#colorBtn');

const colors = ['red', 'blue', 'green', 'purple', 'pink'];
let colorIndex = 0;

colorButton?.addEventListener('click', () => {
    // Change to next color
    colorButton.style.backgroundColor = colors[colorIndex];
    // Move to next color (loop back to start if needed)
    colorIndex = (colorIndex + 1) % colors.length;
});
```

### Game 2: Key Counter
```typescript
let keyCount = 0;

document.addEventListener('keypress', () => {
    keyCount++;
    console.log(`Keys pressed: ${keyCount} 🎹`);
});
```

---
🎉 **POWER-UPS** 🎉

### Event Helper
```typescript
// Make events easier!
function onEvent<K extends keyof HTMLElementEventMap>(
    element: HTMLElement,
    event: K,
    action: (e: HTMLElementEventMap[K]) => void
): void {
    element.addEventListener(event, action);
}

// Use it!
const button = document.querySelector('button')!;
onEvent(button, 'click', () => {
    console.log('Clicked! 🎯');
});
```

## Challenge Time! 🏃‍♂️

### Challenge 1: Button Counter
Make a button that counts its clicks:
```typescript
// Your mission:
// 1. Create a button
// 2. Track clicks
// 3. Show count on button
// Bonus: Add reset feature!
```

### Challenge 2: Secret Code
Listen for a secret keyboard combination:
```typescript
// Example: Listen for "hello"
let typed = '';

document.addEventListener('keypress', (e) => {
    typed += e.key;
    
    if (typed.includes('hello')) {
        console.log('Secret found! 🎉');
        typed = '';
    }
});
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Handle clicks
- [x] Track keyboard
- [x] Make fun stuff
- [ ] Ready for more!

## Quick Reference 📝
```typescript
// Common events:
'click'      // Mouse clicks
'input'      // Typing
'keydown'    // Key pressed
'mousemove'  // Mouse moving
'submit'     // Form submit
```

## Remember! 🧠
- Check if elements exist
- Use proper event types
- Make it fun!
- Test your code!

---
Need a Break? 🎮
- Move around!
- Stretch!
- Try your new events!
- Come back excited!

You're becoming an event master! 🌟