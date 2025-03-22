# Observer Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Observer Pattern?

The **Observer Pattern** defines a one-to-many dependency between objects, so when one object (subject) changes its state, all its dependents (observers) are notified automatically.

## Why and When to Use the Observer Pattern?

### Benefits:
- **Loose coupling**: Observers and subjects are independent.
- **Dynamic relationships**: Observers can be added or removed easily.
- **Broadcast communication**: Easily inform multiple observers about state changes.

### Use the Observer Pattern when:
- Multiple objects need to receive updates about state changes.
- You want to decouple classes and reduce dependencies.

## Example of Observer Pattern in TypeScript

### Step 1: Observer Interface

```typescript
interface Observer {
  update(state: string): void;
}
```

### Step 2: Subject Interface

```typescript
interface Subject {
  registerObserver(observer: Observer): void;
  removeObserver(observer: Observer): void;
  notifyObservers(): void;
}
```

### Step 3: Concrete Subject

```typescript
class WeatherStation implements Subject {
  private observers: Observer[] = [];
  private state: string = '';

  registerObserver(observer: Observer): void {
    this.observers.push(observer);
  }

  removeObserver(observer: Observer): void {
    this.observers = this.observers.filter(obs => obs !== observer);
  }

  notifyObservers(): void {
    this.observers.forEach(observer => observer.update(this.state));
  }

  setState(state: string): void {
    console.log(`WeatherStation: New state is '${state}'`);
    this.state = state;
    this.notifyObservers();
  }
}
```

### Step 4: Concrete Observers

```typescript
class PhoneDisplay implements Observer {
  update(state: string): void {
    console.log(`Phone Display: The weather is '${state}'.`);
  }
}

class TVDisplay implements Observer {
  update(state: string): void {
    console.log(`TV Display: Weather update - '${state}'.`);
  }
}
```

### Step 5: Using the Observer Pattern

```typescript
const weatherStation = new WeatherStation();

const phoneDisplay = new PhoneDisplay();
const tvDisplay = new TVDisplay();

weatherStation.registerObserver(phoneDisplay);
weatherStation.registerObserver(tvDisplay);

weatherStation.setState("Sunny");
weatherStation.setState("Rainy");

weatherStation.removeObserver(phoneDisplay);
weatherStation.setState("Windy");
```

### Output
```
WeatherStation: New state is 'Sunny'
Phone Display: The weather is 'Sunny'.
TV Display: Weather update - 'Sunny'.

WeatherStation: New state is 'Rainy'
Phone Display: The weather is 'Rainy'.
TV Display: Weather update - 'Rainy'.

WeatherStation: New state is 'Windy'
TV Display: Weather update - 'Windy'.
```

## Conclusion

The Observer Pattern efficiently manages multiple observers, providing dynamic and loosely coupled communication between objects.