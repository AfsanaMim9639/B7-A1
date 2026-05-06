# `Pick` and `Omit` — Keep Your Interfaces DRY

## Introduction

One of the most common mistakes in large TypeScript projects is copying the same interface over and over — tweaking it slightly for each use case. A separate one for the login form, another for the profile card, yet another for the admin view. This approach is called code duplication, and it is a slow poison.

`Pick` and `Omit` are two TypeScript utility types that solve this problem completely. You start with one master interface and carve out exactly the slices you need — no copy-pasting, no manual syncing, no silent bugs.

---

## Body

### The master interface — single source of truth

Everything starts with one complete interface that holds all the fields your domain needs.

```ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
  avatar: string;
  role: "admin" | "user";
  createdAt: Date;
}
```

**This is your single source of truth. Everything else derives from it.**

---

### `Pick` — grab only what you need

`Pick<T, Keys>` creates a new type using only the fields you list. Think of it as saying "give me just these."

```ts
// Bad — manual duplicate interface
interface LoginForm {
  email: string;    // copied from User
  password: string; // copied from User
  // if User changes, this breaks silently
}
```

```ts
// Good — Pick from master
type LoginForm = Pick<User, "email" | "password">;

// Result — TypeScript sees this as:
// { email: string; password: string; }
```

**Now if `User.email` ever changes type, `LoginForm` updates automatically. Zero maintenance.**

---

### `Omit` — drop what you do not want

`Omit<T, Keys>` does the opposite — it gives you everything except the fields you exclude. Think of it as "give me all of it, minus these."

```ts
// Bad — rewriting almost the whole thing
interface PublicUser {
  id: number;
  name: string;
  email: string;
  avatar: string;
  role: "admin" | "user";
  createdAt: Date;
  // forgot to add new fields when User changed? bug.
}
```

```ts
// Good — Omit from master
type PublicUser = Omit<User, "password">;

// Result — everything in User, except password
// { id, name, email, avatar, role, createdAt }
```

**If you add a new field to `User`, it automatically appears in `PublicUser` too. No manual syncing ever.**

---

### Real world — one master, many slices

```ts
type LoginForm   = Pick<User, "email" | "password">;
type ProfileCard = Pick<User, "name" | "avatar" | "role">;
type PublicUser  = Omit<User, "password">;
type AdminView   = Omit<User, "avatar">;

// All derived from one interface.
// Change User once — everything stays in sync.
```

> **The DRY payoff:** Your master interface is the single source of truth. `Pick` and `Omit` are lenses — they let you look at exactly the slice you need, without ever copy-pasting a single field.

---

## Conclusion

Duplicate interfaces mean duplicate bugs. Every time something changes in `User`, you have to manually update every copy — and missing even one creates a silent bug that is hard to track down.

**Duplicate interfaces are tech debt in disguise. One master interface plus `Pick` and `Omit` is all you need to keep things clean, consistent, and easy to change.**

Following the DRY principle in TypeScript is not difficult — you just need to know the right utility types.