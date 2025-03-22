# Factory Design Pattern in TypeScript

## What is the Factory Design Pattern?

The **Factory Design Pattern** is a creational design pattern used to encapsulate object creation logic. Instead of directly creating an instance of a class with the `new` keyword, the factory pattern provides an interface or method to instantiate objects, allowing subclasses or helper methods to determine the specific class to instantiate.

This pattern is beneficial when the exact class of an object cannot be determined until runtime or when you want to separate and centralize object creation logic from the rest of your code.

## Why and When to Use the Factory Pattern?

The factory pattern offers several key benefits:

- **Encapsulation**: Creation logic is centralized, simplifying maintenance and updates.
- **Decoupling**: The code using objects only depends on an interface or abstract class, not on concrete implementations.
- **Flexibility**: Easily swap or extend objects without changing client code.

Use the factory pattern when:

- You have several related classes, and you want to instantiate them dynamically.
- The type of object to create depends on runtime conditions or configurations.
- You want to simplify object creation logic in a complex application.

## Example of Factory Pattern in TypeScript

Let's explore the factory pattern with a general-purpose example involving payment methods.

### Define the Interface and Concrete Classes

First, create an interface representing a generic payment method:

```typescript
interface PaymentMethod {
  pay(amount: number): void;
}

class CreditCardPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Paid $${amount} using Credit Card.`);
  }
}

class PayPalPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Paid $${amount} using PayPal.`);
  }
}

class BitcoinPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Paid $${amount} using Bitcoin.`);
  }
}
```

**Explanation**:  
We have an interface `PaymentMethod` with a method `pay(amount: number)`. Each concrete class (`CreditCardPayment`, `PayPalPayment`, and `BitcoinPayment`) implements this interface and provides its own version of the `pay` method.

### Implementing the Factory

Now, create a factory class responsible for instantiating the appropriate payment method based on input:

```typescript
type PaymentType = 'creditCard' | 'paypal' | 'bitcoin';

class PaymentFactory {
  static createPaymentMethod(type: PaymentType): PaymentMethod {
    switch (type) {
      case 'creditCard':
        return new CreditCardPayment();
      case 'paypal':
        return new PayPalPayment();
      case 'bitcoin':
        return new BitcoinPayment();
      default:
        throw new Error(`Payment method ${type} not supported.`);
    }
  }
}
```

**Explanation**:  
The `PaymentFactory` class has a static method `createPaymentMethod` that accepts a type parameter and returns an instance of the corresponding class. This centralizes the logic for creating payment method instances.

### Using the Factory

Here's how you might use the factory to create and use a payment method dynamically:

```typescript
// Client code
const paymentType: PaymentType = 'paypal';
const paymentMethod: PaymentMethod = PaymentFactory.createPaymentMethod(paymentType);

paymentMethod.pay(150);
```

**Output:**
```
Paid $150 using PayPal.
```

**Explanation**:  
The client code doesn't directly create the instance of the payment method. Instead, it asks the `PaymentFactory` for the appropriate instance based on a runtime value (`paymentType`).

### Extending the Factory

Suppose you want to add a new payment type, `ApplePay`. Simply:

1. Implement the new class:

```typescript
class ApplePayPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Paid $${amount} using Apple Pay.`);
  }
}
```

2. Update the factory method:

```typescript
type PaymentType = 'creditCard' | 'paypal' | 'bitcoin' | 'applePay';

class PaymentFactory {
  static createPaymentMethod(type: PaymentType): PaymentMethod {
    switch (type) {
      case 'creditCard':
        return new CreditCardPayment();
      case 'paypal':
        return new PayPalPayment();
      case 'bitcoin':
        return new BitcoinPayment();
      case 'applePay':
        return new ApplePayPayment();
      default:
        throw new Error(`Payment method ${type} not supported.`);
    }
  }
}
```

The rest of your application can now use `applePay` without modifying existing code, thanks to the encapsulation provided by the factory pattern.

## Conclusion

The Factory Design Pattern simplifies object creation and provides a clear abstraction layer, improving maintainability and flexibility. By centralizing creation logic, it's easy to manage, extend, and modify classes without affecting client code, making it a robust solution for many practical scenarios.

