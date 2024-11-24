# Understanding the Spread Operator in TypeScript
<!-- Doc type - Knowledge Pill :pill: -->
## Goal

Learn how to use the spread operator (`...`) to work with arrays, objects, and functions efficiently.

## Step 1: What is the Spread Operator?

The spread operator (`...`) allows you to:
* Copy or merge arrays and objects
* Expand arrays into individual elements
* Pass elements of an array as arguments to a function

## Step 2: Using the Spread Operator with Arrays

### Example 1: Copying an Array

```typescript
const originalArray = [1, 2, 3];
const copiedArray = [...originalArray];

console.log("Original:", originalArray);  // Output: [1, 2, 3]
console.log("Copied:", copiedArray);      // Output: [1, 2, 3]
```

### Example 2: Merging Arrays

```typescript
const array1 = [1, 2];
const array2 = [3, 4];
const mergedArray = [...array1, ...array2];

console.log("Merged:", mergedArray);  // Output: [1, 2, 3, 4]
```

### Example 3: Expanding an Array into Function Arguments

```typescript
const numbers = [10, 20, 30];

function sum(a: number, b: number, c: number): number {
  return a + b + c;
}

console.log("Sum:", sum(...numbers));  // Output: 60
```

## Step 3: Using the Spread Operator with Objects

### Example 4: Copying an Object

```typescript
const originalObject = { name: "Alice", age: 25 };
const copiedObject = { ...originalObject };

console.log("Original:", originalObject);  // Output: { name: "Alice", age: 25 }
console.log("Copied:", copiedObject);      // Output: { name: "Alice", age: 25 }
```

### Example 5: Merging Objects

```typescript
const obj1 = { name: "Alice" };
const obj2 = { age: 25 };
const mergedObject = { ...obj1, ...obj2 };

console.log("Merged:", mergedObject);  // Output: { name: "Alice", age: 25 }
```

## Step 4: Combining Arrays and Objects

### Example 6: Mixing Arrays and Objects

```typescript
const array = ["Alice", "Bob"];
const object = { age: 30 };

const combined = { ...object, names: [...array] };

console.log("Combined:", combined);
// Output: { age: 30, names: ["Alice", "Bob"] }
```

## Step 5: Practice Exercises

### Exercise 1: Modify an Array

1. Copy the array `[5, 10, 15]` into a new array
2. Add `20` at the end of the new array
3. Log the result

**Solution:**
```typescript
const array = [5, 10, 15];
const newArray = [...array, 20];

console.log("Modified Array:", newArray);  // Output: [5, 10, 15, 20]
```

### Exercise 2: Update an Object

1. Copy the object `{ name: "John", age: 40 }`
2. Add a new property `city: "New York"` to the copy
3. Log the result

**Solution:**
```typescript
const person = { name: "John", age: 40 };
const updatedPerson = { ...person, city: "New York" };

console.log("Updated Object:", updatedPerson);
// Output: { name: "John", age: 40, city: "New York" }
```

## Step 6: Run the Code

1. Save the code in a file named `spreadOperator.ts`

2. Compile the code:
```bash
tsc spreadOperator.ts
```

3. Run the code:
```bash
node spreadOperator.js
```