# Generics — Write Once, Work With Anything

## Introduction

A function that only works with `string` is not reusable. A function written with `any` loses type safety entirely. There is a perfect solution sitting right between those two extremes — Generics.

Generics let you write functions and components that work with any type while keeping TypeScript's full type safety intact. Write it once, use it everywhere, and TypeScript figures out the types automatically.

---

## Body

### The problem without Generics

Say you want a function that returns the first item of an array. Simple enough — but what type does it return?

```ts
// Bad — loses all type information
function first(arr: any[]): any {
  return arr[0];
}

const name = first(["Alice", "Bob"]); // TypeScript thinks: any
name.toUpperCase(); // no autocomplete, no safety
```

**You threw away all the type info the moment you wrote `any`. TypeScript cannot help you anymore.**

---

### Enter Generics

A Generic is a type placeholder. You write `<T>` and TypeScript figures out the actual type when the function is called.

```ts
// Good — Generic keeps the type alive
function first<T>(arr: T[]): T {
  return arr[0];
}

const name = first(["Alice", "Bob"]); // TypeScript knows: string
const num  = first([10, 20, 30]);     // TypeScript knows: number

name.toUpperCase(); // autocomplete works
num.toFixed(2);     // autocomplete works
```

**Same function, any type, full safety. That is the whole point of Generics.**

---

### How it works

When you call `first(["Alice", "Bob"])`, TypeScript looks at what you passed in, sees `string[]`, and automatically replaces `T` with `string`. You never have to specify it manually — TypeScript infers it.

```ts
first<string>(["Alice", "Bob"]); // explicit — works
first(["Alice", "Bob"]);         // inferred — also works, cleaner
```

---

### Reusable components — a real example

Say you want an API response wrapper that works for any kind of data.

```ts
// Bad — one interface per response type
interface UserResponse {
  data: User;
  error: string | null;
  loading: boolean;
}

interface ProductResponse {
  data: Product;
  error: string | null;
  loading: boolean;
}

// duplicating the same shape over and over...
```

```ts
// Good — one Generic interface for all responses
interface ApiResponse<T> {
  data: T;
  error: string | null;
  loading: boolean;
}

type UserResponse    = ApiResponse<User>;
type ProductResponse = ApiResponse<Product>;
type OrderResponse   = ApiResponse<Order>;
```

**One interface. Infinite reuse. If you change the shape, every response type updates automatically.**

---

### Generic functions with constraints

Sometimes you want `T` to be flexible but not completely open. Use `extends` to constrain it.

```ts
// T must have an "id" field — nothing else required
function findById<T extends { id: number }>(items: T[], id: number): T | undefined {
  return items.find(item => item.id === id);
}

findById(users, 1);     // works — User has id
findById(products, 5);  // works — Product has id
findById([1, 2, 3], 1); // error — number has no id
```

**Constraints let you be flexible without being reckless.**

---

### Multiple type parameters

Generics can take more than one placeholder. A classic example — a function that pairs two values of any type.

```ts
function pair<A, B>(first: A, second: B): [A, B] {
  return [first, second];
}

pair("hello", 42);     // [string, number]
pair(true, { x: 10 }); // [boolean, { x: number }]
```

---

### Real world — a generic fetch wrapper

```ts
async function fetchData<T>(url: string): Promise<T> {
  const res = await fetch(url);
  return res.json() as T;
}

const user    = await fetchData<User>("/api/user");
const product = await fetchData<Product>("/api/product");

console.log(user.name);     // autocomplete works
console.log(product.price); // autocomplete works
```

**Without Generics, you get `any` back from every fetch. With Generics, TypeScript knows the exact shape of every response.**

> **The mental model:** Generics are like function parameters, but for types. Instead of passing a value, you pass a type — and TypeScript uses it to keep everything consistent end to end.

---

## Conclusion

Generics might look intimidating at first — seeing `<T>` feels like things just got complicated. But the core idea is simple: treat a type like a parameter.

**Generics are what separates a reusable utility from a one-trick function. Write it once, pass any type, and TypeScript keeps you safe the whole way through.**

Once you get comfortable with the Generic pattern, you will never want to reach for `any` again.