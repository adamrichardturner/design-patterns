# Facade Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Facade Pattern?

The **Facade Pattern** provides a simplified interface to a complex subsystem. It encapsulates complex interactions and exposes a straightforward API, making subsystems easier to use and understand.

## Why and When to Use the Facade Pattern?

### Benefits:
- **Simplified Interface**: Provides a clear and easy-to-use API.
- **Reduced Complexity**: Hides subsystem complexities from clients.
- **Improved Maintainability**: Makes subsystems easier to use and maintain.

### Use the Facade Pattern when:
- You want to simplify interaction with complex systems.
- You need a single entry point to a subsystem.
- You want to reduce dependencies and improve readability.

## Example of Facade Pattern in TypeScript

### Step 1: Create Complex Subsystem Classes

```typescript
class CPU {
  freeze(): void {
    console.log("CPU freeze.");
  }

  jump(position: number): void {
    console.log(`CPU jump to position ${position}.`);
  }

  execute(): void {
    console.log("CPU execute.");
  }
}

class Memory {
  load(position: number, data: string): void {
    console.log(`Memory loading data '${data}' into position ${position}.`);
  }
}

class HardDrive {
  read(sector: number, size: number): string {
    return `Data from sector ${sector}, size ${size}`;
  }
}
```

### Step 2: Implement the Facade Class

```typescript
class ComputerFacade {
  private cpu: CPU;
  private memory: Memory;
  private hardDrive: HardDrive;

  constructor() {
    this.cpu = new CPU();
    this.memory = new Memory();
    this.hardDrive = new HardDrive();
  }

  start(): void {
    this.cpu.freeze();
    const data = this.hardDrive.read(0, 1024);
    this.memory.load(0, data);
    this.cpu.jump(0);
    this.cpu.execute();
  }
}
```

### Step 3: Using the Facade

```typescript
const computer = new ComputerFacade();
computer.start();
```

### Output
```
CPU freeze.
Memory loading data 'Data from sector 0, size 1024' into position 0.
CPU jump to position 0.
CPU execute.
```

## Conclusion

The Facade Pattern simplifies complex interactions by providing a clear and intuitive interface, enhancing usability and maintainability in complex applications.