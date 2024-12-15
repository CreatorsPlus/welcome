# Express & TypeScript: Server Magic! 🚀
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Build typed Express servers
- Handle requests safely
- Send awesome responses
- Make routing fun!

## Quick Win! ⚡
Try this basic server:
```typescript
import express from 'express';

const app = express();

app.get('/', (req, res) => {
    res.send('Server magic! ✨');
});

app.listen(3000, () => {
    console.log('Magic happens on port 3000! 🎩');
});
```

## Level 1: Type-Safe Routes 🛡️

### Basic Route Types
```typescript
import { Request, Response } from 'express';

// Magic route with types!
app.get('/spells', (req: Request, res: Response) => {
    res.json({
        spell: 'Lumos',
        power: 'Light',
        cooldown: 0
    });
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Made first route
- [x] Added types
- [ ] Ready for requests!

## Level 2: Request Powers! 🎮

### Query Parameters
```typescript
// Get info from URLs!
app.get('/potions', (req: Request<{}, {}, {}, {strength?: string}>, res: Response) => {
    const strength = req.query.strength || 'normal';
    console.log(`Making ${strength} potion! 🧪`);
});

// Try it: /potions?strength=strong
```

### Body Parsing
```typescript
// Read request bodies!
interface SpellBook {
    name: string;
    spells: string[];
}

app.post('/spellbooks', (
    req: Request<{}, {}, SpellBook>,
    res: Response
) => {
    const { name, spells } = req.body;
    console.log(`New spellbook: ${name} with ${spells.length} spells! 📚`);
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Handle queries
- [x] Parse bodies
- [ ] Level up to middleware!

## Level 3: Middleware Magic! 🧙‍♂️

### Magic Shields
```typescript
// Protect your routes!
function magicShield(
    req: Request,
    res: Response,
    next: NextFunction
): void {
    const hasWand = req.headers['x-wand-type'];
    
    if (!hasWand) {
        res.status(403).json({
            error: 'You shall not pass! 🧙‍♂️'
        });
        return;
    }
    
    next();
}

// Use your shield!
app.use('/restricted', magicShield);
```

### Error Catching
```typescript
// Catch those errors!
app.use((
    err: Error,
    req: Request,
    res: Response,
    next: NextFunction
) => {
    console.error('🔥 Spell backfired:', err);
    res.status(500).json({
        message: 'Magic mishap!',
        error: err.message
    });
});
```

## Mini Games! 🎮

### Game 1: Route Builder
```typescript
// Create a typed route builder!
type RouteHandler<T> = (req: Request<{}, {}, T>, res: Response) => void;

function createRoute<T>(handler: RouteHandler<T>) {
    return handler;
}

// Use it!
const addSpell = createRoute<{spell: string}>((req, res) => {
    console.log(`Learning ${req.body.spell}! ✨`);
    res.json({ learned: true });
});
```

### Game 2: Response Builder
```typescript
// Make response helper!
class MagicResponse {
    static success<T>(data: T) {
        return {
            success: true,
            data,
            sparkles: '✨'
        };
    }
    
    static error(message: string) {
        return {
            success: false,
            error: message,
            smoke: '💨'
        };
    }
}

// Use it!
app.get('/magic', (req, res) => {
    res.json(MagicResponse.success({
        spell: 'Wingardium Leviosa'
    }));
});
```

---
🎉 **POWER-UPS** 🎉

### Quick Type Helper
```typescript
// Make types easier!
type ApiResponse<T> = {
    data: T;
    message: string;
    timestamp: number;
};

function respond<T>(res: Response, data: T, message: string): void {
    const response: ApiResponse<T> = {
        data,
        message,
        timestamp: Date.now()
    };
    res.json(response);
}

// Use it!
app.get('/wands', (req, res) => {
    respond(res, ['holly', 'oak', 'elder'], 'Wands found! 🪄');
});
```

## Practice Time! 🏃‍♂️

### Challenge 1: Magic Router
```typescript
// Build a router that:
// 1. Logs all requests
// 2. Checks for magic token
// 3. Times the response

// Start here:
const magicRouter = express.Router();
```

### Challenge 2: Spell Validator
```typescript
// Create middleware that:
// 1. Validates spell format
// 2. Checks power level
// 3. Prevents forbidden spells

interface Spell {
    name: string;
    power: number;
    element: 'fire' | 'water' | 'air' | 'earth';
}

// Your code here!
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Route with types
- [x] Use middleware
- [x] Handle errors
- [ ] Ready for more!

## Remember! 🧠
- Always type your routes
- Use middleware for common tasks
- Handle errors gracefully
- Keep responses consistent

---
Need a Break? 🎮
- Test your routes!
- Try new middlewares!
- Make cool responses!
- Come back magical!

You're a server wizard now! 🧙‍♂️