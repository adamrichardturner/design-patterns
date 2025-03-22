# TypeScript Fundamentals for Understanding Design Patterns

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

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

**TypeScript** is a superset of JavaScript, offering static typing and additional features like interfaces, generics, and decorators.

---

## Basic Types

TypeScript introduces static types to JavaScript variables:

```typescript
let isDone: boolean = false;
let age: number = 25;
let name: string = 'John';
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ['hello', 10];
```

---

## Interfaces

Interfaces define the structure objects should adhere to:

```typescript
interface Person {
  name: string;
  age: number;
}

const john: Person = { name: 'John', age: 30 };
```

---

## Classes

Classes encapsulate behavior and state:

```typescript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  speak(): void {
    console.log(`${this.name} makes a noise.`);
  }
}

const dog = new Animal('Dog');
dog.speak();
```

---

## Abstract Classes

Abstract classes define base behavior, leaving implementation specifics to derived classes:

```typescript
abstract class Shape {
  abstract area(): number;

  describe(): void {
    console.log(`Area: ${this.area()}`);
  }
}

class Circle extends Shape {
  radius: number;

  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}
```

---

## Inheritance and Polymorphism

Inheritance enables classes to extend and reuse behavior:

```typescript
class Cat extends Animal {
  speak(): void {
    console.log(`${this.name} meows.`);
  }
}

const cat = new Cat('Cat');
cat.speak(); // Cat meows.
```

---

## Generics

Generics allow types to be parameterized for greater flexibility:

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let output = identity<string>('Hello');
```

---

## Encapsulation

Encapsulation protects object state and behaviors:

```typescript
class BankAccount {
  private balance: number = 0;

  deposit(amount: number): void {
    if (amount > 0) this.balance += amount;
  }

  getBalance(): number {
    return this.balance;
  }
}
```

---

## Access Modifiers

Control visibility with `public`, `private`, and `protected`:

```typescript
class Employee {
  public name: string;
  protected salary: number;

  constructor(name: string, salary: number) {
    this.name = name;
    this.salary = salary;
  }

  private getSalary(): number {
    return this.salary;
  }
}
```

---

## Type Assertions

Type assertions explicitly specify types:

```typescript
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;
```

---

## Modules

Organize and reuse code across files:

```typescript
// file: math.ts
export function add(x: number, y: number): number {
  return x + y;
}

// file: app.ts
import { add } from './math';
console.log(add(2, 3));
```

---

## Advanced Types

Advanced types like union, intersection, and mapped types enhance flexibility:

### Union Types

```typescript
function printId(id: number | string): void {
  console.log(`Your ID is ${id}`);
}
```

### Intersection Types

```typescript
type Admin = { adminPrivileges: string[] };
type User = { username: string };

type AdminUser = Admin & User;
```

### Mapped Types

```typescript
type Readonly<T> = { readonly [P in keyof T]: T[P] };

type ReadonlyPerson = Readonly<Person>;
```

---

## Conclusion

Understanding these core TypeScript concepts equips you to effectively implement and leverage design patterns, leading to cleaner, more robust, and maintainable code.

