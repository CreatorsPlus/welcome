# API Docs: Write Your Spellbook! 📚
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Document your API spells
- Create magic guides
- Test your enchantments
- Share your wisdom!

## Quick Win! ⚡
Try this documentation spell:
```typescript
import swaggerJsdoc from 'swagger-jsdoc';

// Create your first spellbook!
const spellbook = {
    openapi: '3.0.0',
    info: {
        title: 'Magic API',
        version: '1.0.0',
        description: 'A collection of magical endpoints'
    }
};

// Add your first spell!
/**
 * @swagger
 * /spells:
 *   get:
 *     summary: Get all spells
 *     responses:
 *       200:
 *         description: A list of magical spells
 */
app.get('/spells', (req, res) => {
    res.json([
        { name: 'Lumos', type: 'light' },
        { name: 'Wingardium Leviosa', type: 'levitation' }
    ]);
});
```

## Level 1: Documentation Basics! 📖

### Spell Documentation
```typescript
// Document your magical endpoints!
/**
 * @swagger
 * /cast/{spellName}:
 *   post:
 *     summary: Cast a spell
 *     tags: [Spells]
 *     parameters:
 *       - in: path
 *         name: spellName
 *         required: true
 *         schema:
 *           type: string
 *     responses:
 *       200:
 *         description: Spell cast successfully! ✨
 *       404:
 *         description: Spell not found in spellbook! 📚
 */
app.post('/cast/:spellName', (req, res) => {
    const spell = findSpell(req.params.spellName);
    if (!spell) {
        res.status(404).json({
            message: 'Spell not found in spellbook! 📚'
        });
        return;
    }
    res.json({ message: 'Spell cast successfully! ✨' });
});
```

### Magic Objects
```typescript
/**
 * @swagger
 * components:
 *   schemas:
 *     Spell:
 *       type: object
 *       required:
 *         - name
 *         - type
 *       properties:
 *         name:
 *           type: string
 *           description: The name of the spell ✨
 *         type:
 *           type: string
 *           enum: [light, dark, nature]
 *           description: The type of magic 🌟
 *         power:
 *           type: integer
 *           minimum: 1
 *           maximum: 100
 *           description: Spell power level ⚡
 *     
 *     Wizard:
 *       type: object
 *       required:
 *         - name
 *         - level
 *       properties:
 *         name:
 *           type: string
 *         level:
 *           type: integer
 *         spells:
 *           type: array
 *           items:
 *             $ref: '#/components/schemas/Spell'
 */
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Documented endpoints
- [x] Defined schemas
- [ ] Ready for testing!

## Level 2: Interactive Testing! 🎮

### Test Pages
```typescript
// Create interactive test pages!
import swaggerUi from 'swagger-ui-express';

// Setup your testing ground!
app.use(
    '/spellbook',
    swaggerUi.serve,
    swaggerUi.setup(specs, {
        explorer: true,
        customCss: `
            .swagger-ui .topbar {
                background: linear-gradient(45deg, #4F3BA9, #9B5DE5);
            }
            .swagger-ui .btn.execute {
                background-color: #4F3BA9;
            }
        `,
        customSiteTitle: "Wizard's API Spellbook"
    })
);

// Add test examples!
/**
 * @swagger
 * /learn-spell:
 *   post:
 *     summary: Learn a new spell
 *     requestBody:
 *       required: true
 *       content:
 *         application/json:
 *           schema:
 *             $ref: '#/components/schemas/Spell'
 *           example:
 *             name: Expecto Patronum
 *             type: light
 *             power: 95
 */
```

### Security Documentation
```typescript
/**
 * @swagger
 * components:
 *   securitySchemes:
 *     WizardAuth:
 *       type: http
 *       scheme: bearer
 *       bearerFormat: JWT
 *       description: Use your magic token! 🎫
 * 
 * /secret-spells:
 *   get:
 *     security:
 *       - WizardAuth: []
 *     summary: Get secret spells
 *     responses:
 *       200:
 *         description: Secret spells revealed! 🎭
 *       401:
 *         description: You need a magic token! 🔒
 */
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Added testing UI
- [x] Documented security
- [ ] Level up to examples!

## Level 3: Example Magic! 📝

