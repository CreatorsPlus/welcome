# Save Your Stuff: Browser Storage Made Fun! 🎲
<!-- Doc type - Knowledge Pill 💊 -->

## Your Power-Ups 🎯
- Save data in the browser
- Find your saved stuff
- Make data persist

## Instant Win! ⚡
Try this in your console (F12):
```typescript
// Save something
localStorage.setItem('myName', 'Super Coder');

// Get it back
console.log('Saved name:', localStorage.getItem('myName'));
```
Boom! 🎉 You just saved your first piece of data!

## Storage Types - Pick Your Tool! 🛠️

### Local Storage (Saves Forever)
```typescript
// 💾 Saves until you clear it
localStorage.setItem('theme', 'dark');
localStorage.setItem('level', '42');

// Still there after refresh!
```

### Session Storage (Temporary)
```typescript
// ⏳ Only until you close tab
sessionStorage.setItem('gameScore', '1000');
sessionStorage.setItem('currentLevel', '5');

// Gone when tab closes!
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Can save data
- [x] Know storage types
- [ ] Let's save cool stuff!

## Save Cool Stuff! 🎨

### Save Colors
```typescript
// 🎨 Try this!
function saveColor(color: string): void {
    localStorage.setItem('favoriteColor', color);
    // Change page background
    document.body.style.backgroundColor = color;
}

// Use it!
saveColor('pink');  // Watch the magic!
```

### Save Player Score
```typescript
// 🎮 Game score saver
function saveScore(score: number): void {
    // Convert number to string for storage
    localStorage.setItem('highScore', score.toString());
    console.log('Score saved! 🎉');
}

// Try it!
saveScore(1000);
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Save simple data
- [x] See instant results
- [ ] Level up to objects!

## Level Up: Save Objects! 🚀

### The Easy Way
```typescript
// 🎯 Save an object
const player = {
    name: 'CoolCoder',
    level: 42,
    powers: ['jump', 'run']
};

// Save it!
localStorage.setItem('player', JSON.stringify(player));

// Get it back!
const savedPlayer = JSON.parse(
    localStorage.getItem('player') || '{}'
);

console.log('Found player:', savedPlayer);
```

## Quick Games! 🎮

### Game 1: Color Memory
```typescript
// Save your favorite colors
const colors = ['red', 'blue', 'green'];
localStorage.setItem('colors', JSON.stringify(colors));

// Challenge: Get them back!
// Your code here:
const savedColors = // ?
```

### Game 2: Settings Saver
```typescript
// Create settings
const settings = {
    volume: 80,
    brightness: 100,
    notifications: true
};

// Your mission:
// 1. Save settings
// 2. Get them back
// 3. Log them to console
```

---
🎉 **POWER-UPS** 🎉

### Safety First! 
```typescript
// 🛡️ Safe storage wrapper
function save(key: string, data: any): void {
    try {
        localStorage.setItem(key, JSON.stringify(data));
        console.log('Saved! ✨');
    } catch (error) {
        console.log('Oops! Storage full or blocked 🚫');
    }
}

// Safe getter
function load<T>(key: string, fallback: T): T {
    try {
        const data = localStorage.getItem(key);
        return data ? JSON.parse(data) : fallback;
    } catch {
        return fallback;
    }
}

// Try it!
save('pet', { name: 'Fluffy', type: 'cat' });
const pet = load('pet', { name: 'Unknown', type: 'unknown' });
```

## Practice Time! 🏃‍♂️

### Challenge 1: Todo Saver
```typescript
// Save a todo list
const todos = ['Learn TypeScript', 'Build something cool'];

// Your mission:
// 1. Save todos
// 2. Add new todo
// 3. Save again
// 4. Get full list
```

### Challenge 2: Theme Switcher
```typescript
// Save user's theme preference
function saveTheme(isDark: boolean): void {
    // Your code here!
}

// Load and apply theme
function loadTheme(): boolean {
    // Your code here!
    return false;  // Change this!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Save & load data
- [x] Handle objects
- [x] Create safe storage
- [ ] Ready to build stuff!

## Remember! 🧠
- localStorage = Forever storage
- sessionStorage = Tab-only storage
- Always use try/catch
- JSON for objects

Need a break? 🎮
- Save your progress!
- Stretch!
- Drink water!
- Come back fresh!

You're doing great! 🌟