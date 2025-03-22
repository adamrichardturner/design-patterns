# Singleton Design Pattern in TypeScript

## What is the Singleton Design Pattern?

The **Singleton Design Pattern** is a creational pattern that ensures a class has only one instance and provides a global point of access to that instance. Singleton is useful for scenarios where exactly one instance of a class is needed to coordinate actions across a system.

Typical use cases include configuration classes, logging, or managing shared resources such as database connections.

## Why and When to Use the Singleton Pattern?

### Benefits:
- **Controlled Access**: Ensures only one instance of a class.
- **Resource Efficiency**: Manages shared resources effectively.
- **Global Accessibility**: Provides a global point of access.

### Use Singleton Pattern when:
- Exactly one instance of a class is required.
- Shared resources must be consistently managed.
- You want to provide global accessibility to that single instance.

## Example of Singleton Pattern in TypeScript

Let's explore the Singleton pattern with a simple configuration manager example.

### Step 1: Implement Singleton Class

```typescript
class ConfigurationManager {
  private static instance: ConfigurationManager;
  private configuration: { [key: string]: string };

  // Private constructor to prevent external instantiation
  private constructor() {
    this.configuration = {};
  }

  // Static method to provide global access point
  public static getInstance(): ConfigurationManager {
    if (!ConfigurationManager.instance) {
      ConfigurationManager.instance = new ConfigurationManager();
    }
    return ConfigurationManager.instance;
  }

  // Example methods to manage configuration
  public setConfig(key: string, value: string): void {
    this.configuration[key] = value;
  }

  public getConfig(key: string): string | undefined {
    return this.configuration[key];
  }
}
```

### Step 2: Using the Singleton

Here's how to access and use the singleton:

```typescript
// Retrieve the singleton instance
const configManager = ConfigurationManager.getInstance();

// Set some configuration
configManager.setConfig("appName", "My Application");
configManager.setConfig("version", "1.0.0");

// Retrieve the same singleton instance elsewhere in your application
const anotherConfigReference = ConfigurationManager.getInstance();

console.log(anotherConfigReference.getConfig("appName")); // Output: My Application
console.log(anotherConfigReference.getConfig("version")); // Output: 1.0.0
```

### Step 3: Verify Singleton Behavior

Let's verify that both references point to the same instance:

```typescript
console.log(configManager === anotherConfigReference); // Output: true
```

This output confirms both variables reference the same singleton instance.

## Singleton with Lazy Initialization

The Singleton pattern shown above uses lazy initialization, meaning the instance is created only when first requested. This approach helps in conserving resources if the instance isn't immediately needed.

## Thread Safety (Note)

JavaScript and TypeScript run in single-threaded environments (except Web Workers). Therefore, thread safety is usually not an issue. However, in multi-threaded languages or environments, additional synchronization is needed.

## Advantages and Considerations

### Advantages:
- Ensures consistent management of shared resources.
- Reduces memory usage by reusing a single instance.
- Provides a clear, global access point.

### Considerations:
- Can introduce global state, making testing harder.
- Should be used carefully to avoid hidden dependencies.

## Conclusion

The Singleton Design Pattern provides an effective way to manage single-instance objects like configurations, logging services, or database connections. It ensures controlled and consistent access to critical shared resources, making your application easier to manage and maintain.