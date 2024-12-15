# Template Magic: Server-Side Spells! 🏰
<!-- Doc type - Knowledge Pill 💊 -->

## Your Quest! 🎯
Learn to:
- Cast template spells
- Create magical layouts
- Share view components
- Make dynamic pages!

## Quick Win! ⚡
Try this magical template:
```ejs
<!-- views/spellbook.ejs -->
<div class="spellbook">
    <h1><%= title %></h1>
    <% spells.forEach(spell => { %>
        <div class="spell">
            ✨ <%= spell.name %>
        </div>
    <% }); %>
</div>

// Cast it with TypeScript!
app.get('/spellbook', (req, res) => {
    res.render('spellbook', {
        title: 'My Spellbook',
        spells: [
            { name: 'Lumos' },
            { name: 'Wingardium Leviosa' }
        ]
    });
});
```

## Level 1: Layout Magic 📜

### Base Layout Scroll
```ejs
<!-- views/layouts/scroll.ejs -->
<!DOCTYPE html>
<html>
<head>
    <title>🔮 <%= title %></title>
</head>
<body>
    <%- include('../partials/navigation') %>
    
    <div class="scroll">
        <%- body %>
    </div>
    
    <%- include('../partials/footer') %>
</body>
</html>

// Use it with TypeScript!
interface ScrollData {
    title: string;
    user?: Wizard;  // Your user type
}

app.get('/', (req, res) => {
    const data: ScrollData = {
        title: 'Magic Home',
        user: getCurrentWizard(req)
    };
    res.render('home', data);
});
```

---
⭐ **CHECKPOINT 1** ⭐
- [x] Made first template
- [x] Used layouts
- [ ] Ready for partials!

## Level 2: Partial Scrolls! 📜

### Magic Components
```ejs
<!-- views/partials/spell-card.ejs -->
<div class="spell-card">
    <h3><%= spell.name %></h3>
    <p>Power: <%= spell.power %></p>
    <% if (spell.available) { %>
        <button>Cast! ✨</button>
    <% } %>
</div>

// Use it in other scrolls!
<div class="spells">
    <% spells.forEach(spell => { %>
        <%- include('partials/spell-card', { spell }) %>
    <% }); %>
</div>
```

### Navigation Scroll
```ejs
<!-- views/partials/navigation.ejs -->
<nav class="magic-nav">
    <% navItems.forEach(item => { %>
        <a 
            href="<%= item.path %>"
            class="<%= currentPath === item.path ? 'active' : '' %>"
        >
            <%= item.label %>
        </a>
    <% }); %>
</nav>

// Type-safe navigation!
interface NavItem {
    path: string;
    label: string;
    icon?: string;
}

// Add to all pages
app.use((req, res, next) => {
    res.locals.navItems = [
        { path: '/', label: 'Home 🏰' },
        { path: '/spells', label: 'Spells ✨' },
        { path: '/potions', label: 'Potions 🧪' }
    ];
    res.locals.currentPath = req.path;
    next();
});
```

---
⭐ **CHECKPOINT 2** ⭐
- [x] Create partials
- [x] Share components
- [ ] Level up to helpers!

## Level 3: Helper Spells! 🔮

### Magic Helpers
```typescript
// Create your helper spellbook!
const magicHelpers = {
    formatSpellPower(power: number): string {
        return '⚡'.repeat(Math.min(power, 5));
    },
    
    timeAgo(date: Date): string {
        // Magic time calculation...
        return '2 moons ago';
    },
    
    truncate(str: string, len: number): string {
        return str.length > len ? 
            str.slice(0, len) + '...' : 
            str;
    }
};

// Add to your templates!
app.use((req, res, next) => {
    res.locals.helpers = magicHelpers;
    next();
});

// Use in templates!
<div class="spell-power">
    <%= helpers.formatSpellPower(spell.power) %>
</div>
```

## Mini Games! 🎮

### Game 1: Dynamic Menu
```typescript
// Create a magic menu system!
interface MenuItem {
    label: string;
    path: string;
    children?: MenuItem[];
    icon?: string;
}

const menuItems: MenuItem[] = [
    {
        label: 'Spells',
        path: '/spells',
        children: [
            { label: 'New Spell', path: '/spells/new' },
            { label: 'Spell Book', path: '/spells/book' }
        ]
    }
];

// Create the menu partial!
<!-- views/partials/magic-menu.ejs -->
<% function renderMenu(items) { %>
    <ul class="menu">
        <% items.forEach(item => { %>
            <li>
                <a href="<%= item.path %>">
                    <%= item.label %>
                </a>
                <% if (item.children) { %>
                    <%= renderMenu(item.children) %>
                <% } %>
            </li>
        <% }); %>
    </ul>
<% } %>

<%= renderMenu(menuItems) %>
```

### Game 2: Form Builder
```typescript
// Create a magical form builder!
interface FormField {
    type: 'text' | 'number' | 'select';
    name: string;
    label: string;
    options?: string[];
    required?: boolean;
}

// Create form partial!
<!-- views/partials/magic-form.ejs -->
<% fields.forEach(field => { %>
    <div class="field">
        <label><%= field.label %></label>
        <% if (field.type === 'select') { %>
            <select name="<%= field.name %>">
                <% field.options.forEach(opt => { %>
                    <option><%= opt %></option>
                <% }); %>
            </select>
        <% } else { %>
            <input 
                type="<%= field.type %>"
                name="<%= field.name %>"
                required="<%= field.required %>"
            >
        <% } %>
    </div>
<% }); %>
```

---
🎉 **POWER-UPS** 🎉

### Quick View Renderer
```typescript
// Make rendering easier!
class ViewRenderer {
    static render(
        res: Response,
        view: string,
        data: ViewData
    ): void {
        res.render(view, {
            ...data,
            helpers: magicHelpers,
            flash: req.flash()
        });
    }
}

// Use it!
app.get('/spells', (req, res) => {
    ViewRenderer.render(res, 'spells/index', {
        title: 'Spell Collection',
        spells: getSpells()
    });
});
```

## Practice Time! 🏃‍♂️

### Challenge 1: Magic Dashboard
```typescript
// Create a dashboard that shows:
// 1. Spell stats
// 2. Recent activities
// 3. Popular spells
// 4. User rankings

// Start here:
interface DashboardData {
    stats: SpellStats;
    activities: Activity[];
    popularSpells: Spell[];
    rankings: Ranking[];
}

// Your code here!
```

### Challenge 2: Wizard Profile
```typescript
// Create a profile page with:
// 1. Avatar upload
// 2. Spell list
// 3. Achievement badges
// 4. Activity feed

// Start here:
interface WizardProfile {
    // Your code here!
}
```

---
⭐ **FINAL CHECKPOINT** ⭐
- [x] Master layouts
- [x] Create partials
- [x] Use helpers
- [ ] Ready for more!

## Remember! 🧠
- Always validate view data
- Keep partials small and focused
- Use type-safe helpers
- Handle missing data gracefully
- Comment your templates!

---
Need a Break? 🎮
- Write some templates!
- Create new partials!
- Test your layouts!
- Come back creative!

You're a template wizard now! 🧙‍♂️