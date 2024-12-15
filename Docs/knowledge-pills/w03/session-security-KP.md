# Session Magic: Keep Your Castle Safe! 🏰
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Manage visitor sessions
- Store secret stuff safely
- Defend against attacks
- Keep your castle secure!

## Quick Win! ⚡
Try this session spell:
```typescript
import session from 'express-session';

// Create your first session guard!
app.use(session({
    secret: 'magic-secret-key',
    resave: false,
    saveUninitialized: false,
    cookie: { secure: true }
}));

// Use it!
app.post('/login', (req, res) => {
    req.session.wizardId = '123';
    res.json({ message: '🎉 Welcome to the castle!' });
});
```

## Level 1: Session Mastery! 🔮

### Session Keeper
```typescript
// Create your session vault!
class SessionKeeper {
    private store: Map<string, any> = new Map();
    
    createSession(id: string, data: any): void {
        this.store.set(id, {
            data,
            lastAccess: Date.now()
        });
    }
    
    getSession(id: string): any {
        const session = this.store.get(id);
        if (session) {
            session.lastAccess = Date.now();
            return session.data;
        }
        return null;
    }
    
    removeSession(id: string): void {
        this.store.delete(id);
    }
    
    cleanOldSessions(maxAge: number): void {
        const now = Date.now();
        for (const [id, session] of this.store) {
            if (now - session.lastAccess > maxAge) {
                this.store.delete(id);
            }
        }
    }
}

// Use it!
const keeper = new SessionKeeper();

app.post('/enter-castle', (req, res) => {
    const sessionId = crypto.randomUUID();
    keeper.createSession(sessionId, {
        wizardName: req.body.name,
        spellPower: 100
    });
    
    res.cookie('sessionId', sessionId, {
        httpOnly: true,
        secure: true
    });
    
    res.json({ message: '🏰 Welcome to the castle!' });
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Created sessions
- [x] Managed data
- [ ] Ready for storage!

## Level 2: Secure Storage! 💎

### Redis Session Vault
```typescript
import Redis from 'ioredis';

class SessionVault {
    private redis: Redis;
    private prefix = 'session:';
    private ttl = 3600; // 1 hour
    
    constructor(redisUrl: string) {
        this.redis = new Redis(redisUrl);
    }
    
    async saveSession(
        id: string,
        data: any
    ): Promise<void> {
        const key = this.prefix + id;
        await this.redis.setex(
            key,
            this.ttl,
            JSON.stringify(data)
        );
    }
    
    async getSession(id: string): Promise<any> {
        const key = this.prefix + id;
        const data = await this.redis.get(key);
        return data ? JSON.parse(data) : null;
    }
    
    async removeSession(id: string): Promise<void> {
        const key = this.prefix + id;
        await this.redis.del(key);
    }
    
    async touchSession(id: string): Promise<void> {
        const key = this.prefix + id;
        await this.redis.expire(key, this.ttl);
    }
}

// Use it!
const vault = new SessionVault('redis://localhost:6379');

