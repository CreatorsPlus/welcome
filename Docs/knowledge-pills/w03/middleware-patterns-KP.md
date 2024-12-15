# Middleware Magic: Chain of Powers! ⚡
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Chain middleware powers
- Guard your routes
- Transform requests
- Handle errors like a pro!

## Quick Win! ⚡
Try this magical middleware:
```typescript
// Your first middleware power!
const logSpell = (req: Request, res: Response, next: NextFunction) => {
    console.log(`🔮 ${req.method} ${req.path}`);
    next();
};

// Use your power!
app.use(logSpell);
```

## Level 1: Guard Routes 🛡️

### Authentication Guard
```typescript
// Protect your routes!
interface User {
    id: number;
    role: 'wizard' | 'apprentice';
}

const guardSpell = (req: Request, res: Response, next: NextFunction) => {
    const magicToken = req.headers.authorization;
    
    if (!magicToken) {
        res.status(401).json({
            message: 'No magic token! 🚫'
        });
        return;
    }
    
    // Magic token exists! ✨
    next();
};

// Use your guard!
app.use('/secret-spells', guardSpell);
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Made first middleware
- [x] Protected routes
- [ ] Ready for transformations!

## Level 2: Transform Power! 🔄

### Request Transformer
```typescript
// Transform incoming data!
const transformSpell = (req: Request, res: Response, next: NextFunction) => {
    if (req.body) {
        // Convert all strings to lowercase
        Object.keys(req.body).forEach(key => {
            if (typeof req.body[key] === 'string') {
                req.body[key] = req.body[key].toLowerCase();
            }
        });
    }
    
    next();
};

// Add custom data
const addMagicData = (req: Request, res: Response, next: NextFunction) => {
    req.magicPower = 100;  // TypeScript will complain - we'll fix this!
    next();
};

// Fix TypeScript error with declaration merging
declare global {
    namespace Express {
        interface Request {
            magicPower?: number;
        }
    }
}
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Transform data
- [x] Add custom properties
- [ ] Level up to chains!

## Level 3: Chain Magic! ⛓️

### Middleware Chains
```typescript
// Combine your powers!
const spellChain = [
    logSpell,
    guardSpell,
    transformSpell,
    addMagicData
];

// Use the chain!
app.use('/spells', spellChain);

// Or make a mega-chain factory!
function createSpellChain(...middlewares: RequestHandler[]) {
    return (req: Request, res: Response, next: NextFunction) => {
        // Execute each middleware in sequence
        const executeSpell = (index: number): void => {
            if (index === middlewares.length) {
                next();
                return;
            }
            
            middlewares[index](req, res, () => executeSpell(index + 1));
        };
        
        executeSpell(0);
    };
}
```

## Mini Games! 🎮

### Game 1: Timeout Guard
```typescript
// Create a timeout protector!
const timeoutGuard = (timeout: number) => (
    req: Request,
    res: Response,
    next: NextFunction
) => {
    const timer = setTimeout(() => {
        res.status(408).json({
            message: 'Spell took too long! ⏰'
        });
    }, timeout);
    
    res.on('finish', () => clearTimeout(timer));
    next();
};

// Use it!
app.use(timeoutGuard(5000));  // 5 second timeout
```

### Game 2: Rate Limiter
```typescript
// Control the magic flow!
class SpellLimiter {
    private spells: Map<string, number[]> = new Map();
    
    check(key: string, limit: number, window: number): boolean {
        const now = Date.now();
        const spellTimes = this.spells.get(key) || [];
        
        // Remove old spells
        const recent = spellTimes.filter(time => 
            time > now - window
        );
        
        // Check limit
        if (recent.length >= limit) {
            return false;
        }
        
        // Add new spell
        recent.push(now);
        this.spells.set(key, recent);
        return true;
    }
}

// Use it!
const limiter = new SpellLimiter();
const rateLimitSpell = (req: Request, res: Response, next: NextFunction) => {
    const key = req.ip;
    if (!limiter.check(key, 10, 60000)) {  // 10 requests per minute
        res.status(429).json({
            message: 'Too many spells! 🔥'
        });
        return;
    }
    next();
};
```

---
🎉 **POWER-UPS** 🎉

### Error Catcher
```typescript
// Catch those errors!
const errorCatcher = (
    error: Error,
    req: Request,
    res: Response,
    next: NextFunction
) => {
    console.error('🔥 Spell backfired:', error);
    res.status(500).json({
        message: 'Magic mishap!',
        error: error.message
    });
};

// Use it last!
app.use(errorCatcher);
```

## Practice Time! 🏃‍♂️

### Challenge 1: Validation Chain
```typescript
// Create a chain that:
// 1. Validates request body
// 2. Sanitizes input
// 3. Transforms data
// 4. Adds validation result

// Start here:
interface ValidationResult {
    valid: boolean;
    errors: string[];
}

// Your code here!
```

### Challenge 2: Cache Middleware
```typescript
// Create middleware that:
// 1. Checks cache for response
// 2. Returns cached data if found
// 3. Caches new responses
// 4. Handles cache expiration

// Start here:
class CacheManager {
    private cache: Map<string, any> = new Map();
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Chain middleware
- [x] Transform data
- [x] Handle errors
- [ ] Ready for more!

## Remember! 🧠
- Keep middleware focused
- Chain in right order
- Handle all errors
- Always call next()

---
Need a Break? 🎮
- Test your chains!
- Add new powers!
- Fix those bugs!
- Come back stronger!

You're a middleware master now! 🧙‍♂️