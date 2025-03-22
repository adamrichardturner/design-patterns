# Adapter Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Adapter Pattern?

The **Adapter Pattern** allows incompatible interfaces to collaborate by providing a wrapper that translates requests from one interface to another. It helps integrate existing classes or modules without modifying their original code.

## Why and When to Use the Adapter Pattern?

### Benefits:
- **Compatibility**: Lets incompatible interfaces work together.
- **Reusability**: Enables reuse of existing classes or components.
- **Single Responsibility Principle**: Keeps translation logic separate from business logic.

### Use the Adapter Pattern when:
- You want to reuse existing code with an incompatible interface.
- Integrating legacy code or third-party libraries that don't match your interface.

## Example of Adapter Pattern in TypeScript

### Step 1: Existing Class with Incompatible Interface

```typescript
class OldPrinter {
  oldPrint(text: string): void {
    console.log(`Old Printer printing: ${text}`);
  }
}
```

### Step 2: Define Target Interface

```typescript
interface Printer {
  print(text: string): void;
}
```

### Step 3: Create Adapter Class

```typescript
class PrinterAdapter implements Printer {
  private oldPrinter: OldPrinter;

  constructor(oldPrinter: OldPrinter) {
    this.oldPrinter = oldPrinter;
  }

  print(text: string): void {
    this.oldPrinter.oldPrint(text);
  }
}
```

### Step 4: Using the Adapter

```typescript
const oldPrinter = new OldPrinter();
const adapter: Printer = new PrinterAdapter(oldPrinter);

adapter.print("Hello, Adapter Pattern!");
```

### Output
```
Old Printer printing: Hello, Adapter Pattern!
```

## Conclusion

The Adapter Pattern bridges the gap between incompatible interfaces, enhancing compatibility and reuse of existing components without modifying their original implementations.