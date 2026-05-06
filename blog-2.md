# Pick and Omit — your interface's best friends

> One big interface. Many different uses. No copy-pasting required.

---

## The problem

Imagine you have a `User` interface for your whole app. But your login form only needs email and password. Your profile card only shows name and avatar. Your admin panel needs everything except the password.

The bad move? Write a new interface for each. The DRY move? `Pick` and `Omit`.

---

## The master interface

Start with one source of truth — a single interface that holds all the fields.

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

## Pick — grab only what you need

`Pick<T, Keys>` creates a new type with only the fields you list. Think of it as saying "give me just these."

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

## Omit — drop what you don't want

`Omit<T, Keys>` is the opposite — it gives you everything except the fields you exclude. Think "give me all of it, minus these."

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

## Real world — one master, many slices

```ts
type LoginForm  = Pick<User, "email" | "password">;
type ProfileCard = Pick<User, "name" | "avatar" | "role">;
type PublicUser  = Omit<User, "password">;
type AdminView   = Omit<User, "avatar">;

// All derived from one interface.
// Change User once — everything stays in sync.
```

> **The DRY payoff:** your master interface is the single source of truth. `Pick` and `Omit` are lenses — they let you look at exactly the slice you need, without ever copy-pasting a single field.

---

**Duplicate interfaces are tech debt in disguise. One master interface plus `Pick` and `Omit` is all you need to keep things clean, consistent, and easy to change.**