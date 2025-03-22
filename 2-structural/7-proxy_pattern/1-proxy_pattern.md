# Proxy Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Proxy Pattern?

The **Proxy Pattern** provides a placeholder for another object to control access, adding functionality such as lazy loading, access control, logging, or caching without changing the original object's implementation.

## Why and When to Use the Proxy Pattern?

### Benefits:
- **Access Control**: Controls object access.
- **Lazy Initialization**: Delays heavy object creation until necessary.
- **Additional Functionality**: Adds behaviors transparently.

### Use the Proxy Pattern when:
- Controlling access to an object.
- Delaying expensive object creation.
- Adding behaviors like logging or caching transparently.

## Example of Proxy Pattern in TypeScript

### Step 1: Subject Interface

```typescript
interface Image {
  display(): void;
}
```

### Step 2: Real Subject

```typescript
class RealImage implements Image {
  private filename: string;

  constructor(filename: string) {
    this.filename = filename;
    this.loadFromDisk();
  }

  private loadFromDisk(): void {
    console.log(`Loading ${this.filename} from disk.`);
  }

  display(): void {
    console.log(`Displaying ${this.filename}`);
  }
}
```

### Step 3: Proxy Class

```typescript
class ProxyImage implements Image {
  private realImage: RealImage | null = null;
  private filename: string;

  constructor(filename: string) {
    this.filename = filename;
  }

  display(): void {
    if (this.realImage === null) {
      this.realImage = new RealImage(this.filename);
    }
    this.realImage.display();
  }
}
```

### Step 4: Using Proxy

```typescript
const image = new ProxyImage('test_image.jpg');

// Image will be loaded from disk only when display() is called for the first time
image.display();

// Image won't load from disk again
image.display();
```

### Output
```
Loading test_image.jpg from disk.
Displaying test_image.jpg
Displaying test_image.jpg
```

## Conclusion

The Proxy Pattern is an effective way to control access, implement lazy loading, or add additional functionalities transparently, enhancing the flexibility and performance of your application.