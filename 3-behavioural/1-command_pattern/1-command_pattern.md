# Command Design Pattern in TypeScript

[« Back to Project Readme](../../../README.md)

## What is the Command Pattern?

The **Command Pattern** encapsulates a request as an object, enabling you to parameterize methods with different requests, delay their execution, queue or log them, and support undoable operations.

## Why and When to Use the Command Pattern?

### Benefits:
- **Decoupling**: Separates sender and receiver of commands.
- **Flexibility**: Easily support operations like undo, redo, and command logging.
- **Extensibility**: Introduce new commands without changing existing code.

### Use the Command Pattern when:
- You need commands executed later or queued.
- You require an undo/redo functionality.
- You want to decouple the invoker from the receiver.

## Example of Command Pattern in TypeScript

### Step 1: Define the Command Interface

```typescript
interface Command {
  execute(): void;
  undo(): void;
}
```

### Step 2: Receiver (the actual business logic)

```typescript
class Light {
  private isOn = false;

  turnOn(): void {
    this.isOn = true;
    console.log("The light is on");
  }

  turnOff(): void {
    this.isOn = false;
    console.log("The light is off");
  }
}
```

### Step 3: Concrete Commands

```typescript
class LightOnCommand implements Command {
  private light: Light;

  constructor(light: Light) {
    this.light = light;
  }

  execute(): void {
    this.light.turnOn();
  }

  undo(): void {
    this.light.turnOff();
  }
}

class LightOffCommand implements Command {
  private light: Light;

  constructor(light: Light) {
    this.light = light;
  }

  execute(): void {
    this.light.turnOff();
  }

  undo(): void {
    this.light.turnOn();
  }
}
```

### Step 4: Invoker

```typescript
class RemoteControl {
  private history: Command[] = [];

  executeCommand(command: Command): void {
    command.execute();
    this.history.push(command);
  }

  undo(): void {
    const command = this.history.pop();
    if (command) {
      command.undo();
    }
  }
}
```

### Step 5: Using the Command Pattern

```typescript
const light = new Light();
const remoteControl = new RemoteControl();

const lightOn = new LightOnCommand(light);
const lightOff = new LightOffCommand(light);

remoteControl.executeCommand(lightOn);  // Output: The light is on
remoteControl.executeCommand(lightOff); // Output: The light is off

remoteControl.undo();                   // Output: The light is on
remoteControl.undo();                   // Output: The light is off
```

## Conclusion

The Command Pattern effectively encapsulates operations as objects, allowing greater flexibility, decoupling, and easy management of actions such as undo and redo.