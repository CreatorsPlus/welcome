# TypeScript Basics: Interfaces vs Objects vs Classes

## Simple Examples 🎯

```typescript
// 1. Object - Like a box of data
const myPet = {
  name: "Rex",
  age: 3,
  bark() {
    console.log("Woof!");
  }
};


// 2. Interface - Like a blueprint
interface Pet {
  name: string;
  age: number;
  bark(): void;
}


// 3. Class - Like a factory that makes objects
class Dog {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  bark() {
    console.log("Woof!");
  }
}
```

## Real-World Analogy 🌟

Think of building a house:

1. **Object** = An actual house
   ```typescript
   const house = {
     color: "blue",
     rooms: 3,
     hasGarage: true
   };
   ```

2. **Interface** = Building plans/requirements
   ```typescript
   interface House {
     color: string;
     rooms: number;
     hasGarage: boolean;
   }
   ```
  ---
  <details>
  <summary> 💡 Wanna dig deeper??</summary>

  # TypeScript Interfaces: A Complete Guide

  ## Basic Interface 🔨

  ```typescript
  // Define shape of a person
  interface Person {
    name: string;
    age: number;
  }

  // Use the interface
  const alice: Person = {
    name: "Alice",
    age: 30
  };

  // Error: missing age
  const bob: Person = {
    name: "Bob"
  };

  // Error: extra property
  const charlie: Person = {
    name: "Charlie",
    age: 25,
    city: "London"
  };
  ```

  ## Optional Properties 🎈

  ```typescript
  interface Car {
    brand: string;
    model: string;
    year?: number;     // Optional
    color?: string;    // Optional
  }

  // All valid
  const car1: Car = { brand: "Toyota", model: "Camry" };
  const car2: Car = { brand: "Honda", model: "Civic", year: 2020 };
  const car3: Car = { brand: "Tesla", model: "S", year: 2021, color: "red" };
  ```

  ## Read-only Properties 🔒

  ```typescript
  interface Config {
    readonly apiKey: string;
    readonly maxRetries: number;
  }

  const config: Config = {
    apiKey: "abc123",
    maxRetries: 3
  };

  // Error: can't modify readonly property
  config.apiKey = "xyz789";
  ```

  ## Function Types 🎯

  ```typescript
  interface Calculator {
    add(x: number, y: number): number;
    subtract(x: number, y: number): number;
  }

  const calculator: Calculator = {
    add: (x, y) => x + y,
    subtract: (x, y) => x - y
  };

  console.log(calculator.add(5, 3));      // 8
  console.log(calculator.subtract(5, 3));  // 2
  ```

  ## Extending Interfaces 🌱

  ```typescript
  interface Animal {
    name: string;
    species: string;
  }

  interface Pet extends Animal {
    owner: string;
  }

  interface Dog extends Pet {
    breed: string;
    bark(): void;
  }

  const myDog: Dog = {
    name: "Rex",
    species: "Canis lupus",
    owner: "Alice",
    breed: "German Shepherd",
    bark() { console.log("Woof!"); }
  };
  ```

  ## Interface with Classes 🏭

  ```typescript
  interface Vehicle {
    start(): void;
    stop(): void;
  }

  class Bicycle implements Vehicle {
    start() {
      console.log("Start pedaling");
    }
    
    stop() {
      console.log("Stop pedaling");
    }
  }

  class ElectricCar implements Vehicle {
    start() {
      console.log("Press start button");
    }
    
    stop() {
      console.log("Press stop button");
    }
  }
  ```

  ## Index Signatures 📚

  ```typescript
  interface Dictionary {
    [key: string]: string;
  }

  const colors: Dictionary = {
    red: "#FF0000",
    green: "#00FF00",
    blue: "#0000FF"
  };

  // Valid
  colors.yellow = "#FFFF00";

  // Error: value must be string
  colors.purple = 123;
  ```

  ## Hybrid Types 🔄

  ```typescript
  interface Counter {
    count: number;
    reset(): void;
    increment(): void;
    (start: number): string;
  }

  function createCounter(): Counter {
    const counter = function(start: number) {
      return "Count started at " + start;
    } as Counter;
    
    counter.count = 0;
    counter.reset = function() { counter.count = 0; };
    counter.increment = function() { counter.count++; };
    
    return counter;
  }

  const counter = createCounter();
  console.log(counter(10));        // "Count started at 10"
  console.log(counter.count);      // 0
  counter.increment();
  console.log(counter.count);      // 1
  ```

  ## Generic Interfaces 🎨

  ```typescript
  interface Box<T> {
    value: T;
    display(): void;
  }

  const stringBox: Box<string> = {
    value: "Hello",
    display() { console.log(this.value); }
  };

  const numberBox: Box<number> = {
    value: 42,
    display() { console.log(this.value); }
  };

  interface Collection<T> {
    items: T[];
    add(item: T): void;
    remove(item: T): void;
  }

  class List<T> implements Collection<T> {
    items: T[] = [];
    
    add(item: T) {
      this.items.push(item);
    }
    
    remove(item: T) {
      const index = this.items.indexOf(item);
      if (index > -1) {
        this.items.splice(index, 1);
      }
    }
  }
  ```
  </details>

  --- 

1. **Class** = House factory/builder
   ```typescript
   class HouseBuilder {
     color: string;
     rooms: number;
     hasGarage: boolean;

     constructor(color: string, rooms: number, hasGarage: boolean) {
       this.color = color;
       this.rooms = rooms;
       this.hasGarage = hasGarage;
     }

     paint(newColor: string) {
       this.color = newColor;
     }
   }
   ```

## Key Differences 🔑

1. **Object**
   - Just data
   - Use when you need a single instance
   ```typescript
   const myPhone = {
     brand: "Apple",
     model: "iPhone 13"
   };
   ```

2. **Interface**
   - Just rules
   - Use to define shapes
   ```typescript
   interface Phone {
     brand: string;
     model: string;
   }

   // Now any phone must follow these rules
   const myPhone: Phone = {
     brand: "Apple",
     model: "iPhone 13"
   };
   ```


3. **Class**
   - Rules + Behavior + Creating new instances
   - Use when you need multiple similar objects
   ```typescript
   class Phone {
     constructor(
       public brand: string,
       public model: string
     ) {}

     makeCall(number: string) {
       console.log(`Calling ${number}...`);
     }
   }

   // Make as many phones as you want
   const phone1 = new Phone("Apple", "iPhone 13");
   const phone2 = new Phone("Samsung", "S21");
   ```

## When to Use What? 🤔

```typescript
// Use OBJECT when you need just one thing
const settings = {
  theme: "dark",
  fontSize: 16
};

// Use INTERFACE when you need to define a shape
interface UserProfile {
  name: string;
  age: number;
}

// Use CLASS when you need many similar things with behavior
class User {
  constructor(
    public name: string,
    public age: number
  ) {}

  sayHi() {
    console.log(`Hi, I'm ${this.name}!`);
  }
}

// Make many users
const user1 = new User("Alice", 25);
const user2 = new User("Bob", 30);
```