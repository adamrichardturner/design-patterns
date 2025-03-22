# Design Patterns in TypeScript

<img src="banner.png" width="100%" alt="Design Patterns Banner">

This repository contains implementations and explanations of various design patterns organized by category. Each pattern includes detailed explanations, code examples, and practical use cases in TypeScript.

## Prerequisites

Before diving into design patterns, make sure you're familiar with core TypeScript concepts:

- [TypeScript Fundamentals](./0-typescript_concepts/1-typescript_core_concepts.md) - Contains prerequisite TypeScript skills and concepts to help you better understand the pattern implementations.

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

## Design Pattern Selection Guide

Below is a quick reference table to help you choose the right design pattern for your specific use case:

| Pattern | Category | Best Use Cases | Key Benefits |
|---------|----------|---------------|-------------|
| **Factory** | Creational | • Creating objects without specifying exact class<br>• When subclasses decide which class to instantiate<br>• When you need to delegate responsibility to helper subclasses | • Decouples client code from concrete classes<br>• Flexibility in creating different objects<br>• Centralizes complex object creation |
| **Abstract Factory** | Creational | • Creating families of related objects<br>• When system needs to be independent of product creation<br>• When you need to ensure compatibility between various products | • Isolates concrete classes<br>• Simplifies exchanging product families<br>• Promotes consistency among products |
| **Builder** | Creational | • Constructing complex objects step by step<br>• When object construction should be separate from representation<br>• When you need different representations of an object | • Controls construction process<br>• Allows fine-grained object creation<br>• Isolates complex construction code |
| **Prototype** | Creational | • Avoiding expensive object creation<br>• When classes to instantiate are specified at runtime<br>• Avoiding building a class hierarchy of factories | • Reduces subclassing<br>• Hides complexity of creating new instances<br>• Adds/removes products at runtime |
| **Singleton** | Creational | • Ensuring a class has just a single instance<br>• When you need stricter control over global variables<br>• When an object needs to coordinate actions across system | • Controlled access to sole instance<br>• Reduced namespace pollution<br>• Can be refined to permit a controlled number of instances |
| **Decorator** | Structural | • Adding responsibilities to objects dynamically<br>• When extension by subclassing is impractical<br>• When you need to modify behavior without affecting other objects | • More flexible than static inheritance<br>• Avoids feature-laden classes<br>• Combines multiple behaviors |
| **Adapter** | Structural | • Making incompatible interfaces compatible<br>• When reusing existing class with incompatible interface<br>• When creating reusable class that cooperates with unrelated classes | • Allows classes to work together that couldn't otherwise<br>• Improves reusability of legacy code<br>• Increases cleanliness through separation of interfaces |
| **Facade** | Structural | • Providing a simplified interface to a complex subsystem<br>• When you need to layer your subsystems<br>• When you want to reduce tight coupling between clients and subsystems | • Shields clients from subsystem components<br>• Promotes weak coupling<br>• Simplifies usage of complex systems |
| **Bridge** | Structural | • Separating an abstraction from its implementation<br>• When both abstraction and implementation should be extensible<br>• When implementation changes shouldn't impact client code | • Decouples interface from implementation<br>• Improves extensibility<br>• Hides implementation details from clients |
| **Composite** | Structural | • Representing part-whole hierarchies of objects<br>• When clients should ignore differences between compositions and individual objects<br>• Building tree structures | • Simplifies client code<br>• Makes adding new types of components easier<br>• Provides flexibility in building complex structures |
| **Flyweight** | Structural | • When you need to support large numbers of similar objects efficiently<br>• Reducing memory usage when application uses many identical objects<br>• When most object state can be made extrinsic | • Reduces memory usage<br>• Improves performance<br>• Allows efficient sharing of state |
| **Proxy** | Structural | • Controlling access to another object<br>• Adding functionality when simply using an object<br>• When you need lazy-loading, caching, logging, or access control | • Controls access to original object<br>• Can perform operations before/after requests<br>• Can work transparently to the client |
| **Command** | Behavioral | • Parameterizing objects by an action to perform<br>• Specifying, queuing, and executing requests at different times<br>• Supporting undoable operations | • Decouples sender from receiver<br>• Allows queueing of commands<br>• Supports undo/redo operations |
| **Chain of Responsibility** | Behavioral | • When more than one object may handle a request<br>• When the handler isn't known a priori<br>• When you want to issue a request to one of several objects without specifying the receiver explicitly | • Reduces coupling between sender and receivers<br>• Increases flexibility in assigning responsibilities<br>• Can dynamically change the chain at runtime |
| **Observer** | Behavioral | • When a change to one object requires changing others<br>• When an object should notify unknown objects<br>• When you need a publish-subscribe relationship | • Supports loose coupling<br>• Allows dynamic relationships<br>• Enables broadcast communication |
| **Interpreter** | Behavioral | • Implementing a specialized language<br>• When you need to evaluate sentences in a language<br>• For simple languages with well-defined grammar | • Easy to change/extend the grammar<br>• Implements grammar rules as classes<br>• Adds new expressions easily |
| **Iterator** | Behavioral | • Accessing elements of a collection without exposing its implementation<br>• Supporting multiple traversal methods<br>• Providing a uniform interface for traversal | • Simplifies client interface<br>• Supports variations in traversal<br>• Simplifies the aggregate interface |
| **Mediator** | Behavioral | • Defining how objects interact with one another<br>• When components need to interact in complex ways<br>• Reducing chaotic dependencies between objects | • Reduces coupling between components<br>• Centralizes communication logic<br>• Simplifies maintenance |
| **Memento** | Behavioral | • Capturing and restoring an object's internal state<br>• When direct interface to obtain state would expose implementation<br>• When checkpoint/restore functionality is needed | • Preserves encapsulation boundaries<br>• Simplifies originator code<br>• Provides history management |
| **State** | Behavioral | • When an object's behavior depends on its state<br>• When operations have large, multipart conditional statements<br>• When transitioning between well-defined states | • Localizes state-specific behavior<br>• Makes state transitions explicit<br>• Simplifies conditional statements |
| **Strategy** | Behavioral | • When you need different variants of an algorithm<br>• When an algorithm uses data unknown to clients<br>• When you need to eliminate conditional statements | • Isolates algorithm implementation details<br>• Enables switching between strategies at runtime<br>• Replaces inheritance with composition |
| **Template Method** | Behavioral | • Defining the skeleton of an algorithm, deferring some steps to subclasses<br>• When common behavior among subclasses should be factored<br>• Controlling subclass extensions | • Reuses common code<br>• Focuses subclasses on specific steps<br>• Enforces a defined structure |
| **Visitor** | Behavioral | • When you need to perform operations on all elements of a complex structure<br>• When classes are rarely changed but operations on them frequently change<br>• When you need to add new operations without changing elements | • Separates algorithms from objects they operate on<br>• Makes adding new operations easy<br>• Gathers related operations into one class |
