# The Four Pillars of OOP in TypeScript

## Introduction

Object-Oriented Programming — the name alone brings back memories of dry university lectures and abstract diagrams. But in large TypeScript projects, the four pillars of OOP — Encapsulation, Inheritance, Abstraction, and Polymorphism — are not just theory. They are real tools. Without them, maintaining a growing codebase becomes a nightmare.

In this post, we will walk through each pillar with real examples and see how they work together to manage logic and reduce complexity.

---

## Body

### 1. Encapsulation — hide what does not need to be seen

Encapsulation means bundling data and the logic that works on it together, while hiding internal details from the outside world. You expose only what is necessary.

```ts
// Bad — everything is exposed, anyone can break it
class BankAccount {
  balance: number = 0;
}

const account = new BankAccount();
account.balance = -99999; // nothing stops this
```

```ts
// Good — internal state is protected
class BankAccount {
  private balance: number = 0;

  deposit(amount: number): void {
    if (amount <= 0) throw new Error("Amount must be positive");
    this.balance += amount;
  }

  getBalance(): number {
    return this.balance;
  }
}

const account = new BankAccount();
account.deposit(500);
account.balance = -99999; // error — balance is private
```

**The outside world can only interact through controlled methods. Your internal logic stays safe from accidental misuse.**

---

### 2. Inheritance — share logic, do not repeat it

Inheritance lets a child class take on the properties and methods of a parent class. Shared logic lives in one place — every child class gets it automatically.

```ts
// Bad — duplicating the same logic across classes
class Dog {
  name: string;
  constructor(name: string) { this.name = name; }
  eat() { console.log(`${this.name} is eating`); }
  bark() { console.log("Woof!"); }
}

class Cat {
  name: string;
  constructor(name: string) { this.name = name; }
  eat() { console.log(`${this.name} is eating`); } // copied again
  meow() { console.log("Meow!"); }
}
```

```ts
// Good — shared logic lives in the parent
class Animal {
  constructor(public name: string) {}

  eat(): void {
    console.log(`${this.name} is eating`);
  }
}

class Dog extends Animal {
  bark(): void { console.log("Woof!"); }
}

class Cat extends Animal {
  meow(): void { console.log("Meow!"); }
}

const dog = new Dog("Rex");
dog.eat();  // inherited from Animal
dog.bark(); // Dog's own method
```

**Change `eat()` in one place — every child class gets the update. No hunting through files.**

---

### 3. Abstraction — define the shape, not the detail

Abstraction means defining what something should do without specifying how it does it. In TypeScript, this is achieved with `abstract` classes or interfaces.

```ts
// Define the contract — every payment method must have these
abstract class PaymentMethod {
  abstract pay(amount: number): void;
  abstract refund(amount: number): void;

  printReceipt(amount: number): void {
    console.log(`Transaction: $${amount}`);
  }
}

class CreditCard extends PaymentMethod {
  pay(amount: number): void {
    console.log(`Charging $${amount} to credit card`);
  }

  refund(amount: number): void {
    console.log(`Refunding $${amount} to credit card`);
  }
}

class PayPal extends PaymentMethod {
  pay(amount: number): void {
    console.log(`Sending $${amount} via PayPal`);
  }

  refund(amount: number): void {
    console.log(`Refunding $${amount} via PayPal`);
  }
}
```

**The rest of your app just calls `.pay()` and `.refund()` — it does not care whether it is a credit card, PayPal, or crypto. The complexity is hidden behind a clean contract.**

---

### 4. Polymorphism — one interface, many behaviors

Polymorphism means the same method call behaves differently depending on which class is behind it. You write one piece of code that works across many types.

```ts
// Same method name, different behavior per class
function processPayment(method: PaymentMethod, amount: number): void {
  method.pay(amount);
  method.printReceipt(amount);
}

const card   = new CreditCard();
const paypal = new PayPal();

processPayment(card, 100);   // Charging $100 to credit card
processPayment(paypal, 200); // Sending $200 via PayPal
```

**Adding a new payment method? Create a new class, implement `pay()` and `refund()`, and `processPayment()` works with it instantly — no changes needed.**

---

### How the four pillars work together

In a large-scale project, these four are not separate ideas — they stack on top of each other.

```ts
abstract class Notification {           // Abstraction
  protected message: string;            // Encapsulation

  constructor(message: string) {
    this.message = message;
  }

  abstract send(): void;

  log(): void {
    console.log(`[LOG] ${this.message}`);
  }
}

class EmailNotification extends Notification {   // Inheritance
  send(): void {                                 // Polymorphism
    console.log(`Sending email: ${this.message}`);
  }
}

class SMSNotification extends Notification {     // Inheritance
  send(): void {                                 // Polymorphism
    console.log(`Sending SMS: ${this.message}`);
  }
}

function notify(n: Notification): void {
  n.send(); // works for Email, SMS, or anything else you add
  n.log();
}
```

> **The big picture:** Encapsulation protects your data. Inheritance removes repetition. Abstraction hides complexity. Polymorphism makes your code flexible. Together, they make large TypeScript projects manageable — one clean class at a time.

---

## Conclusion

Many developers think OOP is overrated — until their project grows, the team expands, and features keep piling on. Without these four pillars, a codebase turns into a jungle that nobody wants to touch.

**OOP is not about following rules. It is about writing code that stays readable, changeable, and safe as your project grows to thousands of lines.**

Do not just memorize Encapsulation, Inheritance, Abstraction, and Polymorphism. The next time you write a class, ask yourself: am I actually using them?