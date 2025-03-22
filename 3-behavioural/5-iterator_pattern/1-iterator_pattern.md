# Iterator Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Iterator Pattern?

The **Iterator Pattern** provides a way to access elements of a collection sequentially without exposing its underlying representation. It separates traversal logic from collection implementation.

## Why and When to Use the Iterator Pattern?

### Benefits:
- **Decoupling**: Separates collection and traversal.
- **Simplified Interface**: Provides a clear way to iterate.
- **Single Responsibility Principle**: Collection maintains storage; iterator manages traversal.

### Use the Iterator Pattern when:
- You want uniform iteration over different collections.
- You need to encapsulate traversal logic.

## Example of Iterator Pattern in TypeScript

### Step 1: Iterator Interface

```typescript
interface Iterator<T> {
  next(): T | null;
  hasNext(): boolean;
}
```

### Step 2: Aggregate Interface

```typescript
interface Aggregate<T> {
  getIterator(): Iterator<T>;
}
```

### Step 3: Concrete Collection

```typescript
class NumberCollection implements Aggregate<number> {
  private numbers: number[] = [];

  addNumber(num: number): void {
    this.numbers.push(num);
  }

  getIterator(): Iterator<number> {
    return new NumberIterator(this.numbers);
  }
}
```

### Step 4: Concrete Iterator

```typescript
class NumberIterator implements Iterator<number> {
  private index: number = 0;
  private numbers: number[];

  constructor(numbers: number[]) {
    this.numbers = numbers;
  }

  next(): number | null {
    if (this.hasNext()) {
      return this.numbers[this.index++];
    }
    return null;
  }

  hasNext(): boolean {
    return this.index < this.numbers.length;
  }
}
```

### Step 5: Using the Iterator Pattern

```typescript
const numbers = new NumberCollection();
numbers.addNumber(1);
numbers.addNumber(2);
numbers.addNumber(3);

const iterator = numbers.getIterator();

while (iterator.hasNext()) {
  console.log(iterator.next());
}
```

### Output
```
1
2
3
```

## Conclusion

The Iterator Pattern provides a clean and efficient way to traverse collections without exposing their internal structures, improving modularity and maintainability.