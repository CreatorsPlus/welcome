# Weekend Project Part 2: Let's Add Blog Features! 📝

## 🎯 Today's Goals
- Create blog post features
- Add comments system
- Set up file uploads
- Make our API shine!

> Remember: Take breaks whenever you need them! This is a lot, but we'll do it step by step. 🌟

## 📝 Step 1: Blog Post Features (60 mins)

### 1.1 Create Post Types
First, open your terminal in the project folder and create a new file:
```bash
# In your terminal:
mkdir src/types
touch src/types/post.ts
```

Now open `src/types/post.ts` in your editor and add:
```typescript
// In src/types/post.ts
export interface Post {
    id: string;
    title: string;
    content: string;
    authorId: string;
    createdAt: Date;
    updatedAt: Date;
    imageUrl?: string;
}

export interface CreatePostDto {
    title: string;
    content: string;
    image?: Express.Multer.File;
}
```

🎉 **Nice work!** Let's set up the controller next.

### 1.2 Create Post Controller
```bash
# In your terminal:
mkdir src/controllers
touch src/controllers/post.ts
```

Now in `src/controllers/post.ts`:
```typescript
// In src/controllers/post.ts
import { Request, Response } from 'express';
import { Post, CreatePostDto } from '../types/post';

export class PostController {
    // We'll store posts in memory for now
    private posts: Post[] = [];

    async createPost(req: Request, res: Response) {
        try {
            const userId = req.user?.id; // We'll add auth middleware later
            const { title, content } = req.body;
            const imageUrl = req.file?.path; // We'll add file upload later

            const post: Post = {
                id: Date.now().toString(),
                title,
                content,
                authorId: userId || 'anonymous',
                createdAt: new Date(),
                updatedAt: new Date(),
                imageUrl
            };

            this.posts.push(post);

            // Handle both HTML and JSON responses
            if (req.accepts('html')) {
                res.redirect(`/posts/${post.id}`);
            } else {
                res.status(201).json({
                    success: true,
                    data: post
                });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    async getPosts(req: Request, res: Response) {
        try {
            // Handle both HTML and JSON responses
            if (req.accepts('html')) {
                res.render('posts/index', { 
                    posts: this.posts,
                    user: req.user
                });
            } else {
                res.json({
                    success: true,
                    data: this.posts
                });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    async getPost(req: Request, res: Response) {
        try {
            const post = this.posts.find(p => p.id === req.params.id);
            
            if (!post) {
                throw new Error('Post not found');
            }

            if (req.accepts('html')) {
                res.render('posts/show', { 
                    post,
                    user: req.user
                });
            } else {
                res.json({
                    success: true,
                    data: post
                });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    private handleError(error: any, req: Request, res: Response) {
        console.error('Post Error:', error);
        const message = error.message || 'Internal server error';
        
        if (req.accepts('html')) {
            res.status(400).render('error', { message });
        } else {
            res.status(400).json({
                success: false,
                error: message
            });
        }
    }
}
```

✅ **CHECKPOINT!** 
- Take a 5-minute break
- Stretch a bit
- Grab some water
- Ready for templates? Let's go!

### 1.3 Create Post Templates
```bash
# In your terminal:
mkdir -p src/views/posts
touch src/views/posts/index.ejs
touch src/views/posts/show.ejs
touch src/views/posts/create.ejs
```

Now let's create each template. First, `src/views/posts/create.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="post-form">
    <h2>Create New Post</h2>
    <form action="/posts" method="POST" enctype="multipart/form-data">
        <div>
            <label>Title:</label>
            <input type="text" name="title" required>
        </div>
        <div>
            <label>Content:</label>
            <textarea name="content" required></textarea>
        </div>
        <div>
            <label>Image (optional):</label>
            <input type="file" name="image" accept="image/*">
        </div>
        <button type="submit">Create Post</button>
    </form>
</div>

