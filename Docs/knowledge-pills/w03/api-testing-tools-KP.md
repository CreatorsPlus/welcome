# API Testing: Try Your Spells! 🧪
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Test your API spells
- Use magic tools
- Debug enchantments
- Share test results!

## Quick Win! ⚡
Try this testing spell:
```typescript
import request from 'supertest';

// Test your first endpoint!
const response = await request(app)
    .get('/spells')
    .expect(200);

console.log('✨ Test passed! Found spells:', 
    response.body.length
);
```

## Level 1: Testing Tools! 🔧

### Postman Magic
```typescript
// Create a Postman collection!
{
    "info": {
        "name": "Magic API Tests ✨",
        "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
    },
    "item": [
        {
            "name": "Get All Spells 📚",
            "request": {
                "method": "GET",
                "url": "{{baseUrl}}/spells",
                "header": [
                    {
                        "key": "Authorization",
                        "value": "Bearer {{magicToken}}"
                    }
                ]
            },
            "test": {
                "exec": [
                    "pm.test('Status is 200', () => {",
                    "    pm.response.to.have.status(200);",
                    "});",
                    "",
                    "pm.test('Has spells array', () => {",
                    "    const response = pm.response.json();",
                    "    pm.expect(response.spells).to.be.an('array');",
                    "});"
                ]
            }
        }
    ]
}
```

### Thunder Client
```typescript
// Create Thunder Client test!
{
    "name": "Test Spell Casting ✨",
    "url": "{{baseUrl}}/cast/lumos",
    "method": "POST",
    "headers": {
        "Content-Type": "application/json"
    },
    "body": {
        "power": 50,
        "target": "wand"
    },
    "tests": [
        {
            "name": "Should cast successfully",
            "assertions": [
                "status == 200",
                "body.success == true",
                "body.message contains 'cast successfully'"
            ]
        }
    ]
}
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Used Postman
- [x] Used Thunder Client
- [ ] Ready for automation!

## Level 2: Automated Testing! 🤖

### Test Runner
```typescript
class SpellTester {
    private app: Express;
    private token: string;

    constructor(app: Express) {
        this.app = app;
    }

    async login(): Promise<void> {
        const response = await request(this.app)
            .post('/login')
            .send({
                username: 'wizard',
                password: 'magic123'
            });

        this.token = response.body.token;
    }

    async testSpell(spell: {
        name: string;
        power: number;
    }): Promise<void> {
        await request(this.app)
            .post(`/cast/${spell.name}`)
            .set('Authorization', `Bearer ${this.token}`)
            .send({ power: spell.power })
            .expect(200)
            .expect((res) => {
                expect(res.body.success).toBe(true);
                expect(res.body.spell).toBe(spell.name);
            });
    }

    async runAllTests(): Promise<void> {
        await this.login();
        
        // Test basic spells
        await this.testSpell({
            name: 'lumos',
            power: 10
        });
        
        // Test powerful spells
        await this.testSpell({
            name: 'patronus',
            power: 100
        });
        
        console.log('✨ All spells tested successfully!');
    }
}

// Use it!
const tester = new SpellTester(app);
await tester.runAllTests();
```

### Test Scenarios
```typescript
// Create scenario runner!
class TestScenarios {
    static readonly scenarios = {
        'Cast Basic Spell': async (test: SpellTester) => {
            await test.login();
            await test.testSpell({
                name: 'lumos',
                power: 10
            });
        },
        
        'Cast Without Login': async (test: SpellTester) => {
            try {
                await test.testSpell({
                    name: 'lumos',
                    power: 10
                });
                throw new Error('Should have failed! 🌋');
            } catch (error) {
                console.log('✅ Correctly failed without login!');
            }
        },
        
        'Cast Powerful Spell': async (test: SpellTester) => {
            await test.login();
            await test.testSpell({
                name: 'patronus',
                power: 100
            });
        }
    };
    
    static async runAll(app: Express): Promise<void> {
        const tester = new SpellTester(app);
        
        for (const [name, scenario] of Object.entries(this.scenarios)) {
            console.log(`🧪 Running scenario: ${name}`);
            await scenario(tester);
            console.log('✨ Scenario passed!\n');
        }
    }
}
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Created test runner
- [x] Added scenarios
- [ ] Level up to reporting!

## Level 3: Test Reports! 📊

