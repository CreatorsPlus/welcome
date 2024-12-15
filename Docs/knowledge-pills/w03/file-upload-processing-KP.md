# File Upload Powers: Store Those Treasures! 📦
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Handle file uploads
- Process images safely
- Store files properly
- Serve downloads correctly!

## Quick Win! ⚡
Try this magical file handler:
```typescript
import multer from 'multer';

// Create your first uploader! 
const upload = multer({
    dest: 'uploads/',
    limits: { fileSize: 5 * 1024 * 1024 } // 5MB
});

app.post('/upload', upload.single('treasure'), (req, res) => {
    if (!req.file) {
        return res.status(400).json({ error: 'No treasure found! 🏴‍☠️' });
    }
    res.json({ message: 'Treasure stored safely! 🎉' });
});
```

## Level 1: Basic Storage! 📂

### Safe Storage Spell
```typescript
class TreasureVault {
    private storage: multer.StorageEngine;
    
    constructor(private config: {
        path: string;
        maxSize: number;
        allowedTypes: string[];
    }) {
        this.storage = multer.diskStorage({
            destination: (req, file, cb) => {
                cb(null, this.config.path);
            },
            filename: (req, file, cb) => {
                const safeName = this.createSafeName(file.originalname);
                cb(null, safeName);
            }
        });
    }
    
    private createSafeName(original: string): string {
        const timestamp = Date.now();
        const random = Math.random().toString(36).substring(7);
        const ext = path.extname(original);
        return `${timestamp}-${random}${ext}`;
    }
    
    getUploader() {
        return multer({
            storage: this.storage,
            limits: {
                fileSize: this.config.maxSize
            },
            fileFilter: (req, file, cb) => {
                if (this.config.allowedTypes.includes(file.mimetype)) {
                    cb(null, true);
                } else {
                    cb(null, false);
                }
            }
        });
    }
}

// Use it!
const imageVault = new TreasureVault({
    path: './uploads/images',
    maxSize: 5 * 1024 * 1024,
    allowedTypes: ['image/jpeg', 'image/png']
});

app.post('/store-image', 
    imageVault.getUploader().single('image'),
    (req, res) => {
        if (!req.file) {
            return res.status(400).json({
                error: 'Image treasure lost at sea! 🌊'
            });
        }
        res.json({
            message: 'Image safely stored in vault! 🔒',
            path: req.file.path
        });
    }
);
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Handle uploads
- [x] Store files
- [ ] Ready for processing!

## Level 2: Image Processing! 🎨

### Image Processor
```typescript
import sharp from 'sharp';

class ImageWizard {
    static async createThumbnail(
        input: string,
        output: string,
        size: number
    ): Promise<void> {
        await sharp(input)
            .resize(size, size, {
                fit: 'cover',
                position: 'center'
            })
            .jpeg({ quality: 80 })
            .toFile(output);
    }
    
    static async optimize(
        input: string,
        output: string
    ): Promise<void> {
        await sharp(input)
            .jpeg({ quality: 80, progressive: true })
            .toFile(output);
    }
    
    static async watermark(
        input: string,
        output: string,
        text: string
    ): Promise<void> {
        const svg = `
            <svg width="200" height="50">
                <text x="50%" y="50%" 
                      font-family="Arial" 
                      font-size="24" 
                      fill="white" 
                      text-anchor="middle"
                      alignment-baseline="middle"
                      opacity="0.5">
                    ${text}
                </text>
            </svg>
        `;
        
        await sharp(input)
            .composite([{
                input: Buffer.from(svg),
                gravity: 'southeast'
            }])
            .toFile(output);
    }
}

// Use it!
app.post('/process-image', 
    imageVault.getUploader().single('image'),
    async (req, res) => {
        if (!req.file) return res.status(400).json({
            error: 'No image found! 🖼️'
        });
        
        try {
            const thumbnail = `thumbnails/${req.file.filename}`;
            await ImageWizard.createThumbnail(
                req.file.path,
                thumbnail,
                200
            );
            
            res.json({
                message: 'Image processed! ✨',
                original: req.file.path,
                thumbnail
            });
        } catch (error) {
            res.status(500).json({
                error: 'Image processing failed! 🌋'
            });
        }
    }
);
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Process images
- [x] Create thumbnails
- [ ] Level up to streams!

