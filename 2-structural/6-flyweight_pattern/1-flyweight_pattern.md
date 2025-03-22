# Flyweight Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Flyweight Pattern?

The **Flyweight Pattern** is used to minimize memory usage by sharing as much data as possible with similar objects. 

It's especially useful for applications handling many objects with shared state.

## Why and When to Use the Flyweight Pattern?

### Benefits:
- **Memory Efficiency**: Reduces memory consumption by sharing objects.
- **Performance Improvement**: Faster object instantiation.

### Use the Flyweight Pattern when:
- Your application creates a large number of similar objects.
- You want to reduce memory usage by sharing common data.

## Example of Flyweight Pattern in TypeScript

### Step 1: Flyweight Interface

```typescript
interface Shape {
  draw(x: number, y: number): void;
}
```

### Step 2: Concrete Flyweight

```typescript
class Circle implements Shape {
  private color: string;

  constructor(color: string) {
    this.color = color;
  }

  draw(x: number, y: number): void {
    console.log(`Drawing ${this.color} circle at (${x}, ${y})`);
  }
}
```

### Step 3: Flyweight Factory

```typescript
class ShapeFactory {
  private static circleMap: { [color: string]: Shape } = {};

  static getCircle(color: string): Shape {
    let circle = this.circleMap[color];

    if (!circle) {
      circle = new Circle(color);
      this.circleMap[color] = circle;
      console.log(`Creating a new ${color} circle.`);
    }

    return circle;
  }
}
```

### Step 4: Using Flyweights

```typescript
const colors = ['Red', 'Green', 'Blue', 'Red', 'Green'];

colors.forEach((color, index) => {
  const circle = ShapeFactory.getCircle(color);
  circle.draw(index * 10, index * 10);
});
```

### Output
```
Creating a new Red circle.
Drawing Red circle at (0, 0)
Creating a new Green circle.
Drawing Green circle at (10, 10)
Creating a new Blue circle.
Drawing Blue circle at (20, 20)
Drawing Red circle at (30, 30)
Drawing Green circle at (40, 40)
```

## Conclusion

The Flyweight Pattern efficiently handles objects by sharing common data, significantly reducing memory usage and improving application performance when dealing with large sets of similar objects.