### Report Generator
```typescript
class SpellTestReporter {
    private results: {
        passed: string[];
        failed: string[];
        duration: number;
    } = {
        passed: [],
        failed: [],
        duration: 0
    };
    
    async runTest(
        name: string,
        test: () => Promise<void>
    ): Promise<void> {
        const start = Date.now();
        
        try {
            await test();
            this.results.passed.push(name);
            console.log(`✅ ${name}`);
        } catch (error) {
            this.results.failed.push(name);
            console.log(`❌ ${name}: ${error.message}`);
        }
        
        this.results.duration += Date.now() - start;
    }
    
    generateReport(): string {
        return `
            🎭 Spell Test Report
            ===================
            
            ✨ Results:
            - Passed: ${this.results.passed.length}
            - Failed: ${this.results.failed.length}
            - Duration: ${this.results.duration}ms
            
            🎯 Passed Tests:
            ${this.results.passed.map(test => 
                `- ✅ ${test}`
            ).join('\n')}
            
            💥 Failed Tests:
            ${this.results.failed.map(test => 
                `- ❌ ${test}`
            ).join('\n')}
        `;
    }
}
```

## Mini Games! 🎮

### Game 1: Test Builder
```typescript
// Create dynamic tests!
class TestBuilder {
    private tests: Map<string, () => Promise<void>> = new Map();
    
    addTest(name: string, test: () => Promise<void>): this {
        this.tests.set(name, test);
        return this;
    }
    
    async runAll(): Promise<void> {
        for (const [name, test] of this.tests) {
            console.log(`🧪 Running: ${name}`);
            await test();
        }
    }
}

// Use it!
const builder = new TestBuilder()
    .addTest('Basic Spell', async () => {
        // Your test here
    })
    .addTest('Advanced Spell', async () => {
        // Your test here
    });

await builder.runAll();
```

### Game 2: Response Checker
```typescript
// Create response validator!
class ResponseChecker {
    static check(response: any, rules: {
        status?: number;
        body?: Record<string, any>;
        headers?: Record<string, string>;
    }): boolean {
        // Check status
        if (rules.status && 
            response.status !== rules.status) {
            throw new Error(
                `Expected status ${rules.status}, ` +
                `got ${response.status}`
            );
        }
        
        // Check body
        if (rules.body) {
            for (const [key, value] of Object.entries(rules.body)) {
                if (response.body[key] !== value) {
                    throw new Error(
                        `Expected body.${key} to be ${value}, ` +
                        `got ${response.body[key]}`
                    );
                }
            }
        }
        
        // Check headers
        if (rules.headers) {
            for (const [key, value] of Object.entries(rules.headers)) {
                if (response.headers[key] !== value) {
                    throw new Error(
                        `Expected header ${key} to be ${value}, ` +
                        `got ${response.headers[key]}`
                    );
                }
            }
        }
        
        return true;
    }
}

// Use it!
const response = await request(app).get('/spells');
ResponseChecker.check(response, {
    status: 200,
    body: {
        success: true,
        total: 5
    },
    headers: {
        'content-type': 'application/json'
    }
});
```

---
🎉 **POWER-UPS** 🎉

### Quick Test Helper
```typescript
// Make testing easier!
class TestHelper {
    static async retry<T>(
        action: () => Promise<T>,
        maxAttempts = 3,
        delay = 1000
    ): Promise<T> {
        let lastError: Error;
        
        for (let i = 0; i < maxAttempts; i++) {
            try {
                return await action();
            } catch (error) {
                lastError = error;
                await new Promise(r => 
                    setTimeout(r, delay)
                );
            }
        }
        
        throw lastError!;
    }
    
    static async cleanup(
        actions: (() => Promise<void>)[]
    ): Promise<void> {
        for (const action of actions) {
            try {
                await action();
            } catch (error) {
                console.error('Cleanup failed:', error);
            }
        }
    }
}

// Use it!
await TestHelper.retry(async () => {
    const response = await request(app)
        .get('/spells');
    expect(response.status).toBe(200);
});
```

## Practice Time! 🏃‍♂️

### Challenge 1: Test Suite
```typescript
// Create suite that:
// 1. Runs all tests
// 2. Generates reports
// 3. Handles cleanup
// 4. Manages state

interface TestSuite {
    // Your code here!
}
```

### Challenge 2: API Monitor
```typescript
// Create monitor that:
// 1. Checks endpoints
// 2. Measures response time
// 3. Reports errors
// 4. Tracks uptime

interface APIMonitor {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Created tests
- [x] Generated reports
- [x] Added helpers
- [ ] Ready for more!

## Remember! 🧠
- Test thoroughly
- Generate reports
- Handle failures
- Clean up after tests
- Keep tests focused

---
Need a Break? 🎮
- Run some tests!
- Check results!
- Fix failures!
- Come back stronger!

You're a testing wizard now! 🧪