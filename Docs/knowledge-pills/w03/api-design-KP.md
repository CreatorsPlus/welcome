# API Design: Your REST Quest! 🏰
<!-- Doc type - Knowledge Pill 💊 -->

## Your Mission! 🎯
Learn to:
- Design amazing APIs
- Create perfect endpoints
- Handle data like a pro
- Make developers happy!

## Quick Win! ⚡
Try this perfect endpoint:
```typescript
// The perfect REST endpoint!
app.get('/api/treasures/:id', (req, res) => {
    res.json({
        id: req.params.id,
        name: "Dragon's Gold",
        value: 1000,
        found: new Date()
    });
});
```

## Level 1: REST Basics 🗺️

### The Sacred REST Paths
```typescript
// Your API Map!
GET    /treasures     // List all treasures
POST   /treasures     // Add new treasure
GET    /treasures/1   // Get one treasure
PUT    /treasures/1   // Update treasure
DELETE /treasures/1   // Remove treasure

// Try it!
interface Treasure {
    id: number;
    name: string;
    value: number;
}

app.get('/treasures', (req, res) => {
    const treasures: Treasure[] = [
        { id: 1, name: 'Golden Key', value: 100 },
        { id: 2, name: 'Magic Sword', value: 500 }
    ];
    res.json({ data: treasures });
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Know REST paths
- [x] Return JSON
- [ ] Ready for responses!

## Level 2: Response Patterns! 🎨

### Perfect Responses
```typescript
// Your response template!
interface ApiResponse<T> {
    success: boolean;    // Always include this!
    data: T;            // Your main treasure
    message?: string;   // Helpful notes
    timestamp: number;  // When it happened
}

// Use it like magic!
function sendTreasure<T>(res: Response, data: T): void {
    const response: ApiResponse<T> = {
        success: true,
        data,
        timestamp: Date.now()
    };
    res.json(response);
}

// Try it!
app.get('/treasures/1', (req, res) => {
    const treasure = { id: 1, name: 'Golden Key' };
    sendTreasure(res, treasure);
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Structure responses
- [x] Include metadata
- [ ] Level up to queries!

## Level 3: Query Powers! 🔍

### Search and Filter
```typescript
// Magic query handler!
interface TreasureQuery {
    minValue?: number;
    type?: string;
    sort?: 'value' | 'name';
}

app.get('/treasures', (req: Request<{}, {}, {}, TreasureQuery>, res) => {
    const { minValue, type, sort } = req.query;
    
    let treasures = fetchTreasures();  // Your data source
    
    // Apply filters like magic! ✨
    if (minValue) {
        treasures = treasures.filter(t => t.value >= minValue);
    }
    
    if (type) {
        treasures = treasures.filter(t => t.type === type);
    }
    
    // Sort if needed! 🔮
    if (sort) {
        treasures.sort((a, b) => a[sort] > b[sort] ? 1 : -1);
    }
    
    sendTreasure(res, treasures);
});
```

## Mini Games! 🎮

### Game 1: Status Code Master
```typescript
// Match the code to the situation!
function sendResponse(res: Response, situation: string): void {
    switch(situation) {
        case 'found':
            res.status(200).json({ message: 'Success! 🎉' });
            break;
        case 'created':
            res.status(201).json({ message: 'Created! ⭐' });
            break;
        case 'missing':
            res.status(404).json({ message: 'Not found! 😢' });
            break;
        case 'error':
            res.status(500).json({ message: 'Oops! 💥' });
            break;
    }
}
```

### Game 2: Path Builder
```typescript
// Build the perfect path!
class PathMaster {
    static build(resource: string, id?: number): string {
        return id 
            ? `/api/${resource}/${id}`
            : `/api/${resource}`;
    }
}

// Use it!
const treasurePath = PathMaster.build('treasures', 1);
console.log(treasurePath);  // /api/treasures/1
```

---
🎉 **POWER-UPS** 🎉

### Response Helper
```typescript
// Make responses awesome!
class ApiResponder {
    static success<T>(data: T, message?: string) {
        return {
            success: true,
            data,
            message,
            timestamp: Date.now()
        };
    }
    
    static error(code: string, message: string) {
        return {
            success: false,
            error: { code, message },
            timestamp: Date.now()
        };
    }
}

// Use it!
app.get('/treasure-map', (req, res) => {
    try {
        const map = findMap();
        res.json(ApiResponder.success(map, 'Map found! 🗺️'));
    } catch (error) {
        res.status(500).json(
            ApiResponder.error('MAP_ERROR', 'Map was stolen! 🏴‍☠️')
        );
    }
});
```

## Practice Time! 🏃‍♂️

### Challenge 1: Resource Nesting
```typescript
// Create nested routes:
// /kingdoms/:kingdomId/castles
// /kingdoms/:kingdomId/castles/:castleId
// /kingdoms/:kingdomId/castles/:castleId/treasures

// Start here:
interface Kingdom { id: number; name: string; }
interface Castle { id: number; name: string; }
```

### Challenge 2: Query Builder
```typescript
// Build a query system that:
// 1. Handles pagination
// 2. Allows sorting
// 3. Supports filtering
// 4. Validates parameters

interface QueryOptions {
    page?: number;
    limit?: number;
    sort?: string;
    filter?: Record<string, string>;
}

// Your code here!
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Design endpoints
- [x] Structure responses
- [x] Handle queries
- [ ] Ready for more!

## Remember! 🧠
- Use nouns for resources
- Keep paths consistent
- Handle all status codes
- Document everything!

---
Need a Break? 🎮
- Test your endpoints!
- Draw your API map!
- Plan new features!
- Come back creative!

You're an API architect now! 🏛️