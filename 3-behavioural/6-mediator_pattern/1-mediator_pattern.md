# Mediator Pattern in TypeScript

## What is the Mediator Pattern?

The **Mediator Pattern** defines an object that encapsulates how a set of objects interact, promoting loose coupling by preventing direct communication between objects and centralizing interactions.

## Why and When to Use the Mediator Pattern?

### Benefits:
- **Decoupling**: Objects communicate indirectly via mediator.
- **Simplified Communication**: Reduces direct interactions between multiple objects.
- **Maintainability**: Changes affect only the mediator.

### Use the Mediator Pattern when:
- Objects interact in complex ways.
- You want to centralize communication logic.

## Example of Mediator Pattern in TypeScript

### Step 1: Mediator Interface

```typescript
interface Mediator {
  notify(sender: Component, event: string): void;
}
```

### Step 2: Component Base Class

```typescript
class Component {
  protected mediator: Mediator;

  constructor(mediator: Mediator) {
    this.mediator = mediator;
  }
}
```

### Step 3: Concrete Components

```typescript
class Button extends Component {
  click(): void {
    console.log("Button clicked");
    this.mediator.notify(this, 'click');
  }
}

class Checkbox extends Component {
  check(): void {
    console.log("Checkbox checked");
    this.mediator.notify(this, 'check');
  }
}
```

### Step 4: Concrete Mediator

```typescript
class DialogMediator implements Mediator {
  private button: Button;
  private checkbox: Checkbox;

  constructor(button: Button, checkbox: Checkbox) {
    this.button = button;
    this.checkbox = checkbox;
  }

  notify(sender: Component, event: string): void {
    if (sender instanceof Button && event === 'click') {
      console.log("Mediator reacts to button click.");
    }
    if (sender instanceof Checkbox && event === 'check') {
      console.log("Mediator reacts to checkbox check.");
    }
  }
}
```

### Step 5: Using the Mediator Pattern

```typescript
const mediator = new DialogMediator(null!, null!);
const button = new Button(mediator);
const checkbox = new Checkbox(mediator);

// Updating mediator's references
mediator['button'] = button;
mediator['checkbox'] = checkbox;

button.click();
checkbox.check();
```

### Output
```
Button clicked
Mediator reacts to button click.
Checkbox checked
Mediator reacts to checkbox check.
```

## Conclusion

The Mediator Pattern centralizes communication logic, reducing dependencies between components and enhancing maintainability and flexibility.