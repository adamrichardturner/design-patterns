# Strategy Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Strategy Pattern?

The **Strategy Pattern** enables selecting an algorithm at runtime. It defines a family of algorithms, encapsulates each, and makes them interchangeable.

## Why and When to Use the Strategy Pattern?

### Benefits:
- **Flexibility**: Change behavior dynamically.
- **Maintainability**: Easy to add or remove algorithms.

### Use the Strategy Pattern when:
- You have multiple algorithms for a task.
- Algorithms need to be interchangeable.

## Example of Strategy Pattern in TypeScript

### Step 1: Strategy Interface

```typescript
interface Strategy {
  execute(a: number, b: number): number;
}
```

### Step 2: Concrete Strategies

```typescript
class AddStrategy implements Strategy {
  execute(a: number, b: number): number {
    return a + b;
  }
}

class SubtractStrategy implements Strategy {
  execute(a: number, b: number): number {
    return a - b;
  }
}

class MultiplyStrategy implements Strategy {
  execute(a: number, b: number): number {
    return a * b;
  }
}
```

### Step 3: Context Class

```typescript
class Calculator {
  private strategy: Strategy;

  setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  executeStrategy(a: number, b: number): number {
    return this.strategy.execute(a, b);
  }
}
```

### Step 4: Using the Strategy Pattern

```typescript
const calculator = new Calculator();

calculator.setStrategy(new AddStrategy());
console.log("Add Strategy:", calculator.executeStrategy(5, 3));

calculator.setStrategy(new SubtractStrategy());
console.log("Subtract Strategy:", calculator.executeStrategy(5, 3));

calculator.setStrategy(new MultiplyStrategy());
console.log("Multiply Strategy:", calculator.executeStrategy(5, 3));
```

### Output
```
Add Strategy: 8
Subtract Strategy: 2
Multiply Strategy: 15
```

## Conclusion

The Strategy Pattern allows flexible and dynamic selection of algorithms, greatly enhancing application adaptability and maintainability.