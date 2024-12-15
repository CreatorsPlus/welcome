# Auth Magic: Protect Your Kingdom! 🏰
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Guard your routes
- Create magic tokens
- Protect user secrets
- Keep intruders out!

## Quick Win! ⚡
Try this auth spell:
```typescript
import jwt from 'jsonwebtoken';

// Create a magic token!
const token = jwt.sign(
    { userId: '123', role: 'wizard' },
    'your-secret-key',
    { expiresIn: '1h' }
);

console.log('Magic token:', token);
// eyJhbGciOiJIUzI1NiIs... ✨
```

## Level 1: Basic Guards! 🛡️

### Auth Guardian
```typescript
// Create your guardian!
class AuthGuardian {
    private static SECRET = process.env.JWT_SECRET || 'super-secret';
    
    static createToken(user: {
        id: string;
        role: string;
    }): string {
        return jwt.sign(user, this.SECRET, {
            expiresIn: '24h'
        });
    }
    
    static verifyToken(token: string): any {
        try {
            return jwt.verify(token, this.SECRET);
        } catch (error) {
            console.log('❌ Invalid token!');
            return null;
        }
    }
}

// Use your guardian!
app.post('/login', (req, res) => {
    // Pretend we verified password here
    const token = AuthGuardian.createToken({
        id: '123',
        role: 'wizard'
    });
    
    res.json({
        message: '🎉 Welcome, wizard!',
        token
    });
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Created tokens
- [x] Verified tokens
- [ ] Ready for protection!

## Level 2: Route Protection! 🔐

### Protection Spell
```typescript
// Protect your routes!
const protectRoute = (req: Request, res: Response, next: NextFunction) => {
    const token = req.headers.authorization?.split(' ')[1];
    
    if (!token) {
        res.status(401).json({
            message: '🚫 No magic token found!'
        });
        return;
    }
    
    const user = AuthGuardian.verifyToken(token);
    if (!user) {
        res.status(401).json({
            message: '⚠️ Your magic token has expired!'
        });
        return;
    }
    
    // Add user to request
    req.user = user;
    next();
};

// Use it!
app.get('/secret-spells',
    protectRoute,
    (req, res) => {
        res.json({
            spells: ['Lumos', 'Wingardium Leviosa'],
            message: '✨ Secret spells revealed!'
        });
    }
);
```

### Role Guards
```typescript
// Check wizard roles!
const checkRole = (role: string) => {
    return (req: Request, res: Response, next: NextFunction) => {
        if (req.user.role !== role) {
            res.status(403).json({
                message: '🚫 You cannot cast this spell!'
            });
            return;
        }
        next();
    };
};

// Use it!
app.post('/admin/create-spell',
    protectRoute,
    checkRole('archmage'),
    (req, res) => {
        res.json({
            message: '✨ New spell created!'
        });
    }
);
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Protected routes
- [x] Checked roles
- [ ] Level up to passwords!

## Level 3: Password Magic! 🔑

### Password Enchanter
```typescript
import bcrypt from 'bcrypt';

class PasswordEnchanter {
    private static SALT_ROUNDS = 10;
    
    static async enchant(password: string): Promise<string> {
        return bcrypt.hash(password, this.SALT_ROUNDS);
    }
    
    static async verify(
        password: string,
        enchanted: string
    ): Promise<boolean> {
        return bcrypt.compare(password, enchanted);
    }
}

// Use it!
class WizardKeeper {
    async registerWizard(
        username: string,
        password: string
    ): Promise<void> {
        // Enchant the password
        const enchantedPassword = await PasswordEnchanter
            .enchant(password);
            
        // Store the wizard
        await db.wizards.create({
            username,
            password: enchantedPassword
        });
    }
    
    async verifyWizard(
        username: string,
        password: string
    ): Promise<boolean> {
        // Find the wizard
        const wizard = await db.wizards
            .findOne({ username });
            
        if (!wizard) return false;
        
        // Verify the spell
        return PasswordEnchanter.verify(
            password,
            wizard.password
        );
    }
}
```

## Mini Games! 🎮

### Game 1: Token Decoder
```typescript
// Create a token inspector!
class TokenInspector {
    static inspect(token: string): void {
        try {
            const [header, payload] = token.split('.');
            
            console.log('🔍 Header:', 
                Buffer.from(header, 'base64')
                    .toString('utf8')
            );
            
            console.log('📦 Payload:',
                Buffer.from(payload, 'base64')
                    .toString('utf8')
            );
            
            console.log('✅ Token is valid!');
        } catch (error) {
            console.log('❌ Invalid token!');
        }
    }
}

// Try it!
const token = AuthGuardian.createToken({
    id: '123',
    role: 'wizard'
});

TokenInspector.inspect(token);
```

### Game 2: Auth Tester
```typescript
// Create an auth tester!
class AuthTester {
    private tokens: Map<string, string> = new Map();
    
    async testAuth(
        username: string,
        password: string
    ): Promise<string> {
        // Step 1: Register
        console.log('📝 Registering wizard...');
        await keeper.registerWizard(username, password);
        
        // Step 2: Verify
        console.log('🔍 Verifying wizard...');
        const isValid = await keeper
            .verifyWizard(username, password);
            
        if (!isValid) throw new Error('Auth failed!');
        
        // Step 3: Create token
        console.log('✨ Creating token...');
        const token = AuthGuardian.createToken({
            username,
            role: 'wizard'
        });
        
        // Store token
        this.tokens.set(username, token);
        return token;
    }
}

// Try it!
const tester = new AuthTester();
await tester.testAuth('merlin', 'excalibur123');
```

---
🎉 **POWER-UPS** 🎉

### Quick Auth Helper
```typescript
// Make auth easier!
class AuthHelper {
    static async quickAuth(
        req: Request,
        res: Response,
        next: NextFunction
    ): Promise<void> {
        const token = req.headers.authorization?.split(' ')[1];
        req.user = token ? 
            AuthGuardian.verifyToken(token) : 
            null;
        next();
    }
    
    static requireAuth(
        req: Request,
        res: Response,
        next: NextFunction
    ): void {
        if (!req.user) {
            res.status(401).json({
                message: '🚫 Authentication required!'
            });
            return;
        }
        next();
    }
}

// Use it!
app.use(AuthHelper.quickAuth);

app.get('/profile',
    AuthHelper.requireAuth,
    (req, res) => {
        res.json({
            profile: req.user,
            message: '🧙‍♂️ Wizard profile loaded!'
        });
    }
);
```

## Practice Time! 🏃‍♂️

### Challenge 1: Magic Sessions
```typescript
// Create session manager that:
// 1. Stores active sessions
// 2. Expires old sessions
// 3. Prevents multiple logins
// 4. Tracks login attempts

interface SessionManager {
    // Your code here!
}
```

### Challenge 2: Auth Flow
```typescript
// Create auth flow that:
// 1. Registers wizards
// 2. Verifies emails
// 3. Handles password reset
// 4. Logs activities

interface AuthFlow {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Created tokens
- [x] Protected routes
- [x] Secured passwords
- [ ] Ready for more!

## Remember! 🧠
- Always hash passwords
- Never store secrets in tokens
- Use HTTPS in production
- Implement rate limiting
- Log suspicious activity

---
Need a Break? 🎮
- Test your auth!
- Create tokens!
- Check security!
- Come back stronger!

You're a security wizard now! 🧙‍♂️