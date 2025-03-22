# Chain of Responsibility Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Chain of Responsibility Pattern?

The **Chain of Responsibility Pattern** allows you to pass requests along a chain of handlers. Each handler decides either to process the request or to pass it to the next handler in the chain. This pattern promotes loose coupling between sender and receiver.

## Why and When to Use the Chain of Responsibility Pattern?

### Benefits:
- **Decoupling**: Sender and receiver have minimal direct interaction.
- **Flexibility**: You can add or reorder handlers dynamically.
- **Single Responsibility Principle**: Each handler focuses on a single task.

### Use the Chain of Responsibility Pattern when:
- Multiple objects can handle a request.
- You want to dynamically determine which handler processes the request.
- You need to decouple the request sender from its receivers.

## Example of Chain of Responsibility Pattern in TypeScript

### Step 1: Handler Interface

```typescript
interface Handler {
  setNext(handler: Handler): Handler;
  handle(request: string): string | null;
}
```

### Step 2: Abstract Handler

```typescript
abstract class AbstractHandler implements Handler {
  private nextHandler: Handler | null = null;

  setNext(handler: Handler): Handler {
    this.nextHandler = handler;
    return handler;
  }

  handle(request: string): string | null {
    if (this.nextHandler) {
      return this.nextHandler.handle(request);
    }
    return null;
  }
}
```

### Step 3: Concrete Handlers

```typescript
class MonkeyHandler extends AbstractHandler {
  handle(request: string): string | null {
    if (request === "Banana") {
      return `Monkey: I'll eat the ${request}.`;
    }
    return super.handle(request);
  }
}

class SquirrelHandler extends AbstractHandler {
  handle(request: string): string | null {
    if (request === "Nut") {
      return `Squirrel: I'll eat the ${request}.`;
    }
    return super.handle(request);
  }
}

class DogHandler extends AbstractHandler {
  handle(request: string): string | null {
    if (request === "Bone") {
      return `Dog: I'll eat the ${request}.`;
    }
    return super.handle(request);
  }
}
```

### Step 4: Using the Chain of Responsibility

```typescript
const monkey = new MonkeyHandler();
const squirrel = new SquirrelHandler();
const dog = new DogHandler();

monkey.setNext(squirrel).setNext(dog);

function clientRequest(handler: Handler, food: string) {
  console.log(`Who wants a ${food}?`);

  const result = handler.handle(food);
  if (result) {
    console.log(result);
  } else {
    console.log(`${food} was left untouched.`);
  }
}

clientRequest(monkey, "Nut");
clientRequest(monkey, "Banana");
clientRequest(monkey, "Bone");
clientRequest(monkey, "Apple");
```

### Output
```
Who wants a Nut?
Squirrel: I'll eat the Nut.
Who wants a Banana?
Monkey: I'll eat the Banana.
Who wants a Bone?
Dog: I'll eat the Bone.
Who wants an Apple?
Apple was left untouched.
```

## Conclusion

The Chain of Responsibility Pattern allows dynamic handling of requests, providing flexibility and maintaining a clear separation between the sender and receivers.

