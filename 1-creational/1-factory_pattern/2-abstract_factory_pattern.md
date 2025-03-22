# Abstract Factory Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Abstract Factory Design Pattern?

The **Abstract Factory Pattern** is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. 

It enables a client to use different families of objects interchangeably, ensuring that the client code remains unaware of the specific implementations it uses.

The main goal is to encapsulate the creation of groups of related objects, making it easy to switch between these groups or families at runtime.

## Why and When to Use the Abstract Factory Pattern?

Benefits:

- **Consistency**: Ensures that the client always uses a compatible set of objects.
- **Encapsulation**: Keeps the creation logic separated from the usage logic.
- **Flexibility**: Makes it easy to introduce new families of objects without changing existing code.

Use the Abstract Factory pattern when:

- Your application requires different families or groups of related objects.
- You want to ensure compatibility between related objects.
- You need flexibility in configuring or extending these families without altering client code.

## Example of Abstract Factory Pattern in TypeScript

Let's illustrate this with a practical example involving the production of furniture.

### Step 1: Define Abstract Products

Create interfaces representing related products:

```typescript
// Abstract Products
interface Chair {
  sitOn(): void;
}

interface Table {
  putItemOn(): void;
}
```

### Step 2: Create Concrete Products

Implement concrete product classes for each family:

```typescript
// Victorian Furniture
class VictorianChair implements Chair {
  sitOn(): void {
    console.log("Sitting on a Victorian chair.");
  }
}

class VictorianTable implements Table {
  putItemOn(): void {
    console.log("Placing item on a Victorian table.");
  }
}

// Modern Furniture
class ModernChair implements Chair {
  sitOn(): void {
    console.log("Sitting on a modern chair.");
  }
}

class ModernTable implements Table {
  putItemOn(): void {
    console.log("Placing item on a modern table.");
  }
}
```

### Step 3: Define the Abstract Factory

Define the abstract factory interface responsible for creating objects:

```typescript
interface FurnitureFactory {
  createChair(): Chair;
  createTable(): Table;
}
```

### Step 4: Implement Concrete Factories

Create concrete factories for each family:

```typescript
// Victorian Factory
class VictorianFurnitureFactory implements FurnitureFactory {
  createChair(): Chair {
    return new VictorianChair();
  }

  createTable(): Table {
    return new VictorianTable();
  }
}

// Modern Factory
class ModernFurnitureFactory implements FurnitureFactory {
  createChair(): Chair {
    return new ModernChair();
  }

  createTable(): Table {
    return new ModernTable();
  }
}
```

### Step 5: Client Code Using the Factory

Here's how a client can use the abstract factory to create and use furniture sets:

```typescript
function clientCode(factory: FurnitureFactory) {
  const chair = factory.createChair();
  const table = factory.createTable();

  chair.sitOn();
  table.putItemOn();
}

// Use the Victorian furniture set
console.log("Client: Victorian furniture set:");
clientCode(new VictorianFurnitureFactory());

// Use the Modern furniture set
console.log("\nClient: Modern furniture set:");
clientCode(new ModernFurnitureFactory());
```

**Output:**
```
Client: Victorian furniture set:
Sitting on a Victorian chair.
Placing item on a Victorian table.

Client: Modern furniture set:
Sitting on a modern chair.
Placing item on a modern table.
```

### Extending the Abstract Factory

Suppose we want to introduce a new "Art Deco" furniture family. Simply:

1. Implement new concrete products:

```typescript
class ArtDecoChair implements Chair {
  sitOn(): void {
    console.log("Sitting on an Art Deco chair.");
  }
}

class ArtDecoTable implements Table {
  putItemOn(): void {
    console.log("Placing item on an Art Deco table.");
  }
}
```

2. Implement the concrete factory:

```typescript
class ArtDecoFurnitureFactory implements FurnitureFactory {
  createChair(): Chair {
    return new ArtDecoChair();
  }

  createTable(): Table {
    return new ArtDecoTable();
  }
}
```

No changes to client code are needed to use the new furniture family:

```typescript
console.log("\nClient: Art Deco furniture set:");
clientCode(new ArtDecoFurnitureFactory());
```

## Conclusion

The Abstract Factory Design Pattern helps manage complex object creation scenarios involving multiple related objects or families. 

It promotes a highly modular architecture, making your codebase easier to maintain, extend, and adapt to evolving requirements.

