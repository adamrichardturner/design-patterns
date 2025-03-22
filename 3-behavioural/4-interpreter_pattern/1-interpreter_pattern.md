# Interpreter Design Pattern in TypeScript

[« Back to Project README](../../README.md)

## What is the Interpreter Pattern?

The **Interpreter Pattern** defines a grammar for interpreting the sentences in a language and provides an interpreter to deal with this grammar.

## Why and When to Use the Interpreter Pattern?

### Benefits:
- **Language Interpretation**: Helps in parsing and interpreting domain-specific languages
- **Rule Evaluation**: Useful for implementing rules engines or rule-based systems
- **Expression Evaluation**: Good for evaluating expressions in a particular context

### Use When:
- You need to interpret a domain-specific language
- The grammar is relatively simple and can be represented as abstract syntax trees
- Efficiency is not a critical concern

## Example of Interpreter Pattern in TypeScript

```typescript
// Expression interface
interface Expression {
  interpret(context: Record<string, boolean>): boolean;
}

// Terminal expressions
class VariableExpression implements Expression {
  private name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  interpret(context: Record<string, boolean>): boolean {
    return context[this.name] || false;
  }
}

// Non-terminal expressions
class AndExpression implements Expression {
  private left: Expression;
  private right: Expression;
  
  constructor(left: Expression, right: Expression) {
    this.left = left;
    this.right = right;
  }
  
  interpret(context: Record<string, boolean>): boolean {
    return this.left.interpret(context) && this.right.interpret(context);
  }
}

class OrExpression implements Expression {
  private left: Expression;
  private right: Expression;
  
  constructor(left: Expression, right: Expression) {
    this.left = left;
    this.right = right;
  }
  
  interpret(context: Record<string, boolean>): boolean {
    return this.left.interpret(context) || this.right.interpret(context);
  }
}

class NotExpression implements Expression {
  private expression: Expression;
  
  constructor(expression: Expression) {
    this.expression = expression;
  }
  
  interpret(context: Record<string, boolean>): boolean {
    return !this.expression.interpret(context);
  }
}

// Client code
const context: Record<string, boolean> = { x: true, y: false };

const x = new VariableExpression('x');
const y = new VariableExpression('y');
const andExpression = new AndExpression(x, y);
const orExpression = new OrExpression(x, y);
const notExpression = new NotExpression(y);

console.log(`x AND y = ${andExpression.interpret(context)}`); // false
console.log(`x OR y = ${orExpression.interpret(context)}`);   // true
console.log(`NOT y = ${notExpression.interpret(context)}`);   // true
```

## Conclusion

The Interpreter Pattern is powerful for parsing and evaluating expressions in a domain-specific language. While it can become complex for large grammars, it's excellent for simple language interpretation needs.
