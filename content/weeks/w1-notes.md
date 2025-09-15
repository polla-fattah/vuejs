---
title: "Week 1 — TypeScript for Java Developers "
description: "TypeScript setup, strict typing, unions, narrowing, generics, async/await — with runnable examples for Node"
date: 2025-09-07T00:00:00+02:00
lastmod: 2025-09-07T00:00:00+02:00
draft: false
weight: 1
toc: true
seo:
  title: "Week 1 — TypeScript for Java Developers"
  description: "TypeScript setup, strict typing, unions, narrowing, generics, async/await — with runnable examples for Node"
  canonical: ""
  noindex: false
---

> **Goal:** Learn TypeScript language fundamentals (without frameworks), focusing on what differs from Java:
> strict typing, unions, narrowing, structural typing, async/await, and good error handling.

---

## 0) How we run TypeScript this week

### Quick project scaffold (Node + TS)
```bash
mkdir ts-week1 && cd ts-week1
npm init -y
npm i -D typescript ts-node @types/node
npx tsc --init
````

**Recommended `tsconfig.json` (strict + modern):**

```jsonc
{
  "compilerOptions": {
    "target": "ES2021",
    "module": "ES2020",
    "moduleResolution": "bundler",
    "strict": true,
    "noImplicitAny": true,
    "exactOptionalPropertyTypes": true,
    "noUncheckedIndexedAccess": true,
    "useUnknownInCatchVariables": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "outDir": "dist",
    "rootDir": "src"
  },
  "include": ["src"]
}
```

**Scripts** in `package.json`:

```json
{
  "type": "module",
  "scripts": {
    "dev": "ts-node src/main.ts",
    "build": "tsc -p tsconfig.json",
    "start": "node dist/main.js",
    "type-check": "tsc -p tsconfig.json --noEmit"
  }
}
```

Create `src/main.ts` and run:

```bash
npm run dev      # run with ts-node (fast)
npm run build && npm start  # compile to JS then run
npm run type-check          # only types
```

---

## 1) TypeScript vs Java — the key mindset shifts

### 1.1 Structural typing (vs Java’s nominal typing)

In TS, compatibility is **shape-based**, not class-name based.

```ts
type Point = { x: number; y: number }
class Pixel { constructor(public x: number, public y: number) {} }

const p: Point = new Pixel(1, 2)   // ✅ OK: same structure (x:number, y:number)
```

### 1.2 Top/bottom types

* **`unknown`** = safe top type (prefer over `any`)
* **`any`** = escape hatch (turns off type safety)
* **`never`** = impossible value (exhaustiveness checks)

```ts
function fail(msg: string): never { throw new Error(msg) }
```

### 1.3 `null` & `undefined` with `strictNullChecks`

Nullability is explicit: `string | null` etc. No implicit “nullable everything”.

```ts
function len(s: string | null): number {
  if (s === null) return 0
  return s.length
}
```

---

## 2) Variables, literals, and inference

### 2.1 `const` vs `let` + inference

```ts
let a = 42           // inferred number
a = 100              // OK
// a = "hi"          // ❌ error

const msg = "ready"  // inferred "ready" (literal type)
```

**Const assertion:**

```ts
const cfg = { mode: "dark", pageSize: 20 } as const
// cfg.mode is "dark", not string
```

### 2.2 Narrowing with `typeof`, `== null`, optional chaining, nullish coalescing

```ts
function norm(v: number | null | undefined): number {
  if (v == null) return 0         // null or undefined
  return v
}

type U = string | number
function format(u: U) {
  return typeof u === "number" ? u.toFixed(2) : u.toUpperCase()
}

