# Builder Design Pattern in TypeScript

[« Back to Project Readme](../../../README.md)

## What is the Builder Design Pattern?

The **Builder Design Pattern** is a creational pattern that simplifies the construction of complex objects. It separates the construction of an object from its representation, allowing the same construction process to create different representations.

This pattern is particularly useful when you have complex objects with many optional or required configurations. It improves readability and maintainability by using method chaining and clearly defined construction steps.

## Why and When to Use the Builder Pattern?

### Benefits:
- **Clarity**: Clearly separates object creation from its use.
- **Flexibility**: Enables creating different object configurations using the same construction process.
- **Immutability**: Often produces immutable objects, enhancing safety and predictability.

### Use Builder Pattern when:
- An object has many attributes or configurations.
- The object construction is complex and requires step-by-step creation.
- You want a clear, fluent interface for object creation.

## Example of Builder Pattern in TypeScript

Let's illustrate this pattern with an example of creating a customizable `Pizza` object.

### Step 1: Define the Product Class

Define the complex object you want to build:

```typescript
class Pizza {
  size: string;
  cheese: boolean;
  pepperoni: boolean;
  mushrooms: boolean;

  constructor(builder: PizzaBuilder) {
    this.size = builder.size;
    this.cheese = builder.cheese;
    this.pepperoni = builder.pepperoni;
    this.mushrooms = builder.mushrooms;
  }

  describe(): void {
    console.log(`Pizza [Size: ${this.size}, Cheese: ${this.cheese}, Pepperoni: ${this.pepperoni}, Mushrooms: ${this.mushrooms}]`);
  }
}
```

### Step 2: Create the Builder Class

Implement the builder that handles step-by-step object construction:

```typescript
class PizzaBuilder {
  size: string;
  cheese: boolean = false;
  pepperoni: boolean = false;
  mushrooms: boolean = false;

  constructor(size: string) {
    this.size = size;
  }

  addCheese(): PizzaBuilder {
    this.cheese = true;
    return this;
  }

  addPepperoni(): PizzaBuilder {
    this.pepperoni = true;
    return this;
  }

  addMushrooms(): PizzaBuilder {
    this.mushrooms = true;
    return this;
  }

  build(): Pizza {
    return new Pizza(this);
  }
}
```

### Step 3: Using the Builder

Here's how a client can use the builder to create pizzas:

```typescript
// Create a pizza with cheese and pepperoni
const pizza1 = new PizzaBuilder('Large')
  .addCheese()
  .addPepperoni()
  .build();

pizza1.describe();

// Create a vegetarian pizza
const pizza2 = new PizzaBuilder('Medium')
  .addCheese()
  .addMushrooms()
  .build();

pizza2.describe();
```

**Output:**
```
Pizza [Size: Large, Cheese: true, Pepperoni: true, Mushrooms: false]
Pizza [Size: Medium, Cheese: true, Pepperoni: false, Mushrooms: true]
```

## Advantages of Using the Builder Pattern

- Easy to manage optional and mandatory attributes clearly.
- Creates highly readable code with method chaining.
- Simplifies the construction of complex objects without constructors with many parameters.

## Extending the Builder Pattern

To extend the builder with additional options (e.g., adding olives), simply:

1. Update the builder class:

```typescript
addOlives(): PizzaBuilder {
  (this as any).olives = true;
  return this;
}
```

2. Update the product class if needed:

```typescript
class Pizza {
  // ...existing properties
  olives: boolean;

  constructor(builder: PizzaBuilder) {
    // ...existing assignments
    this.olives = (builder as any).olives || false;
  }

  describe(): void {
    console.log(`Pizza [Size: ${this.size}, Cheese: ${this.cheese}, Pepperoni: ${this.pepperoni}, Mushrooms: ${this.mushrooms}, Olives: ${this.olives}]`);
  }
}
```

Client usage remains fluent:

```typescript
const pizza3 = new PizzaBuilder('Small')
  .addCheese()
  .addOlives()
  .build();

pizza3.describe();
```

**Output:**
```
Pizza [Size: Small, Cheese: true, Pepperoni: false, Mushrooms: false, Olives: true]
```

## Conclusion

The Builder Design Pattern simplifies constructing complex objects step by step. It provides an intuitive, fluent, and readable approach, making object creation flexible, scalable, and maintainable.