<%- include('../partials/footer') %>
```

Next, `src/views/posts/index.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="posts-list">
    <h2>Blog Posts</h2>
    
    <% if (user) { %>
        <a href="/posts/new" class="create-post-btn">Create New Post</a>
    <% } %>
    
    <div class="posts-grid">
        <% posts.forEach(post => { %>
            <div class="post-card">
                <% if (post.imageUrl) { %>
                    <img src="<%= post.imageUrl %>" alt="Post image">
                <% } %>
                <h3><a href="/posts/<%= post.id %>"><%= post.title %></a></h3>
                <p><%= post.content.substring(0, 100) %>...</p>
                <div class="post-meta">
                    Posted on: <%= post.createdAt.toLocaleDateString() %>
                </div>
            </div>
        <% }); %>
    </div>
</div>

<%- include('../partials/footer') %>
```

Finally, `src/views/posts/show.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="single-post">
    <h1><%= post.title %></h1>
    
    <% if (post.imageUrl) { %>
        <div class="post-image">
            <img src="<%= post.imageUrl %>" alt="Post image">
        </div>
    <% } %>
    
    <div class="post-content">
        <%= post.content %>
    </div>
    
    <div class="post-meta">
        Posted on: <%= post.createdAt.toLocaleDateString() %>
    </div>
    
    <% if (user && user.id === post.authorId) { %>
        <div class="post-actions">
            <a href="/posts/<%= post.id %>/edit" class="edit-btn">Edit Post</a>
            <form action="/posts/<%= post.id %>/delete" method="POST" class="delete-form">
                <button type="submit" class="delete-btn">Delete Post</button>
            </form>
        </div>
    <% } %>
</div>

<%- include('../partials/footer') %>
```

✅ **CHECKPOINT!** 
- Time for another break!
- Check all your files are created
- Make sure indentation is correct
- Ready for styling? Let's make it pretty!

### 1.4 Add Post Styles
Open `src/public/css/style.css` and add:
```css
/* Post Grid */
.posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 2rem;
    padding: 2rem;
}

.post-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.2s;
}

.post-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.post-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
}

.post-card h3 {
    padding: 1rem;
    margin: 0;
}

.post-card p {
    padding: 0 1rem;
    color: #666;
}

.post-meta {
    padding: 1rem;
    color: #888;
    font-size: 0.9rem;
}

/* Single Post */
.single-post {
    max-width: 800px;
    margin: 2rem auto;
    padding: 0 1rem;
}

.post-image img {
    width: 100%;
    max-height: 400px;
    object-fit: cover;
    border-radius: 8px;
}

.post-content {
    line-height: 1.6;
    margin: 2rem 0;
}

.post-actions {
    margin-top: 2rem;
    display: flex;
    gap: 1rem;
}

.edit-btn, .delete-btn {
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
}

.edit-btn {
    background: #4CAF50;
    color: white;
    text-decoration: none;
}

.delete-btn {
    background: #f44336;
    color: white;
    border: none;
}
```

🎉 **Amazing progress!** Let's take a longer break before moving to comments.

## 💭 Step 2: Comments System (45 mins) 

### 2.1 Create Comment Types
```bash
# In your terminal:
touch src/types/comment.ts
```

In `src/types/comment.ts`:
```typescript
export interface Comment {
    id: string;
    content: string;
    authorId: string;
    postId: string;
    createdAt: Date;
}
```


### 2.2 Create Comment Controller
```bash
# In your terminal:
touch src/controllers/comment.ts
```

Open `src/controllers/comment.ts` in your editor:
```typescript
// In src/controllers/comment.ts
import { Request, Response } from 'express';
import { Comment } from '../types/comment';

export class CommentController {
    private comments: Comment[] = [];

