# Form Powers: Validation Magic! 📝
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Process forms safely
- Validate like a pro
- Handle file uploads
- Protect against evil spells!

## Quick Win! ⚡
Try this magical form handler:
```typescript
import { z } from 'zod';

// Define your form shape!
const formSpell = z.object({
    username: z.string().min(3),
    email: z.string().email(),
    power: z.number().min(1).max(100)
});

// Use it!
app.post('/register-wizard', async (req, res) => {
    try {
        const wizard = formSpell.parse(req.body);
        console.log('New wizard:', wizard);
        res.json({ message: '✨ Wizard registered!' });
    } catch (error) {
        res.status(400).json({ error: 'Invalid spell components! 🌋' });
    }
});
```

## Level 1: Form Safety! 🛡️

### Validation Shield
```typescript
// Create your validation shield!
class FormGuardian {
    static validateField(
        value: string,
        rules: {
            required?: boolean;
            minLength?: number;
            pattern?: RegExp;
        }
    ): string[] {
        const errors: string[] = [];
        
        if (rules.required && !value) {
            errors.push('Field is required! 📜');
        }
        
        if (rules.minLength && value.length < rules.minLength) {
            errors.push(`Need at least ${rules.minLength} characters! 📏`);
        }
        
        if (rules.pattern && !rules.pattern.test(value)) {
            errors.push('Invalid format! 🎭');
        }
        
        return errors;
    }
}

// Try it!
const usernameErrors = FormGuardian.validateField('Oz', {
    required: true,
    minLength: 3,
    pattern: /^[a-zA-Z0-9]+$/
});

console.log(usernameErrors);  // ['Need at least 3 characters! 📏']
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Added validation
- [x] Checked fields
- [ ] Ready for more magic!

## Level 2: File Upload Powers! 📎

### Upload Handler
```typescript
import multer from 'multer';

// Create your upload spell!
class UploadMaster {
    private storage: multer.StorageEngine;
    
    constructor(private spellbook: {
        maxSize: number;
        allowedTypes: string[];
        destination: string;
    }) {
        this.storage = multer.diskStorage({
            destination: this.spellbook.destination,
            filename: (req, file, cb) => {
                const magicName = `${Date.now()}-${file.originalname}`;
                cb(null, magicName);
            }
        });
    }
    
    cast() {
        return multer({
            storage: this.storage,
            limits: { fileSize: this.spellbook.maxSize },
            fileFilter: (req, file, cb) => {
                if (this.spellbook.allowedTypes.includes(file.mimetype)) {
                    cb(null, true);
                } else {
                    cb(null, false);
                }
            }
        });
    }
}

// Use it!
const imageUploader = new UploadMaster({
    maxSize: 5 * 1024 * 1024,  // 5MB
    allowedTypes: ['image/jpeg', 'image/png'],
    destination: './uploads'
}).cast();

