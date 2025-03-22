# Composite Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Composite Pattern?

The **Composite Pattern** allows you to treat individual objects and groups of objects uniformly by creating tree structures of objects. Clients can work consistently with both individual items and compositions of items.

## Why and When to Use the Composite Pattern?

### Benefits:
- **Uniformity**: Simplifies client interactions by treating single and composite objects uniformly.
- **Hierarchy Management**: Easily manage hierarchical structures.
- **Flexibility**: Add or remove objects dynamically.

### Use the Composite Pattern when:
- You have hierarchical structures of objects.
- You need to handle groups and individual items uniformly.

## Example of Composite Pattern in TypeScript

### Step 1: Define Component Interface

```typescript
interface FileSystemComponent {
  showDetails(indent?: string): void;
}
```

### Step 2: Leaf Components

```typescript
class File implements FileSystemComponent {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  showDetails(indent: string = ''): void {
    console.log(`${indent}- File: ${this.name}`);
  }
}
```

### Step 3: Composite Component

```typescript
class Folder implements FileSystemComponent {
  private name: string;
  private components: FileSystemComponent[] = [];

  constructor(name: string) {
    this.name = name;
  }

  add(component: FileSystemComponent): void {
    this.components.push(component);
  }

  showDetails(indent: string = ''): void {
    console.log(`${indent}+ Folder: ${this.name}`);
    this.components.forEach(c => c.showDetails(indent + '  '));
  }
}
```

### Step 4: Using the Composite

```typescript
const root = new Folder('root');
const home = new Folder('home');
const file1 = new File('file1.txt');
const file2 = new File('file2.txt');

home.add(file1);
root.add(home);
root.add(file2);

root.showDetails();
```

### Output
```
+ Folder: root
  + Folder: home
    - File: file1.txt
  - File: file2.txt
```

## Conclusion

The Composite Pattern simplifies managing hierarchical structures, allowing individual and composite objects to be treated uniformly, greatly improving code flexibility and maintainability.