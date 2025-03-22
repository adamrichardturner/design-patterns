# Memento Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Memento Pattern?

The **Memento Pattern** provides a way to capture an object's internal state without exposing its implementation details, enabling the state to be restored later, typically used for undo functionality.

## Why and When to Use the Memento Pattern?

### Benefits:
- **Encapsulation**: Protects object's internal state.
- **Undo Operations**: Easily restore previous states.

### Use the Memento Pattern when:
- You need to save snapshots of object states.
- Implementing undo functionalities.

## Example of Memento Pattern in TypeScript

### Step 1: Memento Class

```typescript
class Memento {
  private state: string;

  constructor(state: string) {
    this.state = state;
  }

  getState(): string {
    return this.state;
  }
}
```

### Step 2: Originator Class

```typescript
class Editor {
  private state: string = '';

  type(words: string): void {
    this.state += words;
  }

  save(): Memento {
    return new Memento(this.state);
  }

  restore(memento: Memento): void {
    this.state = memento.getState();
  }

  print(): void {
    console.log(this.state);
  }
}
```

### Step 3: Caretaker Class

```typescript
class History {
  private states: Memento[] = [];

  push(memento: Memento): void {
    this.states.push(memento);
  }

  pop(): Memento | undefined {
    return this.states.pop();
  }
}
```

### Step 4: Using the Memento Pattern

```typescript
const editor = new Editor();
const history = new History();

editor.type("First sentence. ");
history.push(editor.save());

editor.type("Second sentence. ");
history.push(editor.save());

editor.type("Third sentence.");
editor.print(); // First sentence. Second sentence. Third sentence.

editor.restore(history.pop()!);
editor.print(); // First sentence. Second sentence.

editor.restore(history.pop()!);
editor.print(); // First sentence.
```

### Output
```
First sentence. Second sentence. Third sentence.
First sentence. Second sentence.
First sentence.
```

## Conclusion

The Memento Pattern effectively manages object states, allowing easy state restoration and implementing undo functionalities without breaking encapsulation.