### Response Examples
```typescript
/**
 * @swagger
 * /spellbook:
 *   get:
 *     summary: Get your spellbook
 *     responses:
 *       200:
 *         description: Your magical collection! 📚
 *         content:
 *           application/json:
 *             example:
 *               spells:
 *                 - name: Lumos
 *                   type: light
 *                   power: 10
 *                 - name: Expecto Patronum
 *                   type: light
 *                   power: 95
 *               totalSpells: 2
 *               maxPower: 95
 */

// Add error examples too!
/**
 * @swagger
 * /cast/{spellName}:
 *   post:
 *     responses:
 *       400:
 *         description: Invalid spell parameters! 🌋
 *         content:
 *           application/json:
 *             example:
 *               error: Invalid spell parameters!
 *               details:
 *                 - power must be between 1 and 100
 *                 - type must be light, dark, or nature
 */
```

## Mini Games! 🎮

### Game 1: Doc Generator
```typescript
// Create a doc generator!
class SpellbookWriter {
    static generatePage(spell: {
        name: string;
        description: string;
        examples: string[];
    }): string {
        return `
            # ${spell.name} ✨
            
            ${spell.description}
            
            ## Examples 📖
            ${spell.examples.map(ex => 
                `- ${ex}`
            ).join('\n')}
            
            ## Try it! 🎮
            \`\`\`bash
            curl -X POST /cast/${spell.name}
            \`\`\`
        `;
    }
}

// Use it!
const page = SpellbookWriter.generatePage({
    name: 'Lumos',
    description: 'Creates magical light!',
    examples: [
        'Light up a dark room',
        'Create a guiding beacon'
    ]
});
```

### Game 2: Test Builder
```typescript
// Create test examples!
class SpellTester {
    static generateTests(spell: {
        name: string;
        params: any;
    }): string[] {
        return [
            `# Test Good Path 🎯`,
            `curl -X POST /cast/${spell.name} \\`,
            `-H "Content-Type: application/json" \\`,
            `-d '${JSON.stringify(spell.params)}'`,
            '',
            `# Test Bad Path 💥`,
            `curl -X POST /cast/${spell.name} \\`,
            `-H "Content-Type: application/json" \\`,
            `-d '{"power": 999}'`  // Invalid power!
        ];
    }
}

// Try it!
const tests = SpellTester.generateTests({
    name: 'Lumos',
    params: {
        power: 50,
        type: 'light'
    }
});
```

---
🎉 **POWER-UPS** 🎉

### Quick Doc Helper
```typescript
// Make docs easier!
class DocHelper {
    static endpoint(path: string, {
        method = 'GET',
        summary,
        params = [],
        responses = {}
    }: any): string {
        return `
/**
 * @swagger
 * ${path}:
 *   ${method.toLowerCase()}:
 *     summary: ${summary}
 *     parameters:
 *       ${params.map(p => this.param(p)).join('\n *       ')}
 *     responses:
 *       ${Object.entries(responses).map(([code, desc]) =>
            `${code}:\n *         description: ${desc}`
        ).join('\n *       ')}
 */`;
    }
    
    static param({
        name,
        type = 'string',
        required = false,
        description
    }: any): string {
        return `- in: path
 *         name: ${name}
 *         required: ${required}
 *         schema:
 *           type: ${type}
 *         description: ${description}`;
    }
}

// Use it!
console.log(DocHelper.endpoint('/spell/{name}', {
    method: 'POST',
    summary: 'Cast a spell! ✨',
    params: [{
        name: 'name',
        required: true,
        description: 'The spell to cast'
    }],
    responses: {
        200: 'Spell cast successfully! 🎉',
        404: 'Spell not found! 📚'
    }
}));
```

## Practice Time! 🏃‍♂️

### Challenge 1: API Guide
```typescript
// Create a guide that:
// 1. Lists all endpoints
// 2. Shows examples
// 3. Provides test cases
// 4. Explains errors

interface APIGuide {
    // Your code here!
}
```

### Challenge 2: Doc Generator
```typescript
// Create generator that:
// 1. Reads route files
// 2. Extracts comments
// 3. Generates docs
// 4. Creates examples

interface DocGenerator {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Created docs
- [x] Added examples
- [x] Made tests
- [ ] Ready for more!

## Remember! 🧠
- Document all endpoints
- Include examples
- Test your docs
- Keep docs updated
- Make it fun!

---
Need a Break? 🎮
- Write some docs!
- Add examples!
- Test endpoints!
- Come back inspired!

You're a documentation wizard now! 📚