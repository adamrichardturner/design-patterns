# Bridge Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Bridge Pattern?

The **Bridge Pattern** separates abstraction from implementation, allowing them to vary independently. 

It decouples the abstraction (interface or high-level logic) from its implementation details, improving flexibility and maintainability.

## Why and When to Use the Bridge Pattern?

### Benefits:
- **Decoupling**: Separates high-level logic from low-level implementation.
- **Flexibility**: Allows independent modification and extension of abstraction and implementation.
- **Improved Maintainability**: Simplifies future changes and extensions.

### Use the Bridge Pattern when:
- You want abstraction and implementation to evolve independently.
- You have multiple implementations that should be interchangeable.
- You're dealing with complex inheritance hierarchies.

## Example of Bridge Pattern in TypeScript

### Step 1: Define Implementor Interface

```typescript
interface Renderer {
  renderCircle(radius: number): void;
}
```

### Step 2: Concrete Implementations

```typescript
class VectorRenderer implements Renderer {
  renderCircle(radius: number): void {
    console.log(`Drawing a vector circle with radius ${radius}`);
  }
}

class RasterRenderer implements Renderer {
  renderCircle(radius: number): void {
    console.log(`Drawing a raster circle with radius ${radius}`);
  }
}
```

### Step 3: Define Abstraction

```typescript
abstract class Shape {
  protected renderer: Renderer;

  constructor(renderer: Renderer) {
    this.renderer = renderer;
  }

  abstract draw(): void;
  abstract resize(factor: number): void;
}
```

### Step 4: Refined Abstraction

```typescript
class Circle extends Shape {
  private radius: number;

  constructor(renderer: Renderer, radius: number) {
    super(renderer);
    this.radius = radius;
  }

  draw(): void {
    this.renderer.renderCircle(this.radius);
  }

  resize(factor: number): void {
    this.radius *= factor;
  }
}
```

### Step 5: Using the Bridge

```typescript
const raster = new RasterRenderer();
const vector = new VectorRenderer();

const circle = new Circle(vector, 5);
circle.draw();
circle.resize(2);
circle.draw();

const rasterCircle = new Circle(raster, 3);
rasterCircle.draw();
```

### Output
```
Drawing a vector circle with radius 5
Drawing a vector circle with radius 10
Drawing a raster circle with radius 3
```

## Conclusion

The Bridge Pattern effectively separates abstraction from implementation, allowing flexible, maintainable, and independently evolving code.
