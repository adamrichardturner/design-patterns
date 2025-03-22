# Design Patterns in TypeScript

<img src="banner.png" width="100%" alt="Design Patterns Banner">

This repository contains implementations and explanations of various design patterns organized by category. Each pattern includes detailed explanations, code examples, and practical use cases in TypeScript.

## Prerequisites

Before diving into design patterns, make sure you're familiar with core TypeScript concepts:

- [TypeScript Fundamentals](./typescript/1-typescript_core_concepts.md) - Contains prerequisite TypeScript skills and concepts to help you better understand the pattern implementations.

## 1. Creational Patterns

Creational patterns focus on object creation mechanisms, trying to create objects in a manner suitable to the situation.

- [Factory Pattern](1-creational/1-factory_pattern/1-factory_pattern.md) - Encapsulates object creation logic by providing an interface for creating instances of a class
- [Abstract Factory Pattern](1-creational/1-factory_pattern/2-abstract_factory_pattern.md) - Creates families of related objects without specifying their concrete classes
- [Builder Pattern](1-creational/2-builder_pattern/1-builder_pattern.md) - Separates the construction of complex objects from their representation
- [Prototype Pattern](1-creational/3-prototype_pattern/1-prototype_pattern.md) - Creates new objects by copying existing objects
- [Singleton Pattern](1-creational/4-singleton_pattern/1-singleton_pattern.md) - Ensures a class has only one instance and provides a global point of access to it

## 2. Structural Patterns

Structural patterns focus on how classes and objects are composed to form larger structures.

- [Decorator Pattern](2-structural/1-decorator_pattern/1-decorator_pattern.md) - Attaches additional responsibilities to objects dynamically
- [Adapter Pattern](2-structural/2-adapter_pattern/1-adapter_pattern.md) - Allows incompatible interfaces to work together
- [Facade Pattern](2-structural/3-facade_pattern/1-facade_pattern.md) - Provides a simplified interface to a complex subsystem
- [Bridge Pattern](2-structural/4-bridge_pattern/1-bridge_pattern.md) - Separates an abstraction from its implementation
- [Composite Pattern](2-structural/5-composite_pattern/1-composite_pattern.md) - Composes objects into tree structures to represent part-whole hierarchies
- [Flyweight Pattern](2-structural/6-flyweight_pattern/1-flyweight_pattern.md) - Minimizes memory usage by sharing common parts of state between multiple objects
- [Proxy Pattern](2-structural/7-proxy_pattern/1-proxy_pattern.md) - Provides a surrogate or placeholder for another object to control access to it

## 3. Behavioral Patterns

Behavioral patterns focus on communication between objects, how objects interact and distribute responsibility.

- [Command Pattern](3-behavioural/1-command_pattern/1-command_pattern.md) - Encapsulates a request as an object
- [Chain of Responsibility Pattern](3-behavioural/2-chain_of_responsibility_pattern/1-chain_of_responsibility_pattern.md) - Passes a request along a chain of handlers
- [Observer Pattern](3-behavioural/3-observer_pattern/1-observer_pattern.md) - Defines a one-to-many dependency between objects
- [Interpreter Pattern](3-behavioural/4-interpreter_pattern/1-interpreter_pattern.md) - Implements a specialized language
- [Iterator Pattern](3-behavioural/5-iterator_pattern/1-iterator_pattern.md) - Sequentially accesses elements of a collection
- [Mediator Pattern](3-behavioural/6-mediator_pattern/1-mediator_pattern.md) - Defines simplified communication between classes
- [Memento Pattern](3-behavioural/7-memento_pattern/1-memento_pattern.md) - Captures and restores an object's internal state
- [State Pattern](3-behavioural/8-state_pattern/1-state_pattern.md) - Allows an object to alter its behavior when its internal state changes
- [Strategy Pattern](3-behavioural/9-strategy_pattern/1-strategy_pattern.md) - Defines a family of algorithms and makes them interchangeable
- [Template Pattern](3-behavioural/10-template_pattern/1-template_pattern.md) - Defines the skeleton of an algorithm, deferring steps to subclasses
- [Visitor Pattern](3-behavioural/11-visitor_pattern/1-visitor_pattern.md) - Separates an algorithm from an object structure on which it operates

## How to Use This Repository

Each pattern folder contains detailed markdown files explaining:

1. What the pattern is and its core concepts
2. When and why to use the pattern
3. TypeScript implementation examples
4. Real-world use cases and applications

Browse through the categories and click on specific patterns to learn more about their implementation and usage.