## Level 3: Stream Magic! 🌊

### File Streaming
```typescript
class StreamWizard {
    static createReadStream(
        filepath: string,
        options: {
            start?: number;
            end?: number;
        } = {}
    ): fs.ReadStream {
        return fs.createReadStream(filepath, options);
    }
    
    static pipeStream(
        stream: fs.ReadStream,
        res: Response,
        filename: string
    ): void {
        res.setHeader(
            'Content-Disposition',
            `attachment; filename="${filename}"`
        );
        stream.pipe(res);
    }
    
    static handleErrors(
        stream: fs.ReadStream,
        res: Response
    ): void {
        stream.on('error', (error) => {
            console.error('Stream failed! 🌊', error);
            res.status(500).end();
        });
    }
}

// Use it!
app.get('/download/:filename', (req, res) => {
    const filepath = `uploads/${req.params.filename}`;
    
    if (!fs.existsSync(filepath)) {
        return res.status(404).json({
            error: 'Treasure not found! 🗺️'
        });
    }
    
    const stream = StreamWizard.createReadStream(filepath);
    StreamWizard.handleErrors(stream, res);
    StreamWizard.pipeStream(stream, res, req.params.filename);
});
```

## Mini Games! 🎮

### Game 1: File Type Detector
```typescript
// Create a file type checker!
class TreasureInspector {
    private static mimeTypes = new Map([
        ['ffd8ffe0', 'image/jpeg'],
        ['89504e47', 'image/png'],
        ['25504446', 'application/pdf']
    ]);
    
    static async inspect(
        file: Express.Multer.File
    ): Promise<string | null> {
        const buffer = await fs.promises.readFile(file.path);
        const hex = buffer.toString('hex', 0, 4);
        return this.mimeTypes.get(hex) || null;
    }
}

// Use it!
const type = await TreasureInspector.inspect(req.file);
console.log(`Found treasure type: ${type}`);
```

### Game 2: Progress Tracker
```typescript
// Create an upload progress tracker!
class UploadTracker {
    private progress: Map<string, number> = new Map();
    
    track(id: string, event: {
        bytesReceived: number;
        bytesExpected: number;
    }) {
        const percentage = Math.round(
            (event.bytesReceived / event.bytesExpected) * 100
        );
        this.progress.set(id, percentage);
    }
    
    getProgress(id: string): number {
        return this.progress.get(id) || 0;
    }
}

// Use it!
const tracker = new UploadTracker();
app.post('/upload-large', (req, res) => {
    const id = Date.now().toString();
    
    req.on('data', (chunk) => {
        tracker.track(id, {
            bytesReceived: req.socket.bytesRead,
            bytesExpected: parseInt(req.headers['content-length'] || '0')
        });
    });
});
```

---
🎉 **POWER-UPS** 🎉

### Quick File Helper
```typescript
// Make file handling easier!
class FileHelper {
    static async ensureDir(path: string): Promise<void> {
        await fs.promises.mkdir(path, { recursive: true });
    }
    
    static async moveFile(
        source: string,
        destination: string
    ): Promise<void> {
        await fs.promises.rename(source, destination);
    }
    
    static async deleteFile(path: string): Promise<void> {
        await fs.promises.unlink(path);
    }
}

// Use it!
await FileHelper.ensureDir('uploads/temp');
await FileHelper.moveFile('temp/file.jpg', 'uploads/file.jpg');
```

## Practice Time! 🏃‍♂️

### Challenge 1: Batch Uploader
```typescript
// Create uploader that:
// 1. Handles multiple files
// 2. Processes in parallel
// 3. Shows progress
// 4. Handles errors

interface BatchUploader {
    // Your code here!
}
```

### Challenge 2: File Manager
```typescript
// Create manager that:
// 1. Organizes by type
// 2. Generates previews
// 3. Cleans old files
// 4. Tracks usage

interface FileManager {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Handle uploads
- [x] Process files
- [x] Stream content
- [ ] Ready for more!

## Remember! 🧠
- Validate all files
- Handle errors gracefully
- Clean up temporary files
- Use streams for large files
- Keep security in mind

---
Need a Break? 🎮
- Upload some files!
- Process images!
- Stream content!
- Come back refreshed!

You're a file wizard now! 🧙‍♂️