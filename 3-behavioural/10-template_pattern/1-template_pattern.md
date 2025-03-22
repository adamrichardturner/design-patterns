# Template Method Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Template Method Pattern?

The **Template Method Pattern** defines the skeleton of an algorithm in a method, deferring some steps to subclasses. It lets subclasses redefine certain steps without altering the algorithm's structure.

## Why and When to Use the Template Method Pattern?

### Benefits:
- **Reusability**: Common algorithm structure is reused.
- **Extensibility**: Easy to extend specific steps.

### Use the Template Method Pattern when:
- You want to define a standard procedure but allow customization.
- Common steps are consistent across implementations.

## Example of Template Method Pattern in TypeScript

### Step 1: Abstract Class (Template)

```typescript
abstract class Game {
  play(): void {
    this.start();
    this.playGame();
    this.end();
  }

  protected abstract start(): void;
  protected abstract playGame(): void;
  protected abstract end(): void;
}
```

### Step 2: Concrete Implementations

```typescript
class Football extends Game {
  protected start(): void {
    console.log("Football game started!");
  }

  protected playGame(): void {
    console.log("Playing football...");
  }

  protected end(): void {
    console.log("Football game finished!");
  }
}

class Basketball extends Game {
  protected start(): void {
    console.log("Basketball game started!");
  }

  protected playGame(): void {
    console.log("Playing basketball...");
  }

  protected end(): void {
    console.log("Basketball game finished!");
  }
}
```

### Step 3: Using the Template Method Pattern

```typescript
const football = new Football();
football.play();

const basketball = new Basketball();
basketball.play();
```

### Output
```
Football game started!
Playing football...
Football game finished!

Basketball game started!
Playing basketball...
Basketball game finished!
```

## Conclusion

The Template Method Pattern provides a clear, reusable structure, making algorithms easy to manage and extend.