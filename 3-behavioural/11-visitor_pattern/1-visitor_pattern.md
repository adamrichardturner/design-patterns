# Visitor Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Visitor Pattern?

The **Visitor Pattern** lets you define a new operation without changing the classes on which it operates. It separates algorithms from the objects they operate on.

## Why and When to Use the Visitor Pattern?

### Benefits:
- **Open/Closed Principle**: Extend functionality without modifying classes.
- **Single Responsibility Principle**: Separates algorithm logic from object structure.

### Use the Visitor Pattern when:
- You need to perform operations on objects without altering their classes.
- You want to keep algorithms separate from objects.

## Example of Visitor Pattern in TypeScript

### Step 1: Visitor Interface

```typescript
interface Visitor {
  visitConcreteElementA(element: ConcreteElementA): void;
  visitConcreteElementB(element: ConcreteElementB): void;
}
```

### Step 2: Element Interface

```typescript
interface Element {
  accept(visitor: Visitor): void;
}
```

### Step 3: Concrete Elements

```typescript
class ConcreteElementA implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementA(this);
  }

  operationA(): void {
    console.log("ConcreteElementA operation.");
  }
}

class ConcreteElementB implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementB(this);
  }

  operationB(): void {
    console.log("ConcreteElementB operation.");
  }
}
```

### Step 4: Concrete Visitor

```typescript
class ConcreteVisitor implements Visitor {
  visitConcreteElementA(element: ConcreteElementA): void {
    console.log("Visitor performing operation on ConcreteElementA.");
    element.operationA();
  }

  visitConcreteElementB(element: ConcreteElementB): void {
    console.log("Visitor performing operation on ConcreteElementB.");
    element.operationB();
  }
}
```

### Step 5: Using the Visitor Pattern

```typescript
const elements: Element[] = [new ConcreteElementA(), new ConcreteElementB()];
const visitor = new ConcreteVisitor();

elements.forEach(element => element.accept(visitor));
```

### Output
```
Visitor performing operation on ConcreteElementA.
ConcreteElementA operation.
Visitor performing operation on ConcreteElementB.
ConcreteElementB operation.
```

## Conclusion

The Visitor Pattern enables adding new operations without modifying existing classes, separating algorithms clearly and promoting extensibility.