app.use(async (req, res, next) => {
    const sessionId = req.cookies.sessionId;
    if (sessionId) {
        req.session = await vault.getSession(sessionId);
        await vault.touchSession(sessionId);
    }
    next();
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Stored sessions
- [x] Managed expiry
- [ ] Level up to security!

## Level 3: Security Spells! 🛡️

### Security Guard
```typescript
class SecurityGuard {
    private static readonly MAX_ATTEMPTS = 5;
    private static readonly LOCKOUT_TIME = 15 * 60 * 1000; // 15 minutes
    private attempts: Map<string, number[]> = new Map();
    
    checkAttempts(ip: string): boolean {
        const now = Date.now();
        const attempts = this.attempts.get(ip) || [];
        
        // Remove old attempts
        const recent = attempts.filter(
            time => time > now - SecurityGuard.LOCKOUT_TIME
        );
        
        // Check if locked out
        if (recent.length >= SecurityGuard.MAX_ATTEMPTS) {
            return false;
        }
        
        // Add new attempt
        recent.push(now);
        this.attempts.set(ip, recent);
        return true;
    }
    
    resetAttempts(ip: string): void {
        this.attempts.delete(ip);
    }
}

// Add more security spells!
class SecuritySpells {
    static sanitizeInput(input: string): string {
        return input.replace(/[<>]/g, '');
    }
    
    static generateSecureId(): string {
        return crypto.randomBytes(32).toString('hex');
    }
    
    static validatePassword(password: string): boolean {
        return password.length >= 8 &&
               /[A-Z]/.test(password) &&
               /[a-z]/.test(password) &&
               /[0-9]/.test(password);
    }
}
```

## Mini Games! 🎮

### Game 1: Session Inspector
```typescript
// Create session debugger!
class SessionInspector {
    static inspect(session: any): void {
        console.log('🔍 Session Contents:');
        console.log('Created:', new Date(session.created));
        console.log('Last Access:', new Date(session.lastAccess));
        console.log('Data:', session.data);
        
        // Check security
        console.log('🛡️ Security Check:');
        console.log('HTTP Only:', session.cookie.httpOnly ? '✅' : '❌');
        console.log('Secure:', session.cookie.secure ? '✅' : '❌');
        console.log('SameSite:', session.cookie.sameSite || '❌');
    }
}

// Try it!
const session = {
    created: Date.now(),
    lastAccess: Date.now(),
    data: { wizardName: 'Merlin' },
    cookie: {
        httpOnly: true,
        secure: true,
        sameSite: 'strict'
    }
};

SessionInspector.inspect(session);
```

### Game 2: Attack Simulator
```typescript
// Test your defenses!
class AttackSimulator {
    static async testCSRF(url: string): Promise<boolean> {
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'Origin': 'https://evil-site.com'
            }
        });
        return response.status === 403;
    }
    
    static async testXSS(input: string): boolean {
        return !/<script>|javascript:/i.test(input);
    }
    
    static async testInjection(input: string): boolean {
        return !/[;()]|'|"|\$|\\/.test(input);
    }
}

// Run your tests!
async function runSecurityTests() {
    console.log('🛡️ Running security tests...');
    
    console.log('Testing CSRF protection:',
        await AttackSimulator.testCSRF('/api/data')
            ? '✅' : '❌'
    );
    
    console.log('Testing XSS protection:',
        await AttackSimulator.testXSS('<script>alert("boom")</script>')
            ? '✅' : '❌'
    );
    
    console.log('Testing injection protection:',
        await AttackSimulator.testInjection('DROP TABLE users;')
            ? '✅' : '❌'
    );
}
```

---
🎉 **POWER-UPS** 🎉

### Security Helper
```typescript
// Make security easier!
class SecurityHelper {
    static readonly SECURE_HEADERS = {
        'Strict-Transport-Security': 'max-age=31536000',
        'X-Frame-Options': 'DENY',
        'X-Content-Type-Options': 'nosniff',
        'X-XSS-Protection': '1; mode=block',
        'Content-Security-Policy': "default-src 'self'"
    };
    
    static addSecureHeaders(res: Response): void {
        Object.entries(this.SECURE_HEADERS)
            .forEach(([header, value]) => {
                res.setHeader(header, value);
            });
    }
    
    static secureCookie(name: string, value: string): string {
        return `${name}=${value}; HttpOnly; Secure; SameSite=Strict`;
    }
}

// Use it!
app.use((req, res, next) => {
    SecurityHelper.addSecureHeaders(res);
    next();
});
```

## Practice Time! 🏃‍♂️

### Challenge 1: Session Store
```typescript
// Create store that:
// 1. Uses encryption
// 2. Handles concurrent access
// 3. Implements backup
// 4. Rotates keys

interface SecureStore {
    // Your code here!
}
```

### Challenge 2: Security Monitor
```typescript
// Create monitor that:
// 1. Tracks suspicious activity
// 2. Blocks attackers
// 3. Logs security events
// 4. Sends alerts

interface SecurityMonitor {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Managed sessions
- [x] Secured storage
- [x] Added protection
- [ ] Ready for more!

## Remember! 🧠
- Always use HTTPS
- Set secure cookies
- Validate all input
- Monitor for attacks
- Keep sessions short
- Encrypt sensitive data

---
Need a Break? 🎮
- Test your security!
- Check your sessions!
- Run attack tests!
- Come back vigilant!

You're a security master now! 🛡️