const maybeLen = (s?: string) => s?.length ?? 0
```

**Practice**

* Write `toBoolean(x: unknown): boolean` returning `false` for `null/undefined/""/0/NaN`, else `true` (use narrowings).
* Use const assertions to freeze a small config and observe literal types.

---

## 3) Objects, interfaces, and exact optionals

### 3.1 Interfaces vs type aliases (both fine)

```ts
interface User { id: number; name: string; email?: string }
type Id = number | string
type UserMap = Record<Id, User>
```

### 3.2 Optional & readonly

```ts
interface Profile {
  readonly id: number
  nickname?: string         // may be missing
}
```

With `"exactOptionalPropertyTypes": true`, `nickname?: string` means:

* If present, it’s **exactly** `string`
* If absent, property is **not there** (not `undefined` value)

### 3.3 Index signatures & `Record`

```ts
type Counts = Record<string, number>
const c: Counts = { apples: 2, pears: 1 }
```

**Practice**

* Define `Product { id:number; title:string; price:number; tags?: readonly string[] }`.
  Create `Record<number, Product>` and write a function to calculate average price.

---

## 4) Arrays, tuples, ReadonlyArray

```ts
const nums: number[] = [1, 2, 3]
const names: Array<string> = ["Ava", "Bilal"]    // same

const point: [number, number] = [10, 20]
const labelled: [id: number, name: string] = [1, "sensor"]

function pair<T, U>(a: T, b: U): [T, U] { return [a, b] }
const p = pair("x", 10) // [string, number]

const ro: ReadonlyArray<number> = [1, 2, 3]
// ro.push(4) // ❌ cannot mutate
```

**Practice**

* Create a tuple `[string, number, boolean]` and a function to pretty-print it.
* Convert a mutable `string[]` to `readonly string[]` and show compile error on mutation.

---

## 5) Functions, overloads, call signatures

### 5.1 Parameters & returns

```ts
function sum(a: number, b: number): number { return a + b }
const toUpper = (s: string): string => s.toUpperCase()
```

### 5.2 Default, rest

```ts
function greet(name = "friend"): string { return `Hello, ${name}` }
function total(...ns: number[]): number { return ns.reduce((a,n)=>a+n,0) }
```

### 5.3 Overloads (single impl)

```ts
function pick(x: string): string
function pick(x: number): number
function pick(x: string | number) { return x }
```

**Practice**

* Overload `get(id:number)` returns `User`, `get(name:string)` returns `User[]`.
* Write `mapValues<T,U>(obj: Record<string,T>, f:(t:T)=>U): Record<string,U>`.

---

## 6) Union & literal types, narrowing & predicates

### 6.1 Literal unions

```ts
type Role = "admin" | "staff" | "student"
function canEdit(r: Role): boolean { return r === "admin" }
```

### 6.2 `in`, `instanceof`, equality guards

```ts
type A = { kind: "a"; a: number }
type B = { kind: "b"; b: string }
type AB = A | B

function handle(x: AB) {
  switch (x.kind) {
    case "a": return x.a * 2
    case "b": return x.b.length
    default:  const _exhaustive: never = x; return _exhaustive
  }
}
```

### 6.3 User-defined type predicates

```ts
type Person = { name: string }
function isPerson(v: unknown): v is Person {
  return typeof v === "object" && v !== null && "name" in v
}
```

**Practice**

* Create a discriminated union for API responses:
  `{ type:"ok"; data:T } | { type:"error"; message:string }` and write a `handle` function with exhaustive `switch`.
* Add a predicate `isUser(u: unknown): u is User`.

---

## 7) Generics (practical minimum)

```ts
function first<T>(arr: T[]): T | undefined { return arr[0] }

interface Box<T> { value: T }
function wrap<T>(value: T): Box<T> { return { value } }

function getProp<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key]
}
```

Default type parameters:

```ts
interface Cache<T = string> { data: T[] }
const c1: Cache = { data: ["a"] }        // T=string
const c2: Cache<number> = { data: [1] }  // T=number
```

**Practice**

* Write `groupBy<T, K extends keyof any>(items: T[], key: (x:T)=>K): Record<K, T[]>`.
* Create `Maybe<T> = { kind:"some"; value:T } | { kind:"none" }` + helpers.

---

## 8) Type tools you’ll actually use

### 8.1 `keyof`, indexed access, `typeof` (in types)

```ts
type User = { id: number; name: string; email?: string }
type UserKey = keyof User            // "id" | "name" | "email"
type UserId = User["id"]             // number
const sample = { a: 1, b: "x" }
type Sample = typeof sample          // { a: number; b: string }
```

### 8.2 Utility types

```ts
type PartialUser   = Partial<User>
type RequiredUser  = Required<User>
type ReadonlyUser  = Readonly<User>
type UserPreview   = Pick<User, "id" | "name">
type UserSansEmail = Omit<User, "email">
```

### 8.3 Assertions vs `satisfies` (prefer `satisfies`)

```ts
// ✅ satisfies checks *without* changing the inferred type
const cfg = { host: "localhost", port: 5432 } satisfies { host: string; port: number }

