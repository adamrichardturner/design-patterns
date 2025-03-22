# TypeScript Fundamentals for Understanding Design Patterns

[« Back to Project README](../README.md)

This guide provides essential TypeScript concepts and features necessary to effectively understand and implement software design patterns. 

It covers foundational concepts and provides clear examples.

---

## Table of Contents

1. [TypeScript Overview](#typescript-overview)
2. [Basic Types](#basic-types)
3. [Interfaces](#interfaces)
4. [Classes](#classes)
5. [Abstract Classes](#abstract-classes)
6. [Inheritance and Polymorphism](#inheritance-and-polymorphism)
7. [Generics](#generics)
8. [Encapsulation](#encapsulation)
9. [Access Modifiers](#access-modifiers)
10. [Type Assertions](#type-assertions)
11. [Modules](#modules)
12. [Advanced Types](#advanced-types)

---

## TypeScript Overview

**TypeScript** is a superset of JavaScript that adds static type checking and other features to enhance developer productivity and code quality.

### Key Features

- **Static Type Checking**: Catches type-related errors during development rather than at runtime
- **Enhanced IDE Support**: Provides better code completion, navigation, and refactoring tools
- **ECMAScript Compatibility**: Supports the latest JavaScript features while adding its own extensions
- **Gradual Typing**: Allows you to adopt TypeScript incrementally by mixing typed and untyped code
- **Type Inference**: Automatically determines types when not explicitly declared
- **Interfaces and Type Aliases**: Defines custom types for complex objects and functions
- **Generics**: Enables the creation of reusable components that work with a variety of types
- **Tooling**: Includes a powerful compiler (tsc) with many configuration options

### TypeScript vs JavaScript

| Feature | TypeScript | JavaScript |
|---------|------------|------------|
| Type System | Static | Dynamic |
| Compilation | Requires compilation to JavaScript | Runs directly in browsers/Node.js |
| Error Detection | Compile-time | Runtime |
| Language Features | Superset (includes all JS features plus more) | Standard ECMAScript |
| IDE Support | Rich autocompletion and type checking | Limited, depends on JSDoc |

### Compilation Process

```
TypeScript Code (.ts) → TypeScript Compiler (tsc) → JavaScript Code (.js)
```

Example:
```typescript
// TypeScript code (app.ts)
function greet(name: string): string {
  return `Hello, ${name}!`;
}

const user = "TypeScript Developer";
console.log(greet(user));
```

Compiles to:
```javascript
// JavaScript code (app.js)
function greet(name) {
  return `Hello, ${name}!`;
}

const user = "TypeScript Developer";
console.log(greet(user));
```

### When to Use TypeScript

- **Large-scale applications**: Provides better structure and maintainability
- **Team environments**: Improves collaboration through clear type contracts
- **Complex domains**: Makes complicated business logic more understandable
- **Libraries and frameworks**: Offers better documentation through types
- **Refactoring**: Makes code changes safer and more predictable

---

## Basic Types

TypeScript provides a rich set of primitive and complex types to describe various kinds of data.

### Primitive Types

#### Boolean

```typescript
let isDone: boolean = false;
let isActive: boolean = true;
```

- Used for true/false values
- Logical operators: `&&` (AND), `||` (OR), `!` (NOT)

#### Number

```typescript
// Decimal
let decimal: number = 10;

// Binary
let binary: number = 0b1010;

// Octal
let octal: number = 0o744;

// Hexadecimal
let hex: number = 0xf00d;

// Big integers
let big: bigint = 100n;

// Operations
let sum: number = 10 + 5;  // 15
let product: number = 10 * 5;  // 50
```

- Represents both integers and floating-point values
- Supports decimal, binary, octal, and hexadecimal literals
- Special values: `NaN`, `Infinity`

#### String

```typescript
// String literals
let firstName: string = "John";
let lastName: string = 'Doe';

// Template literals (string interpolation)
let fullName: string = `${firstName} ${lastName}`;

// Multi-line strings
let multiLine: string = `
  This is a
  multi-line
  string
`;

// String methods
let uppercased: string = firstName.toUpperCase();  // "JOHN"
let includes: boolean = fullName.includes("John");  // true
```

- Represents textual data
- Can use single quotes (`'`), double quotes (`"`), or backticks (`` ` ``)
- Template literals allow for string interpolation and multi-line strings
- Rich set of string manipulation methods

#### Symbol

```typescript
// Create unique symbols
let sym1: symbol = Symbol();
let sym2: symbol = Symbol("key");
let sym3: symbol = Symbol("key");

// Symbols are always unique
console.log(sym2 === sym3);  // false
```

- Creates unique identifiers
- Commonly used as property keys in objects to avoid name collisions

#### Null and Undefined

```typescript
let u: undefined = undefined;
let n: null = null;

// With strictNullChecks: false
let str: string = null;  // Valid

// With strictNullChecks: true
let strictStr: string = null;  // Error
let nullableStr: string | null = null;  // Valid
```

- `null` represents an intentional absence of value
- `undefined` represents an uninitialized value
- Behavior depends on `strictNullChecks` compiler option

### Complex Types

#### Arrays

```typescript
// Using array type syntax
let numbers: number[] = [1, 2, 3, 4, 5];

// Using generic array type
let strings: Array<string> = ["Hello", "World"];

// Multi-dimensional arrays
let matrix: number[][] = [
  [1, 2, 3],
  [4, 5, 6]
];

// Array methods
numbers.push(6);  // [1, 2, 3, 4, 5, 6]
let firstItem: number = numbers[0];  // 1
let sum: number = numbers.reduce((a, b) => a + b, 0);  // 21
```

- Store multiple values of the same type
- Access elements by index (zero-based)
- Many built-in methods for manipulation: `push()`, `pop()`, `slice()`, etc.
- TypeScript enforces consistent element types

#### Tuples

```typescript
// Declare a tuple type
let tuple: [string, number, boolean] = ["hello", 42, true];

// Access individual elements
let message: string = tuple[0];  // "hello"
let answer: number = tuple[1];   // 42

// Destructuring
let [msg, ans, flag] = tuple;

// Optional tuple elements (TypeScript 4.0+)
type OptionalTuple = [string, number, boolean?];
let opt: OptionalTuple = ["hello", 42]; // The boolean is optional

// Rest elements
type RestTuple = [number, ...string[]];
let rest: RestTuple = [1, "a", "b", "c"];
```

- Fixed-length arrays where each position has a specific type
- Strict ordering of types
- Can destructure like arrays
- Support optional elements and rest elements (TypeScript 4.0+)

#### Enums

```typescript
// Numeric enums (default)
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}

// Custom numeric values
enum HttpStatus {
  OK = 200,
  Created = 201,
  BadRequest = 400,
  Unauthorized = 401
}

// String enums
enum MediaTypes {
  JSON = "application/json",
  XML = "application/xml",
  TEXT = "text/plain"
}

// Usage
let dir: Direction = Direction.Up;
let status: HttpStatus = HttpStatus.OK;
console.log(HttpStatus[200]);  // "OK" (reverse mapping)
```

- Groups of related constants
- Types: numeric (default), string, heterogeneous
- Support reverse mapping (numeric enums only)
- Compiled to efficient JavaScript

#### Any

```typescript
// Variables of type any
let notSure: any = 4;
notSure = "maybe a string";
notSure = false;

// Any in arrays
let items: any[] = [1, "string", false, {}, []];

// Operations on any
notSure.toFixed();  // No error, even if notSure isn't a number
```

- Opts out of type checking for a variable
- Useful for migrating JavaScript or working with dynamic content
- Should be avoided when possible for type safety

#### Unknown

```typescript
// Variables of type unknown
let value: unknown = 30;
value = "hello";
value = true;

// Must perform type checking before operations
if (typeof value === "string") {
  console.log(value.toUpperCase());  // "HELLO"
}

// Type assertion
let strLength: number = (value as string).length;
```

- Type-safe alternative to `any`
- Cannot perform operations without type checking or assertion
- Better for representing truly unknown values

#### Void

```typescript
// Function that returns void
function logMessage(message: string): void {
  console.log(message);
}

// Variable of type void (limited usefulness)
let unusable: void = undefined;
```

- Represents the absence of a value
- Primarily used as a function return type
- Variables of type `void` can only be `undefined` or `null` (with `strictNullChecks: false`)

#### Never

```typescript
// Function that never returns
function throwError(message: string): never {
  throw new Error(message);
}

// Function with unreachable end point
function infiniteLoop(): never {
  while (true) {}
}

// Used in exhaustive type checking
type Shape = Circle | Square;

function assertNever(value: never): never {
  throw new Error(`Unexpected value: ${value}`);
}

function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius ** 2;
  } else if (shape.kind === "square") {
    return shape.sideLength ** 2;
  } else {
    // Will catch if new shapes are added without updating this function
    return assertNever(shape);
  }
}
```

- Represents values that never occur
- Used for functions that never return normally (throw errors or run forever)
- Useful in exhaustive type checking patterns

#### Object

```typescript
// Object type
let obj: object = { key: "value" };

// More specific object types
let person: { name: string; age: number } = {
  name: "John",
  age: 30
};

// Optional properties
let config: { debug?: boolean; timeout: number } = {
  timeout: 5000
  // debug is optional
};

// Index signatures
let dictionary: { [key: string]: number } = {
  "one": 1,
  "two": 2
};
```

- Represents non-primitive types (anything that is not `number`, `string`, `boolean`, `symbol`, `null`, or `undefined`)
- Can specify exact object shapes with property types
- Supports optional properties and index signatures

### Type Aliases and Literal Types

#### Type Aliases

```typescript
// Simple type alias
type ID = string | number;

// Object type alias
type Point = {
  x: number;
  y: number;
};

// Function type alias
type MathOperation = (x: number, y: number) => number;

// Union with different object shapes
type Shape = 
  | { kind: "circle"; radius: number }
  | { kind: "square"; sideLength: number };

// Usage
let id: ID = "abc123";
let point: Point = { x: 10, y: 20 };
let add: MathOperation = (a, b) => a + b;
```

- Creates named types that can be reused
- Can represent simple or complex types
- Does not create new types, just names for existing ones

#### Literal Types

```typescript
// String literal types
type Direction = "north" | "south" | "east" | "west";
let dir: Direction = "north";  // Valid
let invalid: Direction = "up"; // Error

// Numeric literal types
type DiceRoll = 1 | 2 | 3 | 4 | 5 | 6;
let roll: DiceRoll = 6;  // Valid
let invalid: DiceRoll = 7;  // Error

// Boolean literal types
type Bool = true;  // Can only be true
let t: Bool = true;  // Valid
let f: Bool = false;  // Error

// Combined with other types
type Status = "success" | "error" | number;
let response: Status = "success";  // Valid
let code: Status = 404;  // Also valid
```

- Specific, exact values that a type can have
- Types: string literals, numeric literals, boolean literals
- Often combined with unions to create enum-like types
- Provides compile-time checking of allowed values

### Type Assertions

```typescript
// Angle bracket syntax (not usable in JSX)
let someValue: unknown = "this is a string";
let strLength1: number = (<string>someValue).length;

// as syntax (preferred)
let strLength2: number = (someValue as string).length;

// Assertions to narrower types
interface Person {
  name: string;
  age: number;
}

let obj: object = { name: "John", age: 30 };
let person = obj as Person;

// Non-null assertion operator
function getElement(id: string) {
  // Tell TypeScript that getElementById will not return null
  const element = document.getElementById(id)!;
  element.innerHTML = "Hello";  // No error
}
```

- Tell the compiler to treat a value as a specific type
- Does not change runtime behavior or perform runtime checks
- Two syntaxes: angle brackets and `as` keyword
- Cannot assert to any arbitrary type without multiple steps

---

## Interfaces

Interfaces define the structure that objects must conform to, serving as contracts for your code.

### Basic Interface Declaration

```typescript
interface Person {
  name: string;
  age: number;
}

// Object implementing the interface
const john: Person = { 
  name: 'John', 
  age: 30 
};

// Function parameter using interface
function greet(person: Person): string {
  return `Hello, ${person.name}! You are ${person.age} years old.`;
}
```

### Interface Features

#### Optional Properties

```typescript
interface Configuration {
  endpoint: string;
  timeout: number;
  retries?: number;  // Optional property
  debug?: boolean;   // Optional property
}

// Valid implementations
const config1: Configuration = { endpoint: 'api/data', timeout: 3000 };
const config2: Configuration = { endpoint: 'api/data', timeout: 3000, retries: 3 };
const config3: Configuration = { endpoint: 'api/data', timeout: 3000, debug: true };
```

- Optional properties are marked with a question mark (`?`)
- Objects don't need to include optional properties to satisfy the interface

#### Readonly Properties

```typescript
interface Point {
  readonly x: number;
  readonly y: number;
}

const origin: Point = { x: 0, y: 0 };
// origin.x = 10;  // Error: Cannot assign to 'x' because it is a read-only property
```

- Readonly properties can only be set when the object is first created
- Prevents properties from being modified after initialization
- Similar to `const` for variables but for object properties

#### Method Signatures

```typescript
interface Calculator {
  add(a: number, b: number): number;
  subtract(a: number, b: number): number;
  multiply?(a: number, b: number): number;  // Optional method
}

// Implementation
const basicCalc: Calculator = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};

const advancedCalc: Calculator = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b,
  multiply: (a, b) => a * b
};
```

- Interfaces can include method signatures
- Methods can be required or optional
- No implementation details, only the method signature

#### Index Signatures

```typescript
interface StringDictionary {
  [key: string]: string;
}

const colors: StringDictionary = {
  red: '#FF0000',
  green: '#00FF00',
  blue: '#0000FF'
};

// Access with any string key
console.log(colors['red']);    // #FF0000
console.log(colors.blue);      // #0000FF

// Mixed properties and index signatures
interface StringNumberDictionary {
  [key: string]: number;
  length: number;   // Must be compatible with the index signature type
  // name: string;  // Error: Property 'name' of type 'string' is not assignable to 'string' index type 'number'
}
```

- Allow objects to have a variable number of properties
- Specify the type of property names and their corresponding values
- Properties explicitly declared must match the index signature type

#### Interface Extension

```typescript
// Extending a single interface
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
  bark(): void;
}

const dog: Dog = {
  name: 'Rex',
  breed: 'German Shepherd',
  bark: () => console.log('Woof!')
};

// Extending multiple interfaces
interface Swimmer {
  swim(): void;
}

interface Flyer {
  fly(): void;
}

interface Duck extends Animal, Swimmer, Flyer {
  quack(): void;
}

const duck: Duck = {
  name: 'Donald',
  swim: () => console.log('Swimming...'),
  fly: () => console.log('Flying...'),
  quack: () => console.log('Quack!')
};
```

- Interfaces can extend one or more other interfaces
- Combines all the properties and methods from the base interfaces
- Allows for composition and code reuse
- Can override property types from base interfaces with more specific types

#### Interface vs. Type Alias

```typescript
// Interface
interface User {
  name: string;
  email: string;
}

// Adding more properties later
interface User {
  age: number;
}

// Type alias
type Person = {
  name: string;
  email: string;
};

// Cannot add more properties later to a type alias
// type Person = { age: number; };  // Error: Duplicate identifier 'Person'
```

**Interfaces**
- Can be extended with new properties after declaration
- Can extend other interfaces and can be extended by other interfaces
- Better for defining public APIs and object shapes
- Cannot represent primitives or unions directly

**Type Aliases**
- Cannot be changed after declaration
- Can represent unions, intersections, primitives, and tuples
- More flexible but less extensible

#### Implementing Interfaces in Classes

```typescript
interface Vehicle {
  start(): void;
  stop(): void;
}

class Car implements Vehicle {
  // Must implement all interface methods
  start(): void {
    console.log('Car started');
  }
  
  stop(): void {
    console.log('Car stopped');
  }
  
  // Can add additional methods
  honk(): void {
    console.log('Beep!');
  }
}
```

- Classes can implement one or more interfaces
- Must provide implementations for all interface members
- Can add additional properties and methods
- Creates a contract that classes must follow

#### Function Interfaces

```typescript
// Interface describing a function
interface Comparator<T> {
  (a: T, b: T): number;
}

// Function conforming to the interface
const numberComparator: Comparator<number> = (a, b) => {
  return a - b;
};

// Using the function interface
function sort<T>(array: T[], comparator: Comparator<T>): T[] {
  // Implementation of sorting
  return [...array].sort(comparator);
}

const numbers = [3, 1, 4, 1, 5, 9];
const sortedNumbers = sort(numbers, numberComparator);
```

- Interfaces can describe function types
- Useful for callbacks, event handlers, and strategy patterns
- Can be combined with generics for type-safe function interfaces

---

## Classes

Classes are blueprints for creating objects with specific properties and methods, supporting object-oriented programming principles.

### Class Basics

```typescript
class Person {
  // Properties
  name: string;
  age: number;

  // Constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // Methods
  greet(): string {
    return `Hello, my name is ${this.name} and I am ${this.age} years old.`;
  }
  
  // Method with parameters
  celebrateBirthday(): void {
    this.age++;
    console.log(`Happy birthday! ${this.name} is now ${this.age} years old.`);
  }
}

// Creating instances
const alice = new Person('Alice', 28);
console.log(alice.greet());  // Hello, my name is Alice and I am 28 years old.

alice.celebrateBirthday();  // Happy birthday! Alice is now 29 years old.
```

### Access Modifiers

```typescript
class BankAccount {
  // Public property - accessible from anywhere (default)
  public accountHolder: string;
  
  // Private property - only accessible within the class
  private balance: number;
  
  // Protected property - accessible within the class and subclasses
  protected accountNumber: string;
  
  constructor(accountHolder: string, initialBalance: number) {
    this.accountHolder = accountHolder;
    this.balance = initialBalance;
    this.accountNumber = 'ACC' + Math.floor(Math.random() * 1000000);
  }
  
  // Public method
  public deposit(amount: number): void {
    if (amount <= 0) {
      throw new Error('Deposit amount must be positive');
    }
    this.balance += amount;
  }
  
  // Public method
  public withdraw(amount: number): boolean {
    if (amount <= 0) {
      throw new Error('Withdrawal amount must be positive');
    }
    
    if (this.balance < amount) {
      return false;  // Insufficient funds
    }
    
    this.balance -= amount;
    return true;
  }
  
  // Public method to check balance
  public getBalance(): number {
    return this.balance;
  }
  
  // Private method
  private generateStatement(): string {
    return `Account: ${this.accountNumber}\nHolder: ${this.accountHolder}\nBalance: $${this.balance.toFixed(2)}`;
  }
  
  // Public method that uses a private method
  public printStatement(): void {
    console.log(this.generateStatement());
  }
}

const account = new BankAccount('John Doe', 1000);
account.deposit(500);
console.log(account.getBalance());  // 1500
account.withdraw(200);
console.log(account.getBalance());  // 1300

// Error: Property 'balance' is private and only accessible within class 'BankAccount'
// console.log(account.balance);

// Error: Property 'accountNumber' is protected and only accessible within class 'BankAccount' and its subclasses
// console.log(account.accountNumber);

// Error: Property 'generateStatement' is private and only accessible within class 'BankAccount'
// account.generateStatement();
```

### Parameter Properties

```typescript
class Point {
  // Parameter properties - shorthand for declaring and initializing properties
  constructor(
    public x: number,
    public y: number,
    private readonly id: string = 'default'
  ) {
    // No need to manually assign this.x = x, etc.
  }
  
  getPosition(): string {
    return `(${this.x}, ${this.y})`;
  }
  
  getId(): string {
    return this.id;
  }
}

const point = new Point(10, 20, 'point-1');
console.log(point.x);  // 10
console.log(point.getPosition());  // (10, 20)
console.log(point.getId());  // point-1

// error: Property 'id' is private and only accessible within class 'Point'
// console.log(point.id);
```

- Parameter properties combine declaration and initialization in the constructor
- Reduce boilerplate code
- Can use access modifiers (public, private, protected)
- Can use readonly modifier

### Getters and Setters

```typescript
class Circle {
  private _radius: number;
  
  constructor(radius: number) {
    this._radius = radius;
  }
  
  // Getter - accessed like a property
  get radius(): number {
    return this._radius;
  }
  
  // Setter - with validation
  set radius(value: number) {
    if (value <= 0) {
      throw new Error('Radius must be positive');
    }
    this._radius = value;
  }
  
  // Computed property
  get area(): number {
    return Math.PI * this._radius ** 2;
  }
  
  get diameter(): number {
    return this._radius * 2;
  }
}

const circle = new Circle(5);
console.log(circle.radius);  // 5
console.log(circle.area);    // 78.54...

circle.radius = 10;
console.log(circle.radius);  // 10
console.log(circle.area);    // 314.16...

// Throws: Radius must be positive
// circle.radius = -5;
```

- Getters allow controlled access to properties
- Setters allow validation before setting property values
- Accessed like properties, not methods (no parentheses)
- Can create computed properties with getters

### Static Members

```typescript
class MathUtils {
  // Static property
  static readonly PI: number = 3.14159265359;
  
  // Static method
  static square(x: number): number {
    return x * x;
  }
  
  // Static method
  static cube(x: number): number {
    return x * x * x;
  }
  
  // Static method using another static method
  static areaOfCircle(radius: number): number {
    return MathUtils.PI * MathUtils.square(radius);
  }
  
  // Instance method that uses static members
  calculateCircumference(radius: number): number {
    return 2 * MathUtils.PI * radius;
  }
}

// Accessing static members without creating an instance
console.log(MathUtils.PI);  // 3.14159265359
console.log(MathUtils.square(4));  // 16
console.log(MathUtils.areaOfCircle(5));  // 78.5398...

// Instance method requires an instance
const utils = new MathUtils();
console.log(utils.calculateCircumference(5));  // 31.4159...
```

- Static members belong to the class itself, not instances
- Accessed using the class name: `ClassName.staticMember`
- Useful for utility functions and constants
- Static methods can use other static methods and properties
- Instance methods can access static members via the class name

### This and Arrow Functions

```typescript
class Counter {
  count: number = 0;
  
  // Regular method - 'this' depends on how it's called
  increment() {
    this.count++;
  }
  
  // Arrow function method - 'this' is lexically bound
  decrement = () => {
    this.count--;
  }
  
  // Method that demonstrates the issue with 'this'
  delayedIncrement() {
    setTimeout(function() {
      // 'this' is undefined in strict mode or the global object in non-strict mode
      // this.count++;  // Error: Cannot read property 'count' of undefined
    }, 1000);
    
    // Solution 1: Use an arrow function
    setTimeout(() => {
      this.count++;  // 'this' is correctly bound to the Counter instance
    }, 1000);
    
    // Solution 2: Store 'this' in a variable
    const self = this;
    setTimeout(function() {
      self.count++;  // Uses the stored reference
    }, 1000);
    
    // Solution 3: Use bind
    setTimeout(function() {
      this.count++;  // 'this' is bound to the Counter instance
    }.bind(this), 1000);
  }
}

const counter = new Counter();
counter.increment();
console.log(counter.count);  // 1

// Potential issue with 'this'
const incrementFn = counter.increment;
// incrementFn();  // Error: Cannot read property 'count' of undefined

// Arrow function methods work correctly even when detached
const decrementFn = counter.decrement;
decrementFn();  // Works correctly
console.log(counter.count);  // 0
```

- Regular methods: `this` depends on how the method is called
- Arrow function methods: `this` is lexically bound to the containing class instance
- Arrow function methods are created per instance (memory trade-off)
- Regular methods are shared among all instances (more memory efficient)

### Class Inheritance

```typescript
// Base class
class Animal {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  move(distance: number = 0): void {
    console.log(`${this.name} moved ${distance} meters.`);
  }
  
  makeSound(): void {
    console.log('Generic animal sound');
  }
}

// Derived class
class Dog extends Animal {
  breed: string;
  
  constructor(name: string, breed: string) {
    // Must call super() before accessing 'this'
    super(name);
    this.breed = breed;
  }
  
  // Override base class method
  makeSound(): void {
    console.log('Woof! Woof!');
  }
  
  // Call base class method and extend functionality
  move(distance: number = 5): void {
    console.log(`${this.name} the ${this.breed} is running...`);
    super.move(distance);
  }
  
  // Add new methods
  fetch(): void {
    console.log(`${this.name} is fetching the ball!`);
  }
}

const animal = new Animal('Generic animal');
animal.move(10);  // Generic animal moved 10 meters.
animal.makeSound();  // Generic animal sound

const dog = new Dog('Rex', 'German Shepherd');
dog.move();  // Rex the German Shepherd is running... Rex moved 5 meters.
dog.makeSound();  // Woof! Woof!
dog.fetch();  // Rex is fetching the ball!

// Polymorphism
const animals: Animal[] = [
  new Animal('Generic animal'),
  new Dog('Rex', 'German Shepherd')
];

animals.forEach(animal => {
  animal.move();
  animal.makeSound();
  
  // Cannot call Dog-specific methods on Animal reference
  // animal.fetch();  // Error: Property 'fetch' does not exist on type 'Animal'
});
```

- A class can extend one other class using the `extends` keyword
- The `super()` call in the constructor is required before accessing `this`
- Methods can be overridden in the derived class
- `super.methodName()` can be used to call the base class implementation
- Polymorphism allows treating derived class instances as their base class type

---

## Abstract Classes

Abstract classes serve as base classes that cannot be instantiated directly but provide a blueprint for derived classes.

### Basic Abstract Class

```typescript
// Abstract class
abstract class Shape {
  // Regular property
  color: string;
  
  constructor(color: string) {
    this.color = color;
  }
  
  // Abstract method - must be implemented by derived classes
  abstract area(): number;
  
  // Abstract method with parameters
  abstract perimeter(): number;
  
  // Regular method - available to all derived classes
  describe(): void {
    console.log(`This shape is ${this.color} and has an area of ${this.area()} square units.`);
  }
}

// Cannot instantiate an abstract class
// const shape = new Shape('red');  // Error

// Concrete derived class
class Circle extends Shape {
  radius: number;
  
  constructor(color: string, radius: number) {
    super(color);
    this.radius = radius;
  }
  
  // Implementation of the abstract area method
  area(): number {
    return Math.PI * this.radius ** 2;
  }
  
  // Implementation of the abstract perimeter method
  perimeter(): number {
    return 2 * Math.PI * this.radius;
  }
  
  // Additional method specific to Circle
  getDiameter(): number {
    return this.radius * 2;
  }
}

class Rectangle extends Shape {
  width: number;
  height: number;
  
  constructor(color: string, width: number, height: number) {
    super(color);
    this.width = width;
    this.height = height;
  }
  
  area(): number {
    return this.width * this.height;
  }
  
  perimeter(): number {
    return 2 * (this.width + this.height);
  }
  
  // Additional method specific to Rectangle
  isSquare(): boolean {
    return this.width === this.height;
  }
}

// Create instances of concrete classes
const circle = new Circle('blue', 5);
circle.describe();  // This shape is blue and has an area of 78.54... square units.
console.log(`Circle perimeter: ${circle.perimeter()}`);
console.log(`Circle diameter: ${circle.getDiameter()}`);

const rectangle = new Rectangle('green', 4, 6);
rectangle.describe();  // This shape is green and has an area of 24 square units.
console.log(`Rectangle perimeter: ${rectangle.perimeter()}`);
console.log(`Is rectangle a square? ${rectangle.isSquare()}`);

// Polymorphism with abstract classes
const shapes: Shape[] = [
  new Circle('red', 3),
  new Rectangle('yellow', 5, 5)
];

shapes.forEach(shape => {
  shape.describe();
  console.log(`Area: ${shape.area()}`);
  console.log(`Perimeter: ${shape.perimeter()}`);
});
```

### Key Features of Abstract Classes

- **Cannot be instantiated directly**: Abstract classes are meant to be extended by concrete classes
- **Can contain abstract methods**: Methods with no implementation that must be defined in derived classes
- **Can contain concrete methods**: Regular methods with implementations that are inherited by derived classes
- **Can contain properties**: Both regular and abstract properties
- **Can have constructors**: Though they cannot be called directly except via `super()` in derived classes

### Abstract Classes vs. Interfaces

```typescript
// Interface
interface Vehicle {
  start(): void;
  stop(): void;
}

// Abstract class
abstract class AbstractVehicle {
  // Properties
  protected make: string;
  protected model: string;
  
  constructor(make: string, model: string) {
    this.make = make;
    this.model = model;
  }
  
  // Abstract methods
  abstract start(): void;
  abstract stop(): void;
  
  // Concrete method
  getInfo(): string {
    return `${this.make} ${this.model}`;
  }
}

// Concrete class implementing an interface
class Bicycle implements Vehicle {
  start(): void {
    console.log('Start pedaling');
  }
  
  stop(): void {
    console.log('Stop pedaling');
  }
}

// Concrete class extending an abstract class
class Car extends AbstractVehicle {
  constructor(make: string, model: string) {
    super(make, model);
  }
  
  start(): void {
    console.log(`${this.getInfo()} engine started`);
  }
  
  stop(): void {
    console.log(`${this.getInfo()} engine stopped`);
  }
  
  // Additional method
  honk(): void {
    console.log('Beep!');
  }
}
```

**Abstract Classes**
- Can contain implementations for methods
- Can have properties with access modifiers
- Can have constructors
- A class can extend only one abstract class
- Good for creating shared behavior and state

**Interfaces**
- Cannot contain implementations
- Cannot have access modifiers
- Cannot have constructors
- A class can implement multiple interfaces
- Good for defining contracts without implementation details

### When to Use Abstract Classes

- When you want to share code among several related classes
- When the classes that extend the abstract class have many common methods or properties
- When you need to specify some default behavior but also enforce implementing specific methods
- When you need access modifiers for the properties (not available in interfaces)

### Abstract Class Inheritance Chain

```typescript
// Base abstract class
abstract class Media {
  title: string;
  
  constructor(title: string) {
    this.title = title;
  }
  
  abstract play(): void;
  
  displayInfo(): void {
    console.log(`Title: ${this.title}`);
  }
}

// Intermediate abstract class
abstract class AudioMedia extends Media {
  duration: number;
  
  constructor(title: string, duration: number) {
    super(title);
    this.duration = duration;
  }
  
  // Add new abstract method
  abstract adjustVolume(level: number): void;
  
  // Override and extend base method
  displayInfo(): void {
    super.displayInfo();
    console.log(`Duration: ${this.duration} seconds`);
  }
}

// Concrete class
class Song extends AudioMedia {
  artist: string;
  
  constructor(title: string, artist: string, duration: number) {
    super(title, duration);
    this.artist = artist;
  }
  
  // Implement abstract methods
  play(): void {
    console.log(`Playing song: ${this.title} by ${this.artist}`);
  }
  
  adjustVolume(level: number): void {
    console.log(`Adjusting volume to ${level}%`);
  }
  
  // Override and extend
  displayInfo(): void {
    super.displayInfo();
    console.log(`Artist: ${this.artist}`);
  }
}

// Another concrete class
class Podcast extends AudioMedia {
  host: string;
  
  constructor(title: string, host: string, duration: number) {
    super(title, duration);
    this.host = host;
  }
  
  play(): void {
    console.log(`Playing podcast: ${this.title} hosted by ${this.host}`);
  }
  
  adjustVolume(level: number): void {
    console.log(`Setting podcast volume to ${level}%`);
  }
}

// Using the classes
const song = new Song('Bohemian Rhapsody', 'Queen', 355);
song.displayInfo();
song.play();
song.adjustVolume(80);

const podcast = new Podcast('Tech Talk', 'John Doe', 1800);
podcast.displayInfo();
podcast.play();
podcast.adjustVolume(70);
```

- Abstract classes can extend other abstract classes
- Each level can add new abstract or concrete methods
- Each level can override methods from parent classes
- The final concrete class must implement all abstract methods from all levels

---

## Inheritance and Polymorphism

Inheritance and polymorphism are core principles in object-oriented programming that enable code reuse and flexibility.

### Inheritance

Inheritance allows a class to inherit properties and methods from another class, forming a parent-child relationship.

#### Basic Inheritance

```typescript
// Base (parent) class
class Animal {
  name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  eat(): void {
    console.log(`${this.name} is eating.`);
  }
  
  sleep(): void {
    console.log(`${this.name} is sleeping.`);
  }
}

// Derived (child) class
class Dog extends Animal {
  breed: string;
  
  constructor(name: string, breed: string) {
    super(name); // Call the parent constructor
    this.breed = breed;
  }
  
  bark(): void {
    console.log(`${this.name} is barking.`);
  }
}

// Usage
const dog = new Dog('Rex', 'German Shepherd');
dog.eat();   // Inherited method: Rex is eating.
dog.sleep(); // Inherited method: Rex is sleeping.
dog.bark();  // Dog-specific method: Rex is barking.
console.log(dog.breed); // Dog-specific property: German Shepherd
```

#### Method Overriding

```typescript
class Cat extends Animal {
  constructor(name: string) {
    super(name);
  }
  
  // Override the eat method from the parent class
  eat(): void {
    console.log(`${this.name} is eating fish.`);
  }
  
  // Add a new method
  meow(): void {
    console.log(`${this.name} says meow!`);
  }
}

const cat = new Cat('Whiskers');
cat.eat();  // Overridden method: Whiskers is eating fish.
cat.sleep(); // Inherited method: Whiskers is sleeping.
cat.meow();  // Cat-specific method: Whiskers says meow!
```

#### Accessing Parent Methods with super

```typescript
class Bird extends Animal {
  wingSpan: number;
  
  constructor(name: string, wingSpan: number) {
    super(name);
    this.wingSpan = wingSpan;
  }
  
  // Override with super call
  eat(): void {
    // Call the parent's eat method first
    super.eat();
    console.log(`${this.name} is picking at seeds.`);
  }
  
  fly(): void {
    console.log(`${this.name} is flying with a wingspan of ${this.wingSpan}cm.`);
  }
}

const bird = new Bird('Tweety', 30);
bird.eat();
// Output:
// Tweety is eating.
// Tweety is picking at seeds.
```

#### Multi-level Inheritance

```typescript
// Base class
class Vehicle {
  make: string;
  
  constructor(make: string) {
    this.make = make;
  }
  
  start(): void {
    console.log(`${this.make} vehicle started.`);
  }
  
  stop(): void {
    console.log(`${this.make} vehicle stopped.`);
  }
}

// Intermediate class
class Car extends Vehicle {
  model: string;
  
  constructor(make: string, model: string) {
    super(make);
    this.model = model;
  }
  
  start(): void {
    console.log(`${this.make} ${this.model} engine started.`);
  }
  
  drive(): void {
    console.log(`${this.make} ${this.model} is driving.`);
  }
}

// Final derived class
class ElectricCar extends Car {
  batteryCapacity: number;
  
  constructor(make: string, model: string, batteryCapacity: number) {
    super(make, model);
    this.batteryCapacity = batteryCapacity;
  }
  
  start(): void {
    console.log(`${this.make} ${this.model} powered on silently.`);
  }
  
  charge(): void {
    console.log(`${this.make} ${this.model} is charging. Battery capacity: ${this.batteryCapacity}kWh.`);
  }
}

const tesla = new ElectricCar('Tesla', 'Model S', 100);
tesla.start();  // Tesla Model S powered on silently.
tesla.drive();  // Tesla Model S is driving.
tesla.charge(); // Tesla Model S is charging. Battery capacity: 100kWh.
tesla.stop();   // Tesla vehicle stopped. (Inherited from Vehicle)
```

### Polymorphism

Polymorphism allows objects of different classes to be treated as objects of a common superclass, with methods being called based on the actual object type.

#### Method Polymorphism

```typescript
// Base class
class Shape {
  color: string;
  
  constructor(color: string) {
    this.color = color;
  }
  
  // Base method
  calculateArea(): number {
    return 0; // Default implementation
  }
  
  describe(): void {
    console.log(`This is a ${this.color} shape with area ${this.calculateArea()}.`);
  }
}

// Derived classes with different implementations
class Circle extends Shape {
  radius: number;
  
  constructor(color: string, radius: number) {
    super(color);
    this.radius = radius;
  }
  
  calculateArea(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  width: number;
  height: number;
  
  constructor(color: string, width: number, height: number) {
    super(color);
    this.width = width;
    this.height = height;
  }
  
  calculateArea(): number {
    return this.width * this.height;
  }
}

// Polymorphism in action
function printArea(shape: Shape): void {
  console.log(`Area: ${shape.calculateArea()}`);
}

const circle = new Circle('red', 5);
const rectangle = new Rectangle('blue', 4, 6);

printArea(circle);     // Area: 78.54...
printArea(rectangle);  // Area: 24

// Array of different shapes
const shapes: Shape[] = [
  new Circle('green', 3),
  new Rectangle('yellow', 5, 5),
  new Circle('purple', 2)
];

// Process different shapes uniformly
shapes.forEach(shape => {
  shape.describe();
});
```

#### Interface-based Polymorphism

```typescript
// Define an interface
interface Drawable {
  draw(): void;
}

// Classes implementing the interface
class Triangle implements Drawable {
  draw(): void {
    console.log('Drawing a triangle');
  }
}

class Square implements Drawable {
  draw(): void {
    console.log('Drawing a square');
  }
}

class Canvas {
  // Method accepting any object implementing Drawable
  render(item: Drawable): void {
    item.draw();
  }
}

// Using interface-based polymorphism
const canvas = new Canvas();
canvas.render(new Triangle());  // Drawing a triangle
canvas.render(new Square());    // Drawing a square
```

#### Duck Typing

TypeScript also supports "duck typing" or structural typing, where compatibility is determined by the object's shape rather than its type name.

```typescript
// No explicit interface
class Duck {
  quack(): void {
    console.log('Quack!');
  }
  
  swim(): void {
    console.log('Swimming like a duck');
  }
}

// Different class with compatible methods
class RubberDuck {
  quack(): void {
    console.log('Squeak!');
  }
  
  swim(): void {
    console.log('Floating like a rubber duck');
  }
}

// Function using duck typing
function makeItQuack(duck: { quack: () => void }): void {
  duck.quack();
}

const realDuck = new Duck();
const toyDuck = new RubberDuck();

makeItQuack(realDuck);  // Quack!
makeItQuack(toyDuck);   // Squeak!
```

### Key Concepts of Inheritance and Polymorphism

- **Inheritance**
  - Allows a class to reuse code from a parent class
  - Enables the creation of hierarchies of related classes
  - Uses the `extends` keyword to create a parent-child relationship
  - Child classes can override parent methods to provide specialized behavior
  - The `super` keyword can be used to call parent class methods and constructors

- **Polymorphism**
  - Allows objects of different types to be treated through a common superclass
  - Enables more flexible and reusable code
  - Types of polymorphism in TypeScript:
    - **Subtype polymorphism**: Using a base class reference to refer to derived class objects
    - **Interface-based polymorphism**: Objects of different classes implementing the same interface
    - **Duck typing**: Type compatibility based on the shape of an object rather than its declared type

- **Benefits**
  - **Code reuse**: Inherit behavior from parent classes
  - **Abstraction**: Focus on essential features while hiding implementation details
  - **Flexibility**: Change behavior at runtime based on the actual object type
  - **Extensibility**: Add new derived classes without modifying existing code
  - **Modularity**: Organize code into logical hierarchies

- **Best Practices**
  - Favor composition over inheritance when appropriate
  - Keep inheritance hierarchies relatively shallow
  - Use interfaces for unrelated classes that share behavior
  - Override methods deliberately with clear purpose
  - Ensure the Liskov Substitution Principle is maintained (derived classes should be substitutable for their base classes)

---

## Generics

Generics provide a way to create reusable components that work with a variety of types rather than a single type, without sacrificing type safety.

### Basic Generics

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

// Usage with explicit type parameter
const str = identity<string>('hello');  // Type: string
const num = identity<number>(42);       // Type: number

// Usage with type inference
const bool = identity(true);            // Type: boolean
```

### Generic Constraints

```typescript
// Constraint using interface
interface Lengthy {
  length: number;
}

// Generic function with constraint
function logLength<T extends Lengthy>(arg: T): T {
  console.log(`Length: ${arg.length}`);
  return arg;
}

// Valid: string has a length property
logLength('hello');               // Length: 5

// Valid: arrays have a length property
logLength([1, 2, 3]);            // Length: 3

// Valid: custom objects with length property
logLength({ length: 10, value: 'test' });  // Length: 10

// Error: number doesn't have a length property
// logLength(42);
```

### Generic Classes

```typescript
// Generic class
class Box<T> {
  private content: T;
  
  constructor(value: T) {
    this.content = value;
  }
  
  getValue(): T {
    return this.content;
  }
  
  setValue(value: T): void {
    this.content = value;
  }
}

// Usage with different types
const stringBox = new Box<string>('hello');
const value1: string = stringBox.getValue();  // Type: string

const numberBox = new Box<number>(42);
const value2: number = numberBox.getValue();  // Type: number

// Complex types
interface User {
  id: number;
  name: string;
}

const userBox = new Box<User>({ id: 1, name: 'John' });
const user: User = userBox.getValue();  // Type: User
console.log(user.name);  // John
```

### Generic Interfaces

```typescript
// Generic interface
interface Repository<T> {
  get(id: number): T;
  save(item: T): void;
  delete(id: number): void;
}

// Implementation for User type
interface User {
  id: number;
  name: string;
}

class UserRepository implements Repository<User> {
  private users: User[] = [];
  
  get(id: number): User {
    const user = this.users.find(u => u.id === id);
    if (!user) {
      throw new Error(`User with id ${id} not found`);
    }
    return user;
  }
  
  save(item: User): void {
    const existingIndex = this.users.findIndex(u => u.id === item.id);
    if (existingIndex >= 0) {
      this.users[existingIndex] = item;
    } else {
      this.users.push(item);
    }
  }
  
  delete(id: number): void {
    const existingIndex = this.users.findIndex(u => u.id === id);
    if (existingIndex >= 0) {
      this.users.splice(existingIndex, 1);
    }
  }
}

// Implementation for different type
interface Product {
  id: number;
  name: string;
  price: number;
}

class ProductRepository implements Repository<Product> {
  private products: Product[] = [];
  
  get(id: number): Product {
    const product = this.products.find(p => p.id === id);
    if (!product) {
      throw new Error(`Product with id ${id} not found`);
    }
    return product;
  }
  
  save(item: Product): void {
    const existingIndex = this.products.findIndex(p => p.id === item.id);
    if (existingIndex >= 0) {
      this.products[existingIndex] = item;
    } else {
      this.products.push(item);
    }
  }
  
  delete(id: number): void {
    const existingIndex = this.products.findIndex(p => p.id === id);
    if (existingIndex >= 0) {
      this.products.splice(existingIndex, 1);
    }
  }
}
```

### Generic Type Aliases

```typescript
// Generic type alias
type Pair<T, U> = {
  first: T;
  second: U;
};

// Usage
const coordinates: Pair<number, number> = { first: 10, second: 20 };
const entry: Pair<string, number> = { first: 'age', second: 30 };

// Generic function with type alias
function swap<T, U>(pair: Pair<T, U>): Pair<U, T> {
  return {
    first: pair.second,
    second: pair.first
  };
}

const swapped = swap(entry);  // { first: 30, second: 'age' }
```

### Generic Default Types

```typescript
// Generic with default type
function createArray<T = string>(length: number, value: T): T[] {
  return Array(length).fill(value);
}

// Using default type (string)
const strings = createArray(3, 'a');  // ['a', 'a', 'a']

// Specifying a different type
const numbers = createArray<number>(3, 1);  // [1, 1, 1]
```

### Multiple Type Parameters

```typescript
// Function with multiple type parameters
function merge<T, U>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge({ name: 'John' }, { age: 30 });
console.log(merged);  // { name: 'John', age: 30 }

// Dictionary type with different key-value types
interface Dictionary<K extends string | number | symbol, V> {
  [key: K]: V;
}

// Map type for specific keys and values
type UserRoleMap = Dictionary<string, 'admin' | 'user' | 'guest'>;
```

### Generic Function Overloads

```typescript
// Generic function overloads
function process<T extends string>(value: T): string[];
function process<T extends number>(value: T): number;
function process<T extends string | number>(value: T): string[] | number {
  if (typeof value === 'string') {
    return value.split('');
  } else {
    return value * 2;
  }
}

const chars = process('hello');  // ['h', 'e', 'l', 'l', 'o']
const doubled = process(10);     // 20
```

### Generic Conditional Types

```typescript
// Conditional types
type NonNullable<T> = T extends null | undefined ? never : T;

// Usage
type A = NonNullable<string | null>;  // string

// Extract return type of a function
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function greeting(): string {
  return 'Hello';
}

type GreetingReturn = ReturnType<typeof greeting>;  // string
```

### Key-Value Mapping with Generics

```typescript
// Function to transform an object's values
function transformValues<T, U>(
  obj: Record<string, T>,
  transformer: (value: T) => U
): Record<string, U> {
  const result: Record<string, U> = {};
  
  for (const key in obj) {
    if (Object.prototype.hasOwnProperty.call(obj, key)) {
      result[key] = transformer(obj[key]);
    }
  }
  
  return result;
}

// Usage
const numbers = { a: 1, b: 2, c: 3 };
const doubled = transformValues(numbers, n => n * 2);
console.log(doubled);  // { a: 2, b: 4, c: 6 }

const strings = { name: 'John', city: 'New York' };
const uppercased = transformValues(strings, s => s.toUpperCase());
console.log(uppercased);  // { name: 'JOHN', city: 'NEW YORK' }
```

### Generic Utility Types

TypeScript includes several built-in generic utility types:

```typescript
// Partial - Makes all properties optional
interface User {
  id: number;
  name: string;
  email: string;
}

function updateUser(user: User, updates: Partial<User>): User {
  return { ...user, ...updates };
}

const user: User = { id: 1, name: 'John', email: 'john@example.com' };
const updated = updateUser(user, { name: 'Johnny' });
// { id: 1, name: 'Johnny', email: 'john@example.com' }

// Required - Makes all properties required
interface Config {
  endpoint?: string;
  timeout?: number;
}

function validateConfig(config: Required<Config>): boolean {
  return Boolean(config.endpoint && config.timeout);
}

// Readonly - Makes all properties readonly
const readonlyUser: Readonly<User> = { id: 1, name: 'John', email: 'john@example.com' };
// readonlyUser.name = 'Johnny'; // Error: Cannot assign to 'name' because it is a read-only property

// Record - Creates a type with specified properties of specified type
type Role = 'admin' | 'user' | 'guest';
const permissions: Record<Role, string[]> = {
  admin: ['read', 'write', 'delete'],
  user: ['read', 'write'],
  guest: ['read']
};

// Pick - Creates a type by picking specified properties
type UserBasicInfo = Pick<User, 'id' | 'name'>;
const basicInfo: UserBasicInfo = { id: 1, name: 'John' };

// Omit - Creates a type by omitting specified properties
type UserWithoutEmail = Omit<User, 'email'>;
const userWithoutEmail: UserWithoutEmail = { id: 1, name: 'John' };

// Exclude - Excludes types from a union
type Numbers = 1 | 2 | 3 | 4 | 5;
type EvenNumbers = Exclude<Numbers, 1 | 3 | 5>;  // 2 | 4

// Extract - Extracts types from a union
type OddNumbers = Extract<Numbers, 1 | 3 | 5>;  // 1 | 3 | 5

// Parameters - Extracts parameter types from a function
function greet(name: string, age: number): string {
  return `Hello, ${name}! You are ${age} years old.`;
}

type GreetParams = Parameters<typeof greet>;  // [string, number]
```

### Recursive Generic Types

```typescript
// Recursive type for nested arrays
type NestedArray<T> = Array<T | NestedArray<T>>;

const numbers: NestedArray<number> = [1, 2, [3, 4, [5, 6]], 7];

// Recursive type for tree structures
interface TreeNode<T> {
  value: T;
  children?: TreeNode<T>[];
}

const tree: TreeNode<string> = {
  value: 'root',
  children: [
    { value: 'child1' },
    { 
      value: 'child2',
      children: [
        { value: 'grandchild1' },
        { value: 'grandchild2' }
      ]
    }
  ]
};
```

### Benefits of Generics

- **Type Safety**: Maintain type checking while working with different types
- **Code Reusability**: Write functions and classes that work with any type
- **Reduced Code Duplication**: Avoid writing similar code for different types
- **Better APIs**: Create flexible interfaces that don't sacrifice type information
- **Self-Documenting Code**: Types make code more understandable

### When to Use Generics

- When creating functions or classes that should work with a variety of types
- When the type of a value is derived from the type of another value
- When implementing common data structures (arrays, lists, maps, etc.)
- When you want to preserve type information through a transformation
- When creating utility functions that operate on different types

---

## Encapsulation

Encapsulation is a fundamental object-oriented principle that restricts direct access to an object's components and only exposes a limited interface to the outside world.

### Core Concepts of Encapsulation

```typescript
class BankAccount {
  // Private property - hidden from outside access
  private balance: number;
  private accountNumber: string;
  
  // Public methods form the interface to interact with the object
  constructor(initialBalance: number) {
    this.balance = initialBalance;
    this.accountNumber = `ACC-${Math.floor(Math.random() * 1000000)}`;
  }
  
  public deposit(amount: number): void {
    if (amount <= 0) {
      throw new Error('Deposit amount must be positive');
    }
    this.balance += amount;
    this.logTransaction('deposit', amount);
  }
  
  public withdraw(amount: number): boolean {
    if (amount <= 0) {
      throw new Error('Withdrawal amount must be positive');
    }
    
    if (amount > this.balance) {
      return false;
    }
    
    this.balance -= amount;
    this.logTransaction('withdrawal', amount);
    return true;
  }
  
  public getBalance(): number {
    return this.balance;
  }
  
  public getAccountDetails(): { accountNumber: string; balance: number } {
    return {
      accountNumber: this.accountNumber,
      balance: this.balance
    };
  }
  
  // Private method - internal implementation detail
  private logTransaction(type: string, amount: number): void {
    console.log(`Transaction: ${type} of $${amount}`);
    console.log(`New balance: $${this.balance}`);
  }
}

// Using the encapsulated class
const account = new BankAccount(1000);

// We can only interact with the object through its public interface
account.deposit(500);
account.withdraw(200);
console.log(account.getBalance());  // 1300

// Cannot access private members directly
// console.log(account.balance);

// Cannot call private methods
// account.logTransaction('test', 100);
```

### Benefits of Encapsulation

- **Information Hiding**
  - Internal data and implementation details are hidden from the outside
  - Reduces complexity for users of the class
  - Prevents external code from depending on internal details

- **Controlled Access**
  - Data can only be accessed through well-defined methods
  - Enables validation of inputs and state changes
  - Maintains object invariants (constraints that must always be true)

- **Modularity**
  - Changes to internal implementation don't affect external code
  - Components can evolve independently
  - Makes the system more maintainable

- **Security**
  - Prevents unauthorized access to sensitive data
  - Ensures data integrity by controlling how it's modified

### Techniques for Encapsulation

#### Private Class Fields

```typescript
class Person {
  // Private fields - only accessible within the class
  #age: number;
  #ssn: string;
  
  // Public fields
  name: string;
  
  constructor(name: string, age: number, ssn: string) {
    this.name = name;
    this.#age = age;
    this.#ssn = ssn;
  }
  
  getAge(): number {
    return this.#age;
  }
  
  // Last 4 digits only for security
  getLastFourSSN(): string {
    return this.#ssn.substring(this.#ssn.length - 4);
  }
}

const person = new Person('John', 30, '123-45-6789');
console.log(person.name);  // John
console.log(person.getAge());  // 30
console.log(person.getLastFourSSN());  // 6789

// Cannot access private fields
// console.log(person.#age);  // Error: Property '#age' is not accessible
```

#### Getters and Setters

```typescript
class Product {
  private _name: string;
  private _price: number;
  private _quantity: number;
  
  constructor(name: string, price: number, quantity: number) {
    this._name = name;
    this._price = price;
    this._quantity = quantity;
  }
  
  // Getters - control how properties are accessed
  get name(): string {
    return this._name;
  }
  
  get price(): number {
    return this._price;
  }
  
  get quantity(): number {
    return this._quantity;
  }
  
  // Computed property
  get totalValue(): number {
    return this._price * this._quantity;
  }
  
  // Setters - control how properties are modified
  set name(value: string) {
    if (!value || value.trim() === '') {
      throw new Error('Name cannot be empty');
    }
    this._name = value;
  }
  
  set price(value: number) {
    if (value < 0) {
      throw new Error('Price cannot be negative');
    }
    this._price = value;
  }
  
  set quantity(value: number) {
    if (value < 0 || !Number.isInteger(value)) {
      throw new Error('Quantity must be a non-negative integer');
    }
    this._quantity = value;
  }
}

const product = new Product('Laptop', 999.99, 5);

// Using getters
console.log(product.name);       // Laptop
console.log(product.totalValue); // 4999.95

// Using setters with validation
product.price = 899.99;
// product.quantity = -1;  // Error: Quantity must be a non-negative integer
```

#### Closure-based Encapsulation

```typescript
function createCounter() {
  // Private variable - captured in the closure
  let count = 0;
  
  // Return an object with methods that have access to the private variable
  return {
    increment(): void {
      count++;
    },
    decrement(): void {
      count--;
    },
    getCount(): number {
      return count;
    },
    reset(): void {
      count = 0;
    }
  };
}

const counter = createCounter();
counter.increment();
counter.increment();
console.log(counter.getCount());  // 2

// Cannot access the private variable
// console.log(counter.count);  // undefined
```

### Encapsulation Patterns

#### Module Pattern

```typescript
// IIFE (Immediately Invoked Function Expression) to create a module
const Calculator = (function() {
  // Private variables and functions
  let result = 0;
  
  function validate(value: number): void {
    if (typeof value !== 'number' || isNaN(value)) {
      throw new Error('Invalid number');
    }
  }
  
  // Public API
  return {
    add(value: number): void {
      validate(value);
      result += value;
    },
    subtract(value: number): void {
      validate(value);
      result -= value;
    },
    multiply(value: number): void {
      validate(value);
      result *= value;
    },
    divide(value: number): void {
      validate(value);
      if (value === 0) {
        throw new Error('Cannot divide by zero');
      }
      result /= value;
    },
    getResult(): number {
      return result;
    },
    clear(): void {
      result = 0;
    }
  };
})();

Calculator.add(10);
Calculator.multiply(2);
console.log(Calculator.getResult());  // 20

// Private members are not accessible
// console.log(Calculator.result);  // undefined
// Calculator.validate(5);  // Error: validate is not a function
```

#### Namespace Pattern

```typescript
// Namespace for grouping related functionality
namespace Geometry {
  // Private functions and constants
  const PI = Math.PI;
  
  function degreesToRadians(degrees: number): number {
    return degrees * (PI / 180);
  }
  
  // Public API
  export function calculateCircleArea(radius: number): number {
    return PI * radius * radius;
  }
  
  export function calculateRectangleArea(width: number, height: number): number {
    return width * height;
  }
  
  export function calculateTriangleArea(base: number, height: number): number {
    return (base * height) / 2;
  }
  
  export function calculateCircumference(radius: number): number {
    return 2 * PI * radius;
  }
}

// Using the namespace
console.log(Geometry.calculateCircleArea(5));  // 78.54...

// Cannot access private members
// console.log(Geometry.PI);  // Error: Property 'PI' does not exist on type 'typeof Geometry'
// console.log(Geometry.degreesToRadians(90));  // Error: Property 'degreesToRadians' does not exist on type 'typeof Geometry'
```

### Best Practices for Encapsulation

- **Minimal Public Interface**: Expose only what is necessary for client code
- **Default to Private**: Make properties and methods private unless they need to be exposed
- **Immutability**: Use readonly properties when properties shouldn't change after initialization
- **Validation**: Add validation in setters and methods to ensure data integrity
- **Levels of Access**: Use a combination of public, private, and protected for fine-grained control
- **Consistent Naming**: Use conventions like underscore prefix for private members if not using # syntax
- **Documentation**: Clearly document the public interface for users of the class

---

## Access Modifiers

Access modifiers in TypeScript control the visibility and accessibility of class members (properties and methods).

### Types of Access Modifiers

```typescript
class Person {
  // Public - accessible from anywhere (default)
  public name: string;
  
  // Private - only accessible within the class
  private ssn: string;
  
  // Protected - accessible within the class and its subclasses
  protected age: number;
  
  // Readonly - can only be assigned during initialization
  readonly birthDate: Date;
  
  constructor(name: string, ssn: string, age: number, birthDate: Date) {
    this.name = name;
    this.ssn = ssn;
    this.age = age;
    this.birthDate = birthDate;
  }
  
  // Public method
  public getInfo(): string {
    return `${this.name}, Age: ${this.age}`;
  }
  
  // Private method
  private getSSN(): string {
    return this.ssn;
  }
  
  // Protected method
  protected getBirthYear(): number {
    return this.birthDate.getFullYear();
  }
}

// Child class
class Employee extends Person {
  private employeeId: string;
  
  constructor(
    name: string,
    ssn: string,
    age: number,
    birthDate: Date,
    employeeId: string
  ) {
    super(name, ssn, age, birthDate);
    this.employeeId = employeeId;
  }
  
  // Can access protected members from the parent class
  public getEmployeeInfo(): string {
    return `${this.getInfo()}, Birth Year: ${this.getBirthYear()}`;
  }
  
  // Can modify protected members
  public celebrateBirthday(): void {
    this.age++;
    console.log(`Happy Birthday! ${this.name} is now ${this.age} years old.`);
  }
  
  // Cannot access private members from parent
  // public getEmployeeSSN(): string {
  //   return this.ssn;  // Error: Property 'ssn' is private and only accessible within class 'Person'
  // }
  
  // Cannot access parent's private methods
  // public getSSNInfo(): string {
  //   return this.getSSN();  // Error: Property 'getSSN' is private and only accessible within class 'Person'
  // }
}

// Using the classes
const person = new Person('John Doe', '123-45-6789', 30, new Date(1993, 0, 15));
console.log(person.name);  // John Doe
console.log(person.getInfo());  // John Doe, Age: 30

// Cannot access private or protected members
// console.log(person.ssn);  // Error: Property 'ssn' is private
// console.log(person.age);  // Error: Property 'age' is protected
// console.log(person.getSSN());  // Error: Property 'getSSN' is private

// Creating an employee
const employee = new Employee('Jane Smith', '987-65-4321', 28, new Date(1995, 5, 20), 'EMP001');
console.log(employee.name);  // Jane Smith
console.log(employee.getEmployeeInfo());  // Jane Smith, Age: 28, Birth Year: 1995
employee.celebrateBirthday();  // Happy Birthday! Jane Smith is now 29 years old.

// Cannot modify readonly properties
// person.birthDate = new Date();  // Error: Cannot assign to 'birthDate' because it is a read-only property
```

### Detailed Explanation of Each Access Modifier

#### Public

- **Visibility**: Accessible from anywhere
- **Default Modifier**: Members are public by default if no modifier is specified
- **Use Cases**:
  - API methods and properties meant to be used by client code
  - Class constructors (usually)
  - Utility functions that should be available universally

```typescript
class PublicExample {
  // Explicitly public
  public explicitProp: string = 'explicit';
  
  // Implicitly public
  implicitProp: string = 'implicit';
  
  // Public method
  logProps(): void {
    console.log(this.explicitProp, this.implicitProp);
  }
}

const pub = new PublicExample();
pub.explicitProp = 'changed';  // OK - public access
pub.implicitProp = 'modified'; // OK - public access
pub.logProps();  // changed modified
```

#### Private

- **Visibility**: Only accessible within the class itself
- **Implementation**: 
  - TypeScript private (`private` keyword)
  - ECMAScript private (`#` prefix)
- **Use Cases**:
  - Internal state that should not be modified directly
  - Helper methods for internal implementation
  - Data that needs validation before modification

```typescript
class PrivateExample {
  // TypeScript private
  private tsPrivate: string = 'typescript private';
  
  // ECMAScript private (runtime enforced)
  #jsPrivate: string = 'javascript private';
  
  constructor() {
    // Accessible within the class
    this.tsPrivate = 'updated ts';
    this.#jsPrivate = 'updated js';
  }
  
  public getTsPrivate(): string {
    return this.tsPrivate;
  }
  
  public getJsPrivate(): string {
    return this.#jsPrivate;
  }
}

const priv = new PrivateExample();
// priv.tsPrivate = 'external access';  // Error: Property 'tsPrivate' is private
// priv.#jsPrivate = 'external access';  // Error: Property '#jsPrivate' is not accessible

console.log(priv.getTsPrivate());  // updated ts
console.log(priv.getJsPrivate());  // updated js
```

#### Protected

- **Visibility**: Accessible within the class and all subclasses
- **Use Cases**:
  - Methods or properties that subclasses should be able to access
  - Members that need to be inherited but hidden from external access
  - Base class functionality that derived classes may need to modify

```typescript
class Animal {
  protected species: string;
  
  constructor(species: string) {
    this.species = species;
  }
  
  protected makeSound(): void {
    console.log('Generic animal sound');
  }
}

class Cat extends Animal {
  constructor() {
    super('feline');
  }
  
  public meow(): void {
    // Can access protected members from parent
    console.log(`This ${this.species} says: `);
    this.makeSound();
    console.log('Meow!');
  }
}

const cat = new Cat();
cat.meow();
// Output:
// This feline says: 
// Generic animal sound
// Meow!

// Cannot access protected members from outside
// console.log(cat.species);  // Error: Property 'species' is protected
// cat.makeSound();  // Error: Property 'makeSound' is protected
```

#### Readonly

- **Visibility**: Does not affect visibility, only modifiability
- **Restrictions**: Can only be assigned during initialization
- **Use Cases**:
  - Constants and configuration values
  - Properties that should never change after initialization
  - IDs and other permanent identifiers

```typescript
class ReadonlyExample {
  // Public readonly property
  readonly id: number;
  
  // Private readonly property
  private readonly secretKey: string;
  
  // Protected readonly property
  protected readonly createdAt: Date;
  
  constructor(id: number) {
    // Can set readonly properties in constructor
    this.id = id;
    this.secretKey = `SECRET-${Math.random().toString(36).substring(2, 10)}`;
    this.createdAt = new Date();
  }
  
  public getSecretKey(): string {
    // Can read but not modify
    return this.secretKey;
  }
  
  public modifyId(): void {
    // Cannot modify readonly properties after initialization
    // this.id = 100;  // Error: Cannot assign to 'id' because it is a read-only property
  }
}

const readonlyObj = new ReadonlyExample(1);
console.log(readonlyObj.id);  // 1
// readonlyObj.id = 2;  // Error: Cannot assign to 'id' because it is a read-only property
```

### Static Members and Access Modifiers

Access modifiers also apply to static members:

```typescript
class ConfigService {
  // Public static
  public static readonly API_URL: string = 'https://api.example.com';
  
  // Private static
  private static database: string = 'production';
  
  // Protected static
  protected static environment: string = 'production';
  
  // Public static method
  public static getApiEndpoint(resource: string): string {
    return `${ConfigService.API_URL}/${resource}`;
  }
  
  // Private static method
  private static validateEnvironment(): boolean {
    return ['development', 'staging', 'production'].includes(ConfigService.environment);
  }
  
  // Protected static method
  protected static getConnectionString(): string {
    return `db://${ConfigService.database}`;
  }
  
  // Public instance method using static members
  public connect(): void {
    if (ConfigService.validateEnvironment()) {
      console.log(`Connecting to ${ConfigService.getConnectionString()}`);
    }
  }
}

// Accessing public static members
console.log(ConfigService.API_URL);  // https://api.example.com
console.log(ConfigService.getApiEndpoint('users'));  // https://api.example.com/users

// Cannot access private or protected static members
// console.log(ConfigService.database);  // Error: Property 'database' is private
// console.log(ConfigService.environment);  // Error: Property 'environment' is protected
// ConfigService.validateEnvironment();  // Error: Property 'validateEnvironment' is private
```

### Parameter Properties

TypeScript allows combining parameter declaration and property initialization in the constructor:

```typescript
class User {
  // Parameter properties - shorthand for declaring and initializing properties
  constructor(
    public username: string,
    private password: string,
    protected email: string,
    readonly id: number
  ) {
    // No need to manually assign this.username = username, etc.
  }
  
  public verifyPassword(input: string): boolean {
    return this.password === input;
  }
  
  public getEmail(): string {
    return this.email;
  }
}

const user = new User('johndoe', 'secret123', 'john@example.com', 1);
console.log(user.username);  // johndoe
console.log(user.id);  // 1

// Access using methods
console.log(user.verifyPassword('secret123'));  // true
console.log(user.getEmail());  // john@example.com

// Direct access restrictions
// console.log(user.password);  // Error: Property 'password' is private
// console.log(user.email);  // Error: Property 'email' is protected
// user.id = 2;  // Error: Cannot assign to 'id' because it is a read-only property
```

### Benefits of Access Modifiers

- **Encapsulation**: Hide implementation details and expose only what's necessary
- **Data Integrity**: Control how data is accessed and modified
- **Flexibility**: Change internal implementation without affecting external code
- **Security**: Prevent unauthorized access to sensitive information
- **Clear API Boundaries**: Define clear interfaces for interacting with your classes

### Best Practices

- **Use private by default**: Start with private and only expose what's needed
- **Minimize protected usage**: Use protected only when subclasses truly need direct access
- **Consider readonly**: Make properties readonly when they shouldn't change after initialization
- **Document public APIs**: Clearly document the purpose and usage of public members
- **Use getters/setters**: Control access to properties, especially for validation
- **Consistent naming conventions**: Use clear naming patterns for different types of members

---

## Type Assertions

Type assertions in TypeScript allow you to tell the compiler to treat a value as a specific type, overriding its default type inference.

### Basic Type Assertions

```typescript
// "as" syntax (preferred, works in .tsx files)
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;

// Angle bracket syntax (does not work in .tsx files)
let otherValue: unknown = "another string";
let otherLength: number = (<string>otherValue).length;
```

### Type Assertion vs Type Casting

```typescript
// Type assertion in TypeScript (no runtime effect)
const value: any = 42;
const numValue = value as number;
console.log(typeof numValue);  // string (not actually converted at runtime)

// Proper conversion
const actualNumValue = Number(value);
console.log(typeof actualNumValue);  // number
```

### Common Use Cases

#### Asserting DOM Elements

```typescript
// Basic DOM element assertion
const button = document.getElementById('submit-button') as HTMLButtonElement;
button.disabled = true;  // Safe to access button-specific properties

// Without assertion, TypeScript only knows it's an HTMLElement (or null)
const genericElement = document.getElementById('some-element');
// genericElement.value = 'test';  // Error: Property 'value' does not exist on type 'HTMLElement'

// Handling potentially null elements
const maybeElement = document.getElementById('might-not-exist');
if (maybeElement) {
  // Type narrowing with null check
  const element = maybeElement as HTMLInputElement;
  element.value = 'test';
}

// Non-null assertion operator
const definitelyElement = document.getElementById('definitely-exists')!;
console.log(definitelyElement.id);  // Safe - we asserted it's not null
```

#### Working with JSON

```typescript
// Define the expected type
interface User {
  id: number;
  name: string;
  email: string;
}

// Parsing JSON with type assertion
const jsonStr = '{"id": 1, "name": "John", "email": "john@example.com"}';
const user = JSON.parse(jsonStr) as User;

// Now TypeScript knows the shape
console.log(user.id);    // 1
console.log(user.name);  // John
```

#### Force Casting between Incompatible Types

```typescript
// Double assertion for force casting (use with caution)
interface Cat {
  meow(): void;
}

interface Dog {
  bark(): void;
}

// Direct assertion would fail
const pet: Cat = {
  meow() { console.log('Meow!'); }
};

// To force casting between incompatible types, use a double assertion
// First to 'any' or 'unknown', then to the target type
const dog = pet as unknown as Dog;

// TypeScript doesn't complain, but this will fail at runtime
// dog.bark();  // Error at runtime: dog.bark is not a function
```

#### Working with Generic Types

```typescript
// Asserting in generics
function convertToArray<T>(value: T): T[] {
  if (Array.isArray(value)) {
    return value as T[];
  }
  return [value];
}

const numbers = convertToArray<number>(5);      // [5]
const strings = convertToArray<string[]>(['a', 'b']);  // ['a', 'b']
```

### The "!" Non-null Assertion Operator

```typescript
// Finding an element that we're sure exists
function getRequiredElement(): HTMLElement {
  // Without the !, TypeScript would complain about possible null
  const element = document.getElementById('required-element')!;
  return element;
}

// Using it with optional properties
interface Config {
  server?: string;
  port?: number;
}

function startServer(config: Config) {
  // Assert that server is defined
  const server = config.server!;
  
  // Without assertion
  if (config.port) {
    console.log(`Starting server on ${server}:${config.port}`);
  } else {
    console.log(`Starting server on ${server}:80`);
  }
}
```

### Type Predicates (User-Defined Type Guards)

```typescript
// Type predicate for more precise type narrowing
interface Bird {
  fly(): void;
  layEggs(): void;
}

interface Fish {
  swim(): void;
  layEggs(): void;
}

// Type predicate function
function isFish(pet: Bird | Fish): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

function moveAnimal(pet: Bird | Fish) {
  if (isFish(pet)) {
    // TypeScript knows pet is Fish here
    pet.swim();
  } else {
    // TypeScript knows pet is Bird here
    pet.fly();
  }
}

const fish: Fish = {
  swim() { console.log('Swimming'); },
  layEggs() { console.log('Laying fish eggs'); }
};

moveAnimal(fish);  // Swimming
```

### Type Assertion in JSX

```tsx
// In .tsx files, only the 'as' syntax works
// This is why the angle bracket syntax is generally avoided

// Example with React and TypeScript
const MyComponent: React.FC = () => {
  // Asserting the input element
  const inputRef = useRef<HTMLInputElement>(null);
  
  const focusInput = () => {
    // Need non-null assertion since useRef's initial value is null
    (inputRef.current as HTMLInputElement).focus();
    
    // Or using the non-null assertion operator
    inputRef.current!.focus();
  };
  
  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus</button>
    </div>
  );
};
```

### Assertion Gotchas and Best Practices

```typescript
// Incorrect assertion - runtime error!
const value: any = 42;
// The compiler allows this, but it causes runtime errors
// const str = value as string;
// console.log(str.toUpperCase());  // Runtime error: str.toUpperCase is not a function

// Better approach: add runtime checks
if (typeof value === 'string') {
  const str = value;
  console.log(str.toUpperCase());
}

// Another example: optional properties
interface User {
  name: string;
  address?: {
    street: string;
    city: string;
  };
}

const user: User = { name: 'John' };

// Dangerous - may cause runtime error if address is undefined
// const city = (user.address as { city: string }).city;

// Better approach
const city = user.address?.city;
console.log(city);  // undefined

// If you must assert, check first
if (user.address) {
  const street = (user.address as { street: string }).street;
  console.log(street);
}
```

### Guidelines for Type Assertions

- **Use sparingly**: Only use type assertions when you know more about a type than TypeScript does
- **Prefer type guards**: When possible, use `instanceof`, `typeof`, or custom type predicates
- **Check before asserting**: Combine runtime checks with assertions for safer code
- **Document assertions**: Comment why an assertion is necessary, especially for complex cases
- **Consider alternatives**: Look for ways to improve type definitions instead of asserting
- **Beware of DOM assertions**: Always check if elements exist before asserting and accessing properties

---

## Modules

TypeScript modules allow you to organize code into separate files and namespaces, controlling what is exposed to other modules.

### Module Basics

```typescript
// math.ts - Exporting module
// Named exports
export function add(x: number, y: number): number {
  return x + y;
}

export function subtract(x: number, y: number): number {
  return x - y;
}

// Default export
export default function multiply(x: number, y: number): number {
  return x * y;
}

// Exporting constants
export const PI = 3.14159;

// Exporting types
export interface Shape {
  area(): number;
}

export type Point = {
  x: number;
  y: number;
};

// Private function (not exported)
function square(x: number): number {
  return x * x;
}
```

```typescript
// app.ts - Importing module
// Importing named exports
import { add, subtract, PI, type Point } from './math';

// Renaming imports
import { add as addition } from './math';

// Importing default export
import multiply from './math';

// Importing all exports as a namespace
import * as MathUtils from './math';

// Usage
console.log(add(2, 3));         // 5
console.log(addition(2, 3));    // 5
console.log(subtract(5, 2));    // 3
console.log(multiply(2, 3));    // 6
console.log(MathUtils.PI);      // 3.14159
console.log(MathUtils.add(4, 5)); // 9

// Using imported types
const point: Point = { x: 10, y: 20 };
```

### Module Re-export

```typescript
// shapes.ts
export interface Circle {
  radius: number;
  area(): number;
}

export interface Rectangle {
  width: number;
  height: number;
  area(): number;
}
```

```typescript
// index.ts - Re-exporting modules
// Re-export named exports
export { Circle, Rectangle } from './shapes';

// Re-export and rename
export { Circle as RoundShape } from './shapes';

// Re-export everything
export * from './math';

// Re-export default export
export { default as multiplyNumbers } from './math';
```

### Dynamic Imports

```typescript
// Main application code
async function loadModule() {
  try {
    // Dynamically import the module when needed
    const mathModule = await import('./math');
    
    console.log(mathModule.add(5, 3));
    console.log(mathModule.default(4, 2));
  } catch (error) {
    console.error('Failed to load module:', error);
  }
}

// Load the module later
document.getElementById('loadButton')?.addEventListener('click', loadModule);
```

### Module Augmentation

```typescript
// original-module.ts
export interface User {
  id: number;
  name: string;
}
```

```typescript
// augmentation.ts
import { User } from './original-module';

// Module augmentation
declare module './original-module' {
  // Add new properties to existing interface
  interface User {
    email: string;
    role: 'admin' | 'user';
  }
  
  // Add new exports
  export function createUser(name: string): User;
}

// Implementation of augmented function
export function createUser(name: string): User {
  return {
    id: Math.floor(Math.random() * 1000),
    name,
    email: `${name.toLowerCase()}@example.com`,
    role: 'user'
  };
}
```

### Module Organization Patterns

#### Barrel Pattern

```typescript
// models/user.ts
export interface User {
  id: number;
  name: string;
}

// models/product.ts
export interface Product {
  id: number;
  name: string;
  price: number;
}

// models/index.ts - Barrel file
export * from './user';
export * from './product';
```

```typescript
// Importing from barrel
import { User, Product } from './models';

const user: User = { id: 1, name: 'John' };
const product: Product = { id: 1, name: 'Laptop', price: 999 };
```

#### Feature-based Organization

```
src/
├── features/
│   ├── authentication/
│   │   ├── components/
│   │   ├── services/
│   │   ├── types.ts
│   │   └── index.ts
│   ├── products/
│   │   ├── components/
│   │   ├── services/
│   │   ├── types.ts
│   │   └── index.ts
│   └── users/
│       ├── components/
│       ├── services/
│       ├── types.ts
│       └── index.ts
└── shared/
    ├── utils/
    ├── components/
    └── types.ts
```

### Benefits of Modules

- **Code Organization**: Break code into manageable, focused files
- **Encapsulation**: Hide implementation details, only exposing what's needed
- **Reusability**: Import and use modules across different parts of an application
- **Dependency Management**: Clearly express dependencies between parts of code
- **Tree Shaking**: Allow bundlers to remove unused code, reducing final bundle size

### Best Practices

- **Single Responsibility**: Each module should focus on a single aspect or feature
- **Explicit Exports**: Be selective about what you export from a module
- **Consistent Naming**: Use clear and consistent naming for imports and exports
- **Index Files**: Use barrel files to simplify imports from complex directories
- **Avoid Circular Dependencies**: Design modules to avoid circular references
- **Export Types**: Explicitly export interfaces, types, and enums needed by consumers

---

## Advanced Types

TypeScript offers powerful advanced type features to express complex relationships between types and create more precise type definitions.

### Union Types

Union types allow a value to be one of several types.

```typescript
// Basic union type
type ID = string | number;

function printID(id: ID): void {
  console.log(`ID: ${id}`);
  
  // Type narrowing with typeof
  if (typeof id === 'string') {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(0));
  }
}

printID('abc123');  // ID: abc123, ABC123
printID(123);       // ID: 123, 123
```

### Intersection Types

Intersection types combine multiple types into one.

```typescript
// Base interfaces
interface HasName {
  name: string;
}

interface HasAge {
  age: number;
}

// Intersection type
type Person = HasName & HasAge;

// Object must have all properties from both types
const person: Person = {
  name: 'John',
  age: 30
};

// Function parameters using intersection types
function greet(person: HasName & { title: string }): string {
  return `Hello, ${person.title} ${person.name}!`;
}

greet({ name: 'John', title: 'Mr.' });  // Hello, Mr. John!
```

### Type Guards

Type guards help narrow down types within conditional blocks.

```typescript
// Using typeof for primitive types
function process(value: string | number): string {
  if (typeof value === 'string') {
    return value.toLowerCase();
  } else {
    return value.toString();
  }
}

// Using instanceof for classes
class Customer {
  constructor(public name: string) {}
  
  placeOrder(): void {
    console.log(`${this.name} placed an order`);
  }
}

class Employee {
  constructor(public name: string, public department: string) {}
  
  assignTask(): void {
    console.log(`${this.name} assigned a task`);
  }
}

function processUser(user: Customer | Employee): void {
  console.log(`Processing user: ${user.name}`);
  
  if (user instanceof Customer) {
    user.placeOrder();
  } else {
    user.assignTask();
  }
}

// Using property checks
interface Circle {
  kind: 'circle';
  radius: number;
}

interface Square {
  kind: 'square';
  sideLength: number;
}

type Shape = Circle | Square;

function calculateArea(shape: Shape): number {
  if (shape.kind === 'circle') {
    return Math.PI * shape.radius ** 2;
  } else {
    return shape.sideLength ** 2;
  }
}

// Custom type guard using type predicates
interface Cat {
  meow(): void;
}

interface Dog {
  bark(): void;
}

function isCat(animal: Cat | Dog): animal is Cat {
  return 'meow' in animal;
}

function makeAnimalSound(animal: Cat | Dog): void {
  if (isCat(animal)) {
    animal.meow();
  } else {
    animal.bark();
  }
}
```

### Discriminated Unions

Discriminated unions use a common property to differentiate between union members.

```typescript
// Result types with discriminator
type Success = {
  status: 'success';
  data: any;
};

type Error = {
  status: 'error';
  message: string;
};

type ApiResponse = Success | Error;

function handleResponse(response: ApiResponse): void {
  // 'status' is the discriminator property
  switch (response.status) {
    case 'success':
      console.log(`Success with data: ${JSON.stringify(response.data)}`);
      break;
    case 'error':
      console.log(`Error: ${response.message}`);
      break;
  }
}

// Exhaustiveness checking with never
type TaskStatus = 'todo' | 'in-progress' | 'done' | 'canceled';

function getNextStatus(status: TaskStatus): TaskStatus {
  switch (status) {
    case 'todo':
      return 'in-progress';
    case 'in-progress':
      return 'done';
    case 'done':
      return 'done';
    case 'canceled':
      return 'canceled';
    default:
      // This ensures all cases are handled
      const exhaustiveCheck: never = status;
      return exhaustiveCheck;
  }
}
```

### Conditional Types

Conditional types select a type based on a condition.

```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type Result1 = IsString<string>;  // true
type Result2 = IsString<number>;  // false

// Extracting types
type ArrayElementType<T> = T extends (infer U)[] ? U : never;

type NumberArray = number[];
type ExtractedType = ArrayElementType<NumberArray>;  // number

// Built-in conditional utility types
type Nullable<T> = T | null;
type NonNullable<T> = T extends null | undefined ? never : T;

type MaybeString = Nullable<string>;  // string | null
type DefinitelyString = NonNullable<MaybeString>;  // string

// Conditional type with mapped types
type FunctionPropertyNames<T> = {
  [K in keyof T]: T[K] extends Function ? K : never
}[keyof T];

interface User {
  name: string;
  age: number;
  greet(): void;
  getFullName(): string;
}

type UserMethodNames = FunctionPropertyNames<User>;  // 'greet' | 'getFullName'
```

### Mapped Types

Mapped types transform each property in a type.

```typescript
// Basic mapped type
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

interface Person {
  name: string;
  age: number;
}

type ReadonlyPerson = Readonly<Person>;
const person: ReadonlyPerson = { name: 'John', age: 30 };
// person.name = 'Jane';  // Error: Cannot assign to 'name' because it is a read-only property

// Mapping with transformations
type Optional<T> = {
  [P in keyof T]?: T[P];
};

type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

// Combined transformations
type PartialNullable<T> = {
  [P in keyof T]?: T[P] | null;
};

type PartialPerson = Optional<Person>;
const partialPerson: PartialPerson = { name: 'John' };  // age is optional

// Removing modifiers
type Required<T> = {
  [P in keyof T]-?: T[P];  // Remove optional modifier
};

type Mutable<T> = {
  -readonly [P in keyof T]: T[P];  // Remove readonly modifier
};

// Filtering properties by value type
type PickByValueType<T, ValueType> = {
  [P in keyof T as T[P] extends ValueType ? P : never]: T[P]
};

interface User {
  id: number;
  name: string;
  isAdmin: boolean;
  createdAt: Date;
}

type StringProperties = PickByValueType<User, string>;  // { name: string }
```

### Template Literal Types

Template literal types build string literal types by concatenating other types.

```typescript
// Basic template literals
type Greeting = 'Hello' | 'Hi';
type Subject = 'World' | 'TypeScript';

type GreetingPhrase = `${Greeting}, ${Subject}!`;
// 'Hello, World!' | 'Hello, TypeScript!' | 'Hi, World!' | 'Hi, TypeScript!'

// With unions
type Status = 'success' | 'error' | 'pending';
type RequestType = 'GET' | 'POST' | 'PUT' | 'DELETE';

type RequestStatus = `${RequestType}_${Status}`;
// 'GET_success' | 'GET_error' | 'GET_pending' | 'POST_success' | ...

// Creating event handlers
type EventType = 'click' | 'focus' | 'blur';
type Handler<T extends string> = `on${Capitalize<T>}`;

type EventHandler = {
  [E in EventType as Handler<E>]: (event: any) => void;
};
// { onClick: (event: any) => void, onFocus: (event: any) => void, onBlur: (event: any) => void }

// Path manipulation
type Path = 'users' | 'posts' | 'comments';
type ApiRoute = `/api/${Path}` | `/api/${Path}/:id`;
// '/api/users' | '/api/posts' | '/api/comments' | '/api/users/:id' | '/api/posts/:id' | '/api/comments/:id'
```

### Index Types

Index types query and access property types.

```typescript
// Keyof operator
interface User {
  id: number;
  name: string;
  email: string;
}

type UserKey = keyof User;  // 'id' | 'name' | 'email'

// Index access types
type UserIdType = User['id'];  // number
type UserValues = User[keyof User];  // number | string

// Generic property accessor
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: User = { id: 1, name: 'John', email: 'john@example.com' };
const userName = getProperty(user, 'name');  // Type is string
const userId = getProperty(user, 'id');      // Type is number
// const userAge = getProperty(user, 'age');  // Error: Argument of type '"age"' is not assignable to parameter of type 'keyof User'
```

### The infer Keyword

The `infer` keyword is used in conditional types to extract type components.

```typescript
// Extract return type of a function
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function greet(): string {
  return 'Hello';
}

type GreetReturn = ReturnType<typeof greet>;  // string

// Extract array element type
type ElementType<T> = T extends (infer U)[] ? U : never;
type NumberArrayType = number[];
type ExtractedType = ElementType<NumberArrayType>;  // number

// Extract promise value type
type PromiseValueType<T> = T extends Promise<infer V> ? V : never;
type PromiseOfString = Promise<string>;
type ExtractedValue = PromiseValueType<PromiseOfString>;  // string

// Extract function parameter types
type ParameterTypes<T> = T extends (...args: infer P) => any ? P : never;
function add(a: number, b: number): number {
  return a + b;
}
type AddParams = ParameterTypes<typeof add>;  // [number, number]

// Extract constructable types
type InstanceType<T> = T extends new (...args: any[]) => infer R ? R : any;
class Person {
  constructor(public name: string) {}
}
type PersonInstance = InstanceType<typeof Person>;  // Person
```

### Utility Types

TypeScript provides built-in utility types for common type transformations.

```typescript
// Partial - Makes all properties optional
interface User {
  id: number;
  name: string;
  email: string;
  address: {
    street: string;
    city: string;
  };
}

type PartialUser = Partial<User>;  // All properties optional

// Deep Partial (custom utility for nested objects)
type DeepPartial<T> = T extends object ? {
  [P in keyof T]?: DeepPartial<T[P]>;
} : T;

type DeepPartialUser = DeepPartial<User>;

// Required - Makes all properties required
interface Config {
  endpoint?: string;
  timeout?: number;
  retries?: number;
}

type RequiredConfig = Required<Config>;

// Readonly - Makes all properties readonly
type ReadonlyUser = Readonly<User>;

// Deep Readonly (custom utility)
type DeepReadonly<T> = {
  readonly [P in keyof T]: T[P] extends object ? DeepReadonly<T[P]> : T[P];
};

type DeepReadonlyUser = DeepReadonly<User>;

// Record - Creates a type with specified keys and values
type UserRoles = Record<string, 'admin' | 'user' | 'guest'>;
const roles: UserRoles = {
  john: 'admin',
  jane: 'user',
  guest123: 'guest'
};

// Pick - Creates a type by picking properties
type UserBasicInfo = Pick<User, 'id' | 'name'>;

// Omit - Creates a type by omitting properties
type UserWithoutEmail = Omit<User, 'email'>;

// Exclude - Excludes types from a union
type Status = 'active' | 'inactive' | 'pending' | 'suspended';
type PositiveStatus = Exclude<Status, 'inactive' | 'suspended'>;  // 'active' | 'pending'

// Extract - Extracts types from a union
type ActiveStatus = Extract<Status, 'active' | 'pending'>;  // 'active' | 'pending'

// NonNullable - Removes null and undefined from a type
type Response = string | null | undefined;
type ValidResponse = NonNullable<Response>;  // string

// Parameters - Extracts parameter types as a tuple
function createUser(name: string, age: number, isAdmin: boolean): User {
  return { id: 1, name, email: `${name}@example.com`, address: { street: '', city: '' } };
}

type CreateUserParams = Parameters<typeof createUser>;  // [string, number, boolean]

// ConstructorParameters - Extracts constructor parameter types
class Point {
  constructor(public x: number, public y: number) {}
}

type PointConstructorParams = ConstructorParameters<typeof Point>;  // [number, number]

// ReturnType - Extracts the return type of a function
type CreateUserReturn = ReturnType<typeof createUser>;  // User

// InstanceType - Extracts the instance type of a constructor
type PointInstance = InstanceType<typeof Point>;  // Point

// ThisParameterType - Extracts the type of 'this' parameter
function toHex(this: number): string {
  return this.toString(16);
}

type ToHexThisType = ThisParameterType<typeof toHex>;  // number

// OmitThisParameter - Removes the 'this' parameter
type ToHexFunction = OmitThisParameter<typeof toHex>;  // () => string
```

### Branded/Nominal Types

TypeScript is structurally typed by default, but we can simulate nominal typing with branded types.

```typescript
// Creating branded types
type UserId = string & { readonly __brand: unique symbol };
type OrderId = string & { readonly __brand: unique symbol };

// Type-safe functions
function createUser(id: UserId, name: string): { id: UserId; name: string } {
  return { id, name };
}

function getOrder(id: OrderId): { id: OrderId; total: number } {
  return { id, total: 100 };
}

// Creating branded values safely
function asUserId(id: string): UserId {
  // Validation logic here
  return id as UserId;
}

function asOrderId(id: string): OrderId {
  // Validation logic here
  return id as OrderId;
}

// Usage
const userId = asUserId('user-123');
const orderId = asOrderId('order-456');

const user = createUser(userId, 'John');
const order = getOrder(orderId);

// Type safety
// createUser(orderId, 'John');  // Error: Argument of type 'OrderId' is not assignable to parameter of type 'UserId'
// getOrder(userId);  // Error: Argument of type 'UserId' is not assignable to parameter of type 'OrderId'
```

### Recursive Types

Recursive types reference themselves in their definition.

```typescript
// Recursive type for nested objects
type NestedObject = {
  value: string;
  children?: NestedObject[];
};

const nested: NestedObject = {
  value: 'root',
  children: [
    { value: 'child1' },
    {
      value: 'child2',
      children: [
        { value: 'grandchild1' }
      ]
    }
  ]
};

// JSON value type
type JSONValue =
  | string
  | number
  | boolean
  | null
  | JSONValue[]
  | { [key: string]: JSONValue };

const json: JSONValue = {
  name: 'John',
  age: 30,
  isAdmin: false,
  metadata: null,
  skills: ['TypeScript', 'JavaScript'],
  address: {
    street: '123 Main St',
    city: 'Anytown'
  }
};

// File system-like structure
type FileSystemItem = File | Directory;

interface File {
  type: 'file';
  name: string;
  size: number;
}

interface Directory {
  type: 'directory';
  name: string;
  children: FileSystemItem[];
}

const fileSystem: FileSystemItem = {
  type: 'directory',
  name: 'root',
  children: [
    { type: 'file', name: 'file1.txt', size: 100 },
    {
      type: 'directory',
      name: 'subfolder',
      children: [
        { type: 'file', name: 'file2.txt', size: 200 }
      ]
    }
  ]
};
```

### Advanced Types Best Practices

- **Be Explicit**: Use descriptive type names and favor explicit type annotations for clarity
- **Progressive Refinement**: Start with simpler types and refine them as needed
- **DRY Types**: Use type aliases and utility types to avoid repeating type definitions
- **Avoid Any**: Use unknown instead of any when the type is truly unknown
- **Layer Types**: Build complex types by composing simpler ones
- **Document Complex Types**: Add comments to explain the purpose and usage of complex types
- **Type Guards**: Use type guards to narrow types in conditionals
- **Balance Complexity**: Don't over-engineer types; sometimes simpler is better

### Key Concepts to Master

- **Union vs Intersection**: Union (|) means "either this or that", intersection (&) means "both this and that"
- **Type Narrowing**: The process of refining types within conditional blocks
- **Discriminated Unions**: Using a common property to differentiate between union members
- **Type Transformations**: Using mapped types, conditional types, and utility types to transform existing types
- **Type Inference**: Understanding how TypeScript infers types from context
- **Type Compatibility**: Understanding structural typing and when types are compatible
- **Generic Constraints**: Limiting generic type parameters to specific shapes

By mastering these advanced type features, you can create type-safe APIs and ensure your code is both flexible and robust.

