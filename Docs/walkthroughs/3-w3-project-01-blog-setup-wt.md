# Weekend Project Part 1: Let's Build a Blog! 🎨

## 🎯 Today's Goals
- Set up project structure
- Create user authentication
- Build basic blog post features
- Implement dual-mode responses

## 📦 Step 1: Project Setup (30 mins)
> When your brain starts running wild, come back to this checklist!

### 1.1 Create Project Structure
```bash
mkdir blog-project
cd blog-project
npm init -y
```

### 1.2 Install Core Dependencies
```bash
npm install express ejs bcrypt jsonwebtoken cookie-parser
npm install --save-dev typescript @types/express @types/node ts-node nodemon
npm install --save-dev @types/bcrypt @types/jsonwebtoken @types/cookie-parser
```

### 1.3 Create Basic Structure
```plaintext
blog-project/
├── src/
│   ├── routes/       # URL handlers
│   ├── views/        # EJS templates
│   ├── controllers/  # Business logic
│   ├── middleware/   # Request processors
│   └── public/       # Static files
└── package.json
```

✅ **CHECKPOINT!** 
- Take a 5-minute break
- Make sure your structure looks like above
- All dependencies installed? Check package.json
- Ready? Let's code!

## 🔐 Step 2: Authentication Setup (45 mins)

### 2.1 Create User Types (`src/types/user.ts`)
```typescript
export interface User {
    id: string;
    username: string;
    email: string;
    password: string;
    role: 'admin' | 'author' | 'reader';
}

export interface UserLogin {
    email: string;
    password: string;
}
```

### 2.2 Create Auth Controller (`src/controllers/auth.ts`)
```typescript
import { Request, Response } from 'express';
import bcrypt from 'bcrypt';
import jwt from 'jsonwebtoken';

export class AuthController {
    // For now, store users in memory
    private users: User[] = [];
    private readonly JWT_SECRET = 'your-secret-key';

    async register(req: Request, res: Response) {
        try {
            const { email, password, username } = req.body;
            
            // Check if user exists
            if (this.users.find(u => u.email === email)) {
                throw new Error('User already exists');
            }

            // Hash password
            const hashedPassword = await bcrypt.hash(password, 10);

            // Create user
            const user: User = {
                id: Date.now().toString(),
                email,
                username,
                password: hashedPassword,
                role: 'reader'
            };

            this.users.push(user);

            // Return response based on Accept header
            if (req.accepts('html')) {
                res.redirect('/login');
            } else {
                res.status(201).json({
                    message: 'User created successfully'
                });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    async login(req: Request, res: Response) {
        try {
            const { email, password } = req.body;
            
            // Find user
            const user = this.users.find(u => u.email === email);
            if (!user) {
                throw new Error('User not found');
            }

            // Check password
            const valid = await bcrypt.compare(password, user.password);
            if (!valid) {
                throw new Error('Invalid password');
            }

            // Create token
            const token = jwt.sign(
                { userId: user.id, role: user.role },
                this.JWT_SECRET,
                { expiresIn: '1h' }
            );

            // Set cookie
            res.cookie('auth_token', token, {
                httpOnly: true,
                secure: process.env.NODE_ENV === 'production'
            });

            // Return response based on Accept header
            if (req.accepts('html')) {
                res.redirect('/dashboard');
            } else {
                res.json({ token });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    private handleError(error: any, req: Request, res: Response) {
        const message = error.message || 'Internal server error';
        
        if (req.accepts('html')) {
            res.status(400).render('error', { message });
        } else {
            res.status(400).json({ error: message });
        }
    }
}
```

✅ **CHECKPOINT!** 
- Take another 5-minute break
- Check your code for typos
- Ready for auth routes? Let's go!

## 🛣️ Step 3: Auth Routes (30 mins)

### 3.1 Create Auth Routes (`src/routes/auth.ts`)
```typescript
import { Router } from 'express';
import { AuthController } from '../controllers/auth';

const router = Router();
const authController = new AuthController();

router.post('/register', authController.register.bind(authController));
router.post('/login', authController.login.bind(authController));

export default router;
```

### 3.2 Create Auth Views (`src/views/auth/`)
Create `login.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="auth-form">
    <h2>Login</h2>
    <form action="/auth/login" method="POST">
        <div>
            <label>Email:</label>
            <input type="email" name="email" required>
        </div>
        <div>
            <label>Password:</label>
            <input type="password" name="password" required>
        </div>
        <button type="submit">Login</button>
    </form>
</div>

<%- include('../partials/footer') %>
```

Create `register.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="auth-form">
    <h2>Register</h2>
    <form action="/auth/register" method="POST">
        <div>
            <label>Username:</label>
            <input type="text" name="username" required>
        </div>
        <div>
            <label>Email:</label>
            <input type="email" name="email" required>
        </div>
        <div>
            <label>Password:</label>
            <input type="password" name="password" required>
        </div>
        <button type="submit">Register</button>
    </form>
</div>

<%- include('../partials/footer') %>
```

✅ **CHECKPOINT!** 
- Time for another break!
- Test your routes with Postman
- Try accessing the forms in browser
- Ready for blog posts? That's tomorrow!

## 🎨 Step 4: Basic Styling (15 mins)

### 4.1 Create Basic CSS (`src/public/css/style.css`)
```css
.auth-form {
    max-width: 400px;
    margin: 2rem auto;
    padding: 2rem;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.auth-form input {
    width: 100%;
    padding: 0.5rem;
    margin: 0.5rem 0 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.auth-form button {
    width: 100%;
    padding: 0.75rem;
    background: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.auth-form button:hover {
    background: #45a049;
}
```

✅ **FINAL CHECKPOINT FOR TODAY!** 
- Everything working?
- Take notes of any issues
- Commit your code
- Rest up for tomorrow!

## 🎯 Tomorrow's Preview
- Blog post creation
- File uploads
- Comments system
- API documentation

Remember:
- Take breaks regularly
- Test as you go
- Keep code organized
- Ask questions when stuck!