app.post('/upload-scroll', imageUploader.single('scroll'), (req, res) => {
    if (!req.file) {
        return res.status(400).json({ error: 'No scroll found! 📜' });
    }
    res.json({ message: 'Scroll stored safely! ✨' });
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Handle uploads
- [x] Validate files
- [ ] Level up to full forms!

## Level 3: Complete Form Magic! 🎭

### Form Processor
```typescript
interface FormField {
    name: string;
    type: 'text' | 'email' | 'file';
    required?: boolean;
    validation?: {
        minLength?: number;
        pattern?: RegExp;
        message?: string;
    };
}

class FormWizard {
    constructor(private fields: FormField[]) {}
    
    async process(req: Request): Promise<{
        valid: boolean;
        data?: any;
        errors?: Record<string, string[]>;
    }> {
        const errors: Record<string, string[]> = {};
        const data: Record<string, any> = {};
        
        // Check each field
        for (const field of this.fields) {
            const value = req.body[field.name];
            const fieldErrors = this.validateField(field, value);
            
            if (fieldErrors.length > 0) {
                errors[field.name] = fieldErrors;
            } else {
                data[field.name] = value;
            }
        }
        
        return {
            valid: Object.keys(errors).length === 0,
            data: Object.keys(errors).length === 0 ? data : undefined,
            errors: Object.keys(errors).length > 0 ? errors : undefined
        };
    }
    
    private validateField(field: FormField, value: any): string[] {
        const errors: string[] = [];
        
        if (field.required && !value) {
            errors.push(`${field.name} is required! 📜`);
        }
        
        if (field.validation) {
            if (field.validation.minLength && value.length < field.validation.minLength) {
                errors.push(
                    field.validation.message || 
                    `Minimum length is ${field.validation.minLength}! 📏`
                );
            }
            
            if (field.validation.pattern && !field.validation.pattern.test(value)) {
                errors.push(
                    field.validation.message || 
                    `Invalid format! 🎭`
                );
            }
        }
        
        return errors;
    }
}

// Use it!
const registrationForm = new FormWizard([
    {
        name: 'username',
        type: 'text',
        required: true,
        validation: {
            minLength: 3,
            pattern: /^[a-zA-Z0-9]+$/,
            message: 'Username must be alphanumeric!'
        }
    },
    {
        name: 'email',
        type: 'email',
        required: true,
        validation: {
            pattern: /^[^\s@]+@[^\s@]+\.[^\s@]+$/,
            message: 'Invalid email format!'
        }
    }
]);

app.post('/register', async (req, res) => {
    const result = await registrationForm.process(req);
    
    if (!result.valid) {
        return res.status(400).json({ errors: result.errors });
    }
    
    // Process valid data!
    res.json({ message: 'Registration complete! ✨', data: result.data });
});
```

## Mini Games! 🎮

### Game 1: Field Validator
```typescript
// Create a field validator!
class FieldChecker {
    static email(value: string): boolean {
        return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value);
    }
    
    static password(value: string): boolean {
        return /^(?=.*[A-Z])(?=.*[a-z])(?=.*[0-9]).{8,}$/.test(value);
    }
    
    static username(value: string): boolean {
        return /^[a-zA-Z0-9_]{3,20}$/.test(value);
    }
}

// Try it!
console.log(FieldChecker.email('wizard@magic.com'));  // true
console.log(FieldChecker.password('Abcd123!'));      // true
console.log(FieldChecker.username('magic_user_123')); // true
```

### Game 2: Error Collector
```typescript
// Build an error collector!
class ErrorCollector {
    private errors: Map<string, string[]> = new Map();
    
    add(field: string, error: string) {
        const fieldErrors = this.errors.get(field) || [];
        fieldErrors.push(error);
        this.errors.set(field, fieldErrors);
    }
    
    hasErrors(): boolean {
        return this.errors.size > 0;
    }
    
    getErrors(): Record<string, string[]> {
        return Object.fromEntries(this.errors);
    }
}

// Use it!
const collector = new ErrorCollector();
collector.add('username', 'Too short! 📏');
collector.add('email', 'Invalid format! 📧');
console.log(collector.getErrors());
```

---
🎉 **POWER-UPS** 🎉

### Form Helper
```typescript
// Make form handling easier!
class FormHelper {
    static async process<T>(
        schema: z.ZodSchema<T>,
        data: unknown
    ): Promise<[T | null, string[]]> {
        try {
            const validated = await schema.parseAsync(data);
            return [validated, []];
        } catch (error) {
            if (error instanceof z.ZodError) {
                return [null, error.errors.map(e => e.message)];
            }
            return [null, ['Processing failed! 🌋']];
        }
    }
}

// Use it!
const userSchema = z.object({
    name: z.string(),
    email: z.string().email()
});

const [user, errors] = await FormHelper.process(userSchema, req.body);
```

## Practice Time! 🏃‍♂️

### Challenge 1: Multi-step Form
```typescript
// Create a form that:
// 1. Validates each step
// 2. Stores progress
// 3. Allows back/forward
// 4. Shows completion

interface FormStep {
    fields: FormField[];
    validate: (data: any) => Promise<boolean>;
}

// Your code here!
```

### Challenge 2: File Processor
```typescript
// Create processor that:
// 1. Validates file types
// 2. Checks file size
// 3. Renames files
// 4. Generates previews

interface FileProcessor {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Process forms
- [x] Handle files
- [x] Collect errors
- [ ] Ready for more!

## Remember! 🧠
- Always validate input
- Handle files safely
- Collect all errors
- Give clear feedback
- Keep forms simple

---
Need a Break? 🎮
- Test your forms!
- Add validations!
- Handle errors!
- Come back stronger!

You're a form master now! 🧙‍♂️