    async createComment(req: Request, res: Response) {
        try {
            const { content } = req.body;
            const postId = req.params.postId;
            const userId = req.user?.id || 'anonymous';

            const comment: Comment = {
                id: Date.now().toString(),
                content,
                authorId: userId,
                postId,
                createdAt: new Date()
            };

            this.comments.push(comment);

            // Handle different response types
            if (req.accepts('html')) {
                res.redirect(`/posts/${postId}#comments`);
            } else {
                res.status(201).json({
                    success: true,
                    data: comment
                });
            }
        } catch (error) {
            this.handleError(error, req, res);
        }
    }

    getCommentsForPost(postId: string): Comment[] {
        return this.comments.filter(c => c.postId === postId);
    }

    private handleError(error: any, req: Request, res: Response) {
        const message = error.message || 'Error processing comment';
        
        if (req.accepts('html')) {
            res.status(400).render('error', { message });
        } else {
            res.status(400).json({
                success: false,
                error: message
            });
        }
    }
}
```

### 2.3 Update Post Show Template
Open `src/views/posts/show.ejs` and add below the post content:
```ejs
<!-- Add this after the post-content div -->
<div class="comments-section" id="comments">
    <h3>Comments</h3>
    
    <% if (user) { %>
        <form action="/posts/<%= post.id %>/comments" method="POST" class="comment-form">
            <textarea 
                name="content" 
                placeholder="Write your comment..."
                required
            ></textarea>
            <button type="submit">Add Comment</button>
        </form>
    <% } else { %>
        <p><a href="/login">Login to comment</a></p>
    <% } %>

    <div class="comments-list">
        <% comments.forEach(comment => { %>
            <div class="comment">
                <div class="comment-meta">
                    <span class="comment-author">
                        <%= comment.authorId === 'anonymous' ? 'Anonymous' : comment.authorId %>
                    </span>
                    <span class="comment-date">
                        <%= comment.createdAt.toLocaleDateString() %>
                    </span>
                </div>
                <div class="comment-content">
                    <%= comment.content %>
                </div>
            </div>
        <% }); %>
    </div>
</div>
```

### 2.4 Add Comment Styles
Add to your `src/public/css/style.css`:
```css
/* Comments Section */
.comments-section {
    margin-top: 3rem;
    border-top: 1px solid #ddd;
    padding-top: 2rem;
}

.comment-form {
    margin-bottom: 2rem;
}

.comment-form textarea {
    width: 100%;
    min-height: 100px;
    padding: 0.5rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    resize: vertical;
}

