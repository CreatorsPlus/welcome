# TypeScript Classes: Best Practices and Advanced Concepts

## 1. Classes vs Interfaces 💡

Classes should be used when you need:
- Instance creation
- Implementation details
- Object-oriented patterns
- Methods with behavior
- Constructor logic

```typescript
// Use Interface when you only need type checking
interface UserData {
  name: string;
  email: string;
}

// Use Class when you need behavior and instance creation
class User {
  constructor(
    public name: string,
    public email: string
  ) {}

  sendEmail() {
    // Implementation for sending email
    console.log(`Sending email to ${this.email}`);
  }
}

// Interface usage
const userData: UserData = { name: "John", email: "john@example.com" };

// Class usage
const user = new User("John", "john@example.com");
user.sendEmail();
```

## 2. Optional Properties in Classes 💡

Handle optional properties using:
- Optional parameter syntax (`?`)
- Default values
- Initialization in constructor

```typescript
class Product {
  // Optional property with '?'
  description?: string;

  // Default value
  quantity: number = 0;

  // Private optional property
  private _discount?: number;

  constructor(
    public name: string,
    public price: number,
    description?: string
  ) {
    // Initialize optional property conditionally
    if (description) {
      this.description = description;
    }
  }

  // Safe access to optional property
  getDiscountedPrice(): number {
    return this.price * (1 - (this._discount ?? 0));
  }
}

// Usage
const product1 = new Product("Phone", 999);
const product2 = new Product("Laptop", 1999, "High-performance laptop");
```

## 3. Private vs Protected Properties 💡

```typescript
class Animal {
  private _id: string;         // Only accessible within this class
  protected species: string;   // Accessible in this class and derivatives
  public name: string;        // Accessible everywhere

  constructor(id: string, species: string, name: string) {
    this._id = id;
    this.species = species;
    this.name = name;
  }

  // Private method example
  private generateDisplayId(): string {
    return `${this._id}-${Date.now()}`;
  }
}

class Dog extends Animal {
  constructor(id: string, name: string) {
    super(id, "Canis lupus", name);
  }

  describe(): string {
    // Can access protected property
    return `${this.name} is a ${this.species}`;
    
    // Cannot access private property
    // this._id would cause error
  }
}
```

Use cases:
- `private`: Internal implementation details that should never be accessed outside
- `protected`: Properties that derived classes need to access
- `public`: API that external code should use

## 4. Deep Immutability with Readonly 💡

```typescript
class Configuration {
  // Shallow readonly - array contents can be modified
  readonly shallowReadonlyArray: number[] = [1, 2, 3];

  // Deep readonly - complete immutability
  readonly deepReadonlyArray: ReadonlyArray<number> = [1, 2, 3];

  // Readonly object with mutable contents
  readonly shallowReadonlyObject: { items: string[] } = { items: [] };

  // Deep readonly object
  readonly deepReadonlyObject: Readonly<{
    items: ReadonlyArray<string>;
  }> = { items: [] };

  constructor() {
    // These are allowed:
    this.shallowReadonlyArray[0] = 5;
    this.shallowReadonlyObject.items.push("new");

    // These will cause errors:
    // this.shallowReadonlyArray = [4, 5, 6];
    // this.deepReadonlyArray[0] = 5;
    // this.deepReadonlyObject.items.push("new");
  }
}
```

Use cases for deep immutability:
- Configuration objects
- API responses
- State management
- Constants and lookup tables

Advanced immutability example:

```typescript
class StateManager<T extends object> {
  private readonly state: Readonly<T>;

  constructor(initialState: T) {
    this.state = Object.freeze({ ...initialState });
  }

  getState(): Readonly<T> {
    return this.state;
  }

  createNewState(updater: (currentState: T) => T): StateManager<T> {
    const newState = updater({ ...this.state as T });
    return new StateManager(newState);
  }
}

// Usage
const manager = new StateManager({
  users: ["John"],
  settings: { theme: "dark" }
});

// Create new state immutably
const newManager = manager.createNewState(state => ({
  ...state,
  users: [...state.users, "Jane"]
}));
```

## Best Practices Summary 💡

1. Use classes when you need:
   - Instance creation
   - Encapsulation
   - Inheritance
   - Method implementation

2. Use interfaces when you need:
   - Type checking
   - API contracts
   - Object shape definition
   - Multiple implementation possibility

3. For immutability:
   - Use `readonly` for reference immutability
   - Use `ReadonlyArray<T>` for array immutability
   - Use `Readonly<T>` for object immutability
   - Use `Object.freeze()` for runtime immutability

4. Access modifiers:
   - Start with `private`
   - Use `protected` when inheritance needs access
   - Make `public` only what's necessary for the API