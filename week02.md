# Week 2 Project: Interactive Todo Application

## Project Overview
Build a browser-based Todo application using TypeScript, demonstrating DOM manipulation, event handling, and state management.

## Project Structure
```plaintext
todo-app/
├── src/
│   ├── models/
│   │   ├── Todo.ts           // Todo item type definitions
│   │   └── Store.ts          // Data management
│   ├── components/
│   │   ├── TodoList.ts       // Todo list UI component
│   │   ├── TodoItem.ts       // Individual todo UI component
│   │   └── TodoForm.ts       // Add/edit todo form
│   ├── utils/
│   │   ├── dom.ts           // DOM helper functions
│   │   └── validation.ts    // Input validation
│   ├── styles/
│   │   └── main.css         // Styles
│   └── app.ts               // Main application file
├── index.html               // Main HTML file
├── tsconfig.json           // TypeScript configuration
└── package.json            // Project dependencies
```

## Implementation Steps

### 1. Basic Setup (Day 8)
```typescript
// models/Todo.ts
interface Todo {
    id: number;
    title: string;
    completed: boolean;
    createdAt: Date;
}

// Initial HTML structure
<!DOCTYPE html>
<html>
<head>
    <title>TypeScript Todo App</title>
    <link rel="stylesheet" href="styles/main.css">
</head>
<body>
    <div id="app">
        <form id="todo-form">
            <input type="text" id="todo-input" placeholder="Add a new todo">
            <button type="submit">Add</button>
        </form>
        <div id="todo-list"></div>
    </div>
    <script src="dist/app.js"></script>
</body>
</html>
```

### 2. State Management (Day 9-10)
```typescript
// models/Store.ts
class TodoStore {
    private todos: Todo[] = [];
    
    addTodo(title: string): void {
        const todo: Todo = {
            id: Date.now(),
            title,
            completed: false,
            createdAt: new Date()
        };
        this.todos.push(todo);
        this.emit('todo-added', todo);
    }
    
    toggleTodo(id: number): void {
        const todo = this.todos.find(t => t.id === id);
        if (todo) {
            todo.completed = !todo.completed;
            this.emit('todo-updated', todo);
        }
    }
}
```

### 3. UI Components (Day 11-12)
```typescript
// components/TodoList.ts
class TodoList {
    private container: HTMLElement;
    
    constructor(containerId: string) {
        const element = document.getElementById(containerId);
        if (!element) throw new Error('Container not found');
        this.container = element;
    }
    
    render(todos: Todo[]): void {
        this.container.innerHTML = '';
        todos.forEach(todo => {
            const todoEl = this.createTodoElement(todo);
            this.container.appendChild(todoEl);
        });
    }
}
```

### 4. Local Storage (Day 13)
```typescript
// utils/storage.ts
class TodoStorage {
    private readonly STORAGE_KEY = 'todos';
    
    saveTodos(todos: Todo[]): void {
        localStorage.setItem(this.STORAGE_KEY, JSON.stringify(todos));
    }
    
    loadTodos(): Todo[] {
        const data = localStorage.getItem(this.STORAGE_KEY);
        return data ? JSON.parse(data) : [];
    }
}
```

### 5. Advanced Features (Day 14)
- Filtering (all, active, completed)
- Todo editing
- Bulk actions (mark all, clear completed)
- Drag and drop reordering

## Daily Objectives

### Day 8: Project Setup
- [ ] Initialize project structure
- [ ] Set up TypeScript configuration
- [ ] Create basic HTML structure
- [ ] Implement Todo type definitions

### Day 9-10: Core Functionality
- [ ] Implement TodoStore class
- [ ] Add todo creation
- [ ] Add todo completion toggle
- [ ] Basic event handling

### Day 11-12: UI Enhancement
- [ ] Style the application
- [ ] Add animations
- [ ] Implement TodoList component
- [ ] Add form validation

### Day 13: Data Persistence
- [ ] Add local storage
- [ ] Implement data loading/saving
- [ ] Add error handling
- [ ] Add data validation

### Day 14: Advanced Features
- [ ] Add filtering
- [ ] Implement editing
- [ ] Add bulk actions
- [ ] Implement drag and drop

## Learning Outcomes
By completing this project, students will demonstrate:
1. DOM manipulation with TypeScript
2. Event handling and type safety
3. State management
4. Local storage usage
5. UI component design
6. Form handling and validation

## Bonus Challenges
- Add due dates to todos
- Implement categories/tags
- Add priority levels
- Implement undo/redo
- Add keyboard shortcuts

## Evaluation Criteria
- Type safety
- Code organization
- Error handling
- UI/UX design
- Code reusability
- Project structure

> **Pro Tip**: Commit your code regularly and keep components small and focused. Consider creating new Knowledge Pills for complex features you implement.