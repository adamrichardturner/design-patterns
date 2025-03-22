# State Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the State Pattern?

The **State Pattern** allows an object to alter its behavior when its internal state changes. The object will appear to change its class based on the state it currently holds.

## Why and When to Use the State Pattern?

### Benefits:
- **Clear structure**: Easy to manage state-specific behaviors.
- **Simplifies logic**: Avoid complex conditional statements.

### Use the State Pattern when:
- An object's behavior depends heavily on its state.
- State-specific logic is complex.

## Example of State Pattern in TypeScript

### Step 1: State Interface

```typescript
interface State {
  handle(context: Context): void;
}
```

### Step 2: Concrete States

```typescript
class ConcreteStateA implements State {
  handle(context: Context): void {
    console.log("State A handled. Switching to State B.");
    context.setState(new ConcreteStateB());
  }
}

class ConcreteStateB implements State {
  handle(context: Context): void {
    console.log("State B handled. Switching to State A.");
    context.setState(new ConcreteStateA());
  }
}
```

### Step 3: Context Class

```typescript
class Context {
  private state: State;

  constructor(state: State) {
    this.state = state;
  }

  setState(state: State): void {
    this.state = state;
  }

  request(): void {
    this.state.handle(this);
  }
}
```

### Step 4: Using the State Pattern

```typescript
const context = new Context(new ConcreteStateA());

context.request(); // Switches to State B
context.request(); // Switches to State A
context.request(); // Switches to State B
```

### Output
```
State A handled. Switching to State B.
State B handled. Switching to State A.
State A handled. Switching to State B.
```

## Conclusion

The State Pattern effectively organizes state-specific behaviors, making state transitions clear and manageable.