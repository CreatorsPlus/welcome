# Time Travel with Async Code! 🚀
<!-- Doc type - Knowledge Pill 💊 -->

## Your Super Powers! 🎯
Learn to:
- Make code wait
- Fetch data
- Handle loading states
- Catch errors like a pro!

## Quick Win! ⚡
Try this in your console (F12):
```typescript
// Your first time travel!
console.log('Starting... 🏁');

setTimeout(() => {
    console.log('Time traveled 2 seconds! ✨');
}, 2000);

console.log('Getting ready... ⚡');
```
Watch the magic order! 🎭

## Level 1: Promises 🎬

### Make a Promise
```typescript
// Create your first promise!
const magicPromise = new Promise<string>((resolve) => {
    setTimeout(() => {
        resolve('✨ Magic happened! ✨');
    }, 1000);
});

// Use it!
magicPromise.then(result => {
    console.log(result);  // See the magic!
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Made first promise
- [x] Saw async magic
- [ ] Ready for more!

## Level 2: Async/Await ⏰

### The Easy Way
```typescript
// Magic spell: async/await
async function getMagic(): Promise<string> {
    console.log('Starting spell... 🔮');
    
    // Wait 1 second
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    return '✨ Spell complete! ✨';
}

// Try it!
getMagic().then(result => {
    console.log(result);
});
```

### Even Easier!
```typescript
// Use immediately!
async function playMagic() {
    console.log('Getting ready... 🎭');
    const result = await getMagic();
    console.log(result);
}

// Run it!
playMagic();
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Used async/await
- [x] Made magic happen
- [ ] Level up to fetch!

## Level 3: Fetch Data! 🎣

### Get Data From Internet
```typescript
// Get a random joke!
async function getJoke(): Promise<string> {
    try {
        console.log('Finding a joke... 🃏');
        
        const response = await fetch(
            'https://api.chucknorris.io/jokes/random'
        );
        const data = await response.json();
        
        return data.value;
    } catch (error) {
        return 'Oops! No joke found 😅';
    }
}

// Try it!
getJoke().then(joke => {
    console.log('Here is your joke:', joke);
});
```

## Mini Games! 🎮

### Game 1: Loading States
```typescript
// Show loading status!
async function loadGame(): Promise<void> {
    const status = document.querySelector('#status');
    if (!status) return;

    status.textContent = 'Loading... 🔄';
    
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    status.textContent = 'Ready! 🎮';
}

// Play it!
loadGame();
```

### Game 2: Countdown Timer
```typescript
async function countdown(from: number): Promise<void> {
    for (let i = from; i > 0; i--) {
        console.log(`${i}... 🕒`);
        await new Promise(resolve => setTimeout(resolve, 1000));
    }
    console.log('Blast off! 🚀');
}

// Start countdown!
countdown(5);
```

---
🎉 **POWER-UPS** 🎉

### Safe Fetch Helper
```typescript
// Safe data getter!
async function getData<T>(url: string): Promise<T | null> {
    try {
        const response = await fetch(url);
        return await response.json();
    } catch (error) {
        console.log('Oops!', error);
        return null;
    }
}

// Try it!
interface Todo {
    title: string;
    completed: boolean;
}

getData<Todo>('https://jsonplaceholder.typicode.com/todos/1')
    .then(todo => {
        if (todo) {
            console.log('Got todo:', todo.title);
        }
    });
```

## Practice Time! 🏃‍♂️

### Challenge 1: Delay Function
```typescript
// Make a function that waits!
async function delay(ms: number): Promise<void> {
    // Your code here!
    // Hint: use setTimeout with Promise
}

// Use it like this:
async function test() {
    console.log('Start');
    await delay(1000);
    console.log('End');
}
```

### Challenge 2: Retry Logic
```typescript
// Try something multiple times!
async function tryTimes<T>(
    action: () => Promise<T>,
    times: number
): Promise<T | null> {
    // Your code here!
    // Hint: use a loop and try/catch
    return null;
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Used Promises
- [x] Mastered async/await
- [x] Fetched data
- [ ] Ready for more challenges!

## Remember! 🧠
- async = happens later
- await = wait for result
- always use try/catch
- loading states are cool!

---
Need a Break? 🎮
- Perfect time while code loads!
- Stretch!
- Get water!
- Watch a promise resolve!

You're now a time wizard! 🧙‍♂️