# Decorator Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Decorator Pattern?

The **Decorator Pattern** dynamically adds responsibilities or behaviors to objects at runtime without modifying their original structure or class definition. It promotes flexibility by allowing behaviors to be composed or layered on top of objects.

## Why and When to Use the Decorator Pattern?

### Benefits:
- **Flexibility**: Easily add or remove behaviors.
- **Open/Closed Principle**: Extend object functionality without modifying existing code.
- **Dynamic Composition**: Build complex behaviors from simpler components.

### Use the Decorator Pattern when:
- You need to add functionality to objects dynamically.
- Modifying the existing classes is not practical or desirable.
- You want flexible behavior extensions.

## Example of Decorator Pattern in TypeScript

### Step 1: Define Component Interface

```typescript
interface Coffee {
  cost(): number;
  description(): string;
}
```

### Step 2: Concrete Component

```typescript
class SimpleCoffee implements Coffee {
  cost(): number {
    return 5;
  }

  description(): string {
    return 'Simple coffee';
  }
}
```

### Step 3: Decorator Base Class

```typescript
abstract class CoffeeDecorator implements Coffee {
  protected decoratedCoffee: Coffee;

  constructor(coffee: Coffee) {
    this.decoratedCoffee = coffee;
  }

  abstract cost(): number;
  abstract description(): string;
}
```

### Step 4: Concrete Decorators

```typescript
class MilkDecorator extends CoffeeDecorator {
  cost(): number {
    return this.decoratedCoffee.cost() + 2;
  }

  description(): string {
    return `${this.decoratedCoffee.description()}, milk`;
  }
}

class SugarDecorator extends CoffeeDecorator {
  cost(): number {
    return this.decoratedCoffee.cost() + 1;
  }

  description(): string {
    return `${this.decoratedCoffee.description()}, sugar`;
  }
}
```

### Step 5: Using Decorators

```typescript
let coffee: Coffee = new SimpleCoffee();
console.log(coffee.description(), coffee.cost());

coffee = new MilkDecorator(coffee);
console.log(coffee.description(), coffee.cost());

coffee = new SugarDecorator(coffee);
console.log(coffee.description(), coffee.cost());
```

### Output
```
Simple coffee 5
Simple coffee, milk 7
Simple coffee, milk, sugar 8
```

## Conclusion

The Decorator Pattern offers a powerful and flexible way to add functionality dynamically, helping you maintain and scale your applications without unnecessary complexity.