// ❗ assertion forces the type, may be wrong at runtime
const forced = "42" as unknown as number
```

**Practice**

* Build `DeepReadonly<T>` for an object of depth 1 (bonus: recurse).
* Use `satisfies` to validate a constant configuration object.

---

## 9) Errors & result types (safer than exceptions everywhere)

### 9.1 `unknown` in catch (with `useUnknownInCatchVariables`)

```ts
try {
  JSON.parse("{bad")
} catch (e: unknown) {
  if (e instanceof SyntaxError) console.error("JSON error:", e.message)
}
```

### 9.2 Result pattern (discriminated union)

```ts
type Ok<T> = { ok: true;  value: T }
type Err   = { ok: false; error: string }
type Result<T> = Ok<T> | Err

function ok<T>(v: T): Ok<T> { return { ok: true, value: v } }
function err(msg: string): Err { return { ok: false, error: msg } }
```

**Practice**

* Implement `safeParse<T>(json: string): Result<T>` using `unknown` in catch.
* Write `unwrap<T>(r: Result<T>): T` that throws if `ok:false`.

---

## 10) Async TypeScript: Promises & async/await (typed)

### 10.1 Promise basics (type param)

```ts
const delay = (ms: number): Promise<void> =>
  new Promise(res => setTimeout(res, ms))

async function demo(): Promise<number> {
  await delay(100)
  return 42
}
```

### 10.2 Chaining vs async/await

```ts
function getRandomAsync(): Promise<number> {
  return new Promise(res => setTimeout(() => res(Math.random()), 200))
}

getRandomAsync()
  .then(n => n * 100)
  .then(n => console.log("then:", n))

;(async () => {
  const n = await getRandomAsync()
  console.log("await:", n * 100)
})()
```

### 10.3 Parallel & racing

```ts
async function parallel() {
  const [a, b] = await Promise.all([getRandomAsync(), getRandomAsync()])
  console.log(a, b)
}
async function fastest() {
  const first = await Promise.race([getRandomAsync(), getRandomAsync()])
  console.log("first:", first)
}
```

### 10.4 Typed fetch (simulate without DOM libs)

```ts
type Post = { id: number; title: string }

async function fetchPost(id: number): Promise<Result<Post>> {
  await delay(100)
  if (id <= 0) return err("invalid id")
  return ok({ id, title: `Post #${id}` })
}

(async () => {
  const r = await fetchPost(1)
  if (r.ok) console.log(r.value.title)
  else console.error(r.error)
})()
```

**Practice**

* Write `retry<T>(fn: () => Promise<T>, times: number): Promise<T>` with backoff.
* Create `timeout<T>(p: Promise<T>, ms: number): Promise<T>` that rejects on timeout.

---

## 11) Section practices (quick drills)

* **Unions & Narrowing:** Write `toNumber(x: string | number | boolean): number` with guards.
* **Predicates:** `isNonEmptyString(v: unknown): v is string`. Use in a filter.
* **Generics:** `pluck<T, K extends keyof T>(arr: T[], key: K): T[K][]`.
* **Utility Types:** turn `User` into a readonly form with only `id` and `name`.
* **Async:** fetch two posts in parallel, combine titles: `Promise.all`.

---

## 12) End-of-week TypeScript mini-project (no libs)

**Project:** *Typed Address Book (asynchronous, no I/O libraries)*
**You’ll use:** interfaces, unions, generics, discriminated results, async/await.

### 12.1 Types

```ts
export interface Contact {
  id: number
  name: string
  email?: string
  phone?: string
}

export type Id = Contact["id"]

export type Result<T> =
  | { ok: true; value: T }
  | { ok: false; error: string }

export const ok = <T>(value: T): Result<T> => ({ ok: true, value })
export const err = (error: string): Result<never> => ({ ok: false, error })
```

### 12.2 Store (closure + typed async API)

```ts
export function createStore() {
  let seq = 0
  let contacts: Contact[] = []

  const delay = <T>(ms: number, value: T, reject = false) =>
    new Promise<T>((res, rej) => setTimeout(() => reject ? rej(value as any) : res(value), ms))

  async function add(c: Omit<Contact, "id">): Promise<Result<Id>> {
    const id = ++seq
    contacts.push({ id, ...c })
    await delay(150, null)
    return ok(id)
  }

  async function list(): Promise<Result<ReadonlyArray<Contact>>> {
    await delay(50, null)
    return ok(contacts.map(c => ({ ...c })))
  }

  async function get(id: Id): Promise<Result<Contact>> {
    await delay(80, null)
    const found = contacts.find(c => c.id === id)
    return found ? ok({ ...found }) : err("not found")
  }

  async function update(id: Id, patch: Partial<Omit<Contact, "id">>): Promise<Result<Contact>> {
    await delay(100, null)
    const i = contacts.findIndex(c => c.id === id)
    if (i < 0) return err("not found")
    contacts[i] = { ...contacts[i], ...patch }
    return ok({ ...contacts[i] })
  }

  async function remove(id: Id): Promise<Result<boolean>> {
    await delay(120, null)
    const i = contacts.findIndex(c => c.id === id)
    if (i < 0) return err("not found")
    contacts.splice(i, 1)
    return ok(true)
  }

  return { add, list, get, update, remove }
}
```

### 12.3 Demo script (`src/main.ts`)

```ts
import { createStore } from "./store.js"

async function main() {
  const store = createStore()

  // 1) add two in parallel
  const [a, b] = await Promise.all([
    store.add({ name: "Ava", email: "ava@example.com" }),
    store.add({ name: "Bilal", phone: "0750-000-0000" })
  ])
  if (!a.ok || !b.ok) throw new Error("add failed")

  // 2) list
  const l = await store.list()
  if (l.ok) console.log("List:", l.value)

  // 3) update first
  const u = await store.update(a.value, { phone: "0750-111-2222" })
  if (u.ok) console.log("Updated:", u.value)

  // 4) get first
  const g = await store.get(a.value)
  if (g.ok) console.log("Get:", g.value)

  // 5) remove second and list
  await store.remove(b.value)
  const l2 = await store.list()
  if (l2.ok) console.log("After delete:", l2.value)
}

main().catch(e => console.error("Fatal:", e))
```

**Extensions (choose any):**

* Add `type ContactEvent = { type:"created"|"updated"|"deleted"; at: number; contactId: Id }` and keep an in-memory event log.
* Implement `search(q:string): Promise<Result<Contact[]>>` (prefix match on name/email/phone).
* Add `export/import` to/from JSON (use `JSON.parse`/`JSON.stringify`; remember to type values).

---

## 13) Glossary (TS terms you’ll see a lot)

* **Structural typing:** compatibility by shape, not by name.
* **Union types:** `A | B` — value may be one of several forms.
* **Narrowing:** refining a union via checks (`typeof`, `in`, `instanceof`, predicates).
* **Discriminated union:** union where each variant has a distinct literal tag (`kind`, `type`).
* **Utility types:** `Partial`, `Pick`, `Omit`, `Readonly`, `Record`, etc.
* **`unknown` vs `any`:** `unknown` forces you to **check** before use; `any` disables checking.
* **`never`:** unreachable/contradictory type (great for exhaustiveness tests).
* **Exact optionals:** optional props, if present, must match their type exactly.

---

> Next we can layer on: **modules & packaging best-practices**, **testing TypeScript** (Vitest), and then connect these foundations to **Vue’s Composition API** in Week 2+.


---

**Back to [Week 1 Plan](../w1/)**