.comment-form button {
    background: #4CAF50;
    color: white;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.comments-list {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.comment {
    background: #f9f9f9;
    padding: 1rem;
    border-radius: 8px;
}

.comment-meta {
    display: flex;
    justify-content: space-between;
    color: #666;
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
}

.comment-content {
    line-height: 1.4;
}
```

✅ **CHECKPOINT!** 
- Take a break - you've earned it!
- Test commenting functionality
- Check the styling
- Ready for file uploads? Let's go!

## 📁 Step 3: File Uploads (30 mins)

### 3.1 Set Up Multer
```bash
# In your terminal:
npm install multer @types/multer
mkdir uploads  # For storing uploaded files
touch src/middleware/upload.ts
```

Create the upload middleware in `src/middleware/upload.ts`:
```typescript
// In src/middleware/upload.ts
import multer from 'multer';
import path from 'path';

// Configure storage
const storage = multer.diskStorage({
    destination: (req, file, cb) => {
        cb(null, 'uploads/');
    },
    filename: (req, file, cb) => {
        const uniqueSuffix = Date.now() + '-' + Math.round(Math.random() * 1E9);
        cb(null, file.fieldname + '-' + uniqueSuffix + path.extname(file.originalname));
    }
});

// File filter
const fileFilter = (req: Express.Request, file: Express.Multer.File, cb: multer.FileFilterCallback) => {
    const allowedTypes = ['image/jpeg', 'image/png', 'image/gif'];
    
    if (allowedTypes.includes(file.mimetype)) {
        cb(null, true);
    } else {
        cb(new Error('Invalid file type. Only JPEG, PNG and GIF allowed.'));
    }
};

// Create upload middleware
export const upload = multer({ 
    storage,
    fileFilter,
    limits: {
        fileSize: 5 * 1024 * 1024 // 5MB limit
    }
});
```

### 3.2 Update Post Routes
Open `src/routes/post.ts` and update the create post route:
```typescript
// In src/routes/post.ts
import { upload } from '../middleware/upload';

// Update the create post route to use upload
router.post('/', 
    upload.single('image'),  // 'image' matches the form field name
    postController.createPost.bind(postController)
);
```

### 3.3 Serve Static Files
Update your main `app.ts` to serve uploaded files:
```typescript
// In src/app.ts
app.use('/uploads', express.static('uploads'));
```

✅ **CHECKPOINT!** 
- Test file uploads
- Check if images display correctly
- Take a quick break
- Ready for the final step? Let's do it!

## 📚 Step 4: API Documentation 💫 (30 mins)

### 4.1 Create API Documentation Page
```bash
# In your terminal:
mkdir src/views/api
touch src/views/api/docs.ejs
```

Create the documentation template in `src/views/api/docs.ejs`:
```ejs
<%- include('../partials/header') %>

<div class="api-docs">
    <h1>API Documentation</h1>
    
    <section class="endpoint-group">
        <h2>Authentication</h2>
        
        <div class="endpoint">
            <h3>Register User</h3>
            <pre><code>POST /api/auth/register</code></pre>
            <div class="example">
                <strong>Request Body:</strong>
<pre><code>{
  "username": "string",
  "email": "string",
  "password": "string"
}</code></pre>
            </div>
        </div>

        <div class="endpoint">
            <h3>Login</h3>
            <pre><code>POST /api/auth/login</code></pre>
            <div class="example">
                <strong>Request Body:</strong>
<pre><code>{
  "email": "string",
  "password": "string"
}</code></pre>
            </div>
        </div>
    </section>

    <section class="endpoint-group">
        <h2>Posts</h2>
        
        <div class="endpoint">
            <h3>Get All Posts</h3>
            <pre><code>GET /api/posts</code></pre>
        </div>

        <div class="endpoint">
            <h3>Create Post</h3>
            <pre><code>POST /api/posts</code></pre>
            <div class="example">
                <strong>Request Body (multipart/form-data):</strong>
<pre><code>{
  "title": "string",
  "content": "string",
  "image": "file (optional)"
}</code></pre>
            </div>
        </div>
    </section>
</div>

<%- include('../partials/footer') %>
```

### 4.2 Add Documentation Styles
Add to your `src/public/css/style.css`:
```css
/* API Documentation */
.api-docs {
    max-width: 900px;
    margin: 2rem auto;
    padding: 0 1rem;
}

.endpoint-group {
    margin: 3rem 0;
}

.endpoint {
    background: #f5f5f5;
    padding: 1.5rem;
    border-radius: 8px;
    margin: 1.5rem 0;
}

.endpoint h3 {
    margin: 0 0 1rem 0;
    color: #333;
}

.endpoint pre {
    background: #2d2d2d;
    color: #fff;
    padding: 1rem;
    border-radius: 4px;
    overflow-x: auto;
}

.example {
    margin-top: 1rem;
}

.example strong {
    display: block;
    margin-bottom: 0.5rem;
}
```

✅ **FINAL CHECKPOINT!** 
- Test all features together
- Check for any styling issues
- Make sure documentation is clear
- You did it! 🎉

## 🎉 Congratulations!

You've built a full-featured blog platform with:
- User authentication
- Blog posts with images
- Comments system
- API documentation

Next steps you could take:
1. Add search functionality
2. Implement categories/tags
3. Add user profiles
4. Add social sharing

Remember:
- Keep your code organized
- Commit regularly
- Test thoroughly
- Have fun building! 🚀