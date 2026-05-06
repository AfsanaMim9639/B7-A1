# Stop Using `any`. Here's Why.

> You heard it's bad. Let's actually understand why — and what to use instead.

---

## What's the problem with `any`?

When you type something as `any`, TypeScript steps back completely. It stops checking. You can call any method, access any property, pass it anywhere — and TypeScript won't complain. Until runtime, that is.

```ts
// Bad — any lets everything through
function parseData(input: any) {
  console.log(input.name.toUpperCase()); // TypeScript: "looks fine!"
  // Runtime: Cannot read property 'name' of undefined
}
```

**TypeScript trusted you blindly. The bug sneaked straight to production.** That's what makes `any` a **type safety hole** — it's a trapdoor out of the type system.

---

## Enter `unknown` — the safe stranger

`unknown` is TypeScript's way of saying: *"I have no idea what this is — and neither should you, until you prove it."*

**Unlike `any`, you can't do anything with an `unknown` value until you verify what it actually is.** TypeScript forces you to check first.

```ts
// Bad — fails to compile, as it should
function parseData(input: unknown) {
  console.log(input.name); // Error: Object is of type 'unknown'
}
```

```ts
// Good — check before you use
function parseData(input: unknown) {
  if (
    typeof input === "object" &&
    input !== null &&
    "name" in input &&
    typeof (input as any).name === "string"
  ) {
    console.log(input.name.toUpperCase()); // Safe!
  }
}
```

---

## This is called Type Narrowing

**Type narrowing is the process of going from a broad type (like `unknown`) to a specific one (like `string` or `number`) by checking conditions.** TypeScript is smart enough to track your checks and automatically narrow the type inside that block.

```ts
function display(value: unknown) {
  if (typeof value === "string") {
    // TypeScript knows it's a string here
    console.log(value.toUpperCase()); // Safe
  } else if (typeof value === "number") {
    // TypeScript knows it's a number here
    console.log(value.toFixed(2)); // Safe
  }
}
```

> **The mental model:** `any` is trust without verification. `unknown` is trust, but verify first. Type narrowing is how you do the verification.

---

## When does this actually matter?

**Anytime data comes from outside your app — API responses, `JSON.parse()`, user input, third-party libraries — you genuinely don't know what shape it'll be.** That's exactly when `unknown` shines over `any`.

```ts
const raw: unknown = await fetch("/api/user").then(r => r.json());

// Now narrow it before trusting it
if (isValidUser(raw)) {
  console.log(raw.email); // Safe
}
```

---

**`any` opts you out of TypeScript. `unknown` keeps you in — and forces you to be honest about what you actually know. That's the whole deal.**