# Prototype Design Pattern in TypeScript

[« Back to Project Readme](https://github.com/adamrichardturner/design-patterns/blob/main/README.md)

## What is the Prototype Design Pattern?

The **Prototype Design Pattern** is a creational design pattern that involves creating new objects by copying or "cloning" an existing object (the prototype). 

Rather than instantiating new objects from scratch, the prototype pattern leverages duplication of pre-existing instances.

This approach is especially useful when object creation is costly or complex. By cloning existing instances, the prototype pattern significantly simplifies and optimizes object creation.

## Why and When to Use the Prototype Pattern?

### Benefits:
- **Efficiency**: Reduces the overhead of object creation.
- **Flexibility**: Simplifies the creation of objects with similar states.
- **Avoids Complex Initialization**: Avoids repeating complex initialization logic.

### Use Prototype Pattern when:
- Creating objects is resource-intensive or complex.
- You frequently instantiate similar objects differing only slightly.
- You want to avoid subclassing for object creation.

## Example of Prototype Pattern in TypeScript

Let's illustrate the Prototype pattern with an example involving document templates:

### Step 1: Define the Prototype Interface

First, define an interface that declares a method for cloning itself:

```typescript
interface Prototype<T> {
  clone(): T;
}
```

### Step 2: Create Concrete Classes that Implement Prototype

Now create concrete classes representing documents:

```typescript
class DocumentTemplate implements Prototype<DocumentTemplate> {
  title: string;
  body: string;
  footer: string;

  constructor(title: string, body: string, footer: string) {
    this.title = title;
    this.body = body;
    this.footer = footer;
  }

  clone(): DocumentTemplate {
    return new DocumentTemplate(this.title, this.body, this.footer);
  }

  display(): void {
    console.log(`Title: ${this.title}\nBody: ${this.body}\nFooter: ${this.footer}`);
  }
}
```

### Step 3: Using the Prototype

Here's how you clone objects using the prototype:

```typescript
// Original object creation (prototype)
const invoiceTemplate = new DocumentTemplate(
  "Invoice Template",
  "Invoice Body: Customer Details, Items, Total.",
  "Invoice Footer: Company Details"
);

// Cloning the prototype
const clonedInvoice = invoiceTemplate.clone();

// Modifying the cloned object without affecting the original
clonedInvoice.title = "Invoice for John Doe";
clonedInvoice.body = "Invoice Body: Customer John Doe, Items Ordered, Total: $100";

// Display documents
console.log("Original Template:");
invoiceTemplate.display();

console.log("\nCloned & Modified Invoice:");
clonedInvoice.display();
```

**Output:**
```
Original Template:
Title: Invoice Template
Body: Invoice Body: Customer Details, Items, Total.
Footer: Invoice Footer: Company Details

Cloned & Modified Invoice:
Title: Invoice for John Doe
Body: Invoice Body: Customer John Doe, Items Ordered, Total: $100
Footer: Invoice Footer: Company Details
```

## Deep vs. Shallow Cloning

In the above example, we performed shallow cloning because all fields were primitive types (`string`). 

If your object contains references to other objects, you might need **deep cloning** to avoid shared references.

### Example of Deep Cloning

```typescript
class DeepDocument implements Prototype<DeepDocument> {
  title: string;
  details: { [key: string]: string };

  constructor(title: string, details: { [key: string]: string }) {
    this.title = title;
    this.details = details;
  }

  clone(): DeepDocument {
    // Perform deep cloning using JSON methods
    const cloneDetails = JSON.parse(JSON.stringify(this.details));
    return new DeepDocument(this.title, cloneDetails);
  }
}

// Usage example:
const originalDoc = new DeepDocument("Report", { author: "Jane", status: "Draft" });
const clonedDoc = originalDoc.clone();

// Modifying cloned object's nested details
clonedDoc.details.status = "Final";

console.log("Original Document:", originalDoc);
console.log("Cloned Document:", clonedDoc);
```

This prevents changes in cloned objects from affecting the original object.

## Advantages of Using the Prototype Pattern

- Minimizes object creation cost.
- Easily replicates objects without complex construction.
- Reduces class hierarchy complexity.

## Conclusion

The Prototype Design Pattern provides an efficient way to clone complex objects, simplifying their creation. 

By leveraging cloning, you save resources and streamline object initialization, making it an effective choice for applications with performance-sensitive object creation or frequent replication.
