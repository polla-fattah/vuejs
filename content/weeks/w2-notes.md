---
title: "Week 2 – Components & Reactivity Essentials"
description: "SFC anatomy, Composition API basics, core directives, props/emits, slots, and v-model"
date: 2025-09-14T00:00:00+02:00
lastmod: 2025-09-14T00:00:00+02:00
draft: false
weight: 2
toc: true
seo:
  title: "Week 2 – Components & Reactivity Essentials"
  description: "SFC anatomy, Composition API basics, core directives, props/emits, slots, and v-model"
  canonical: ""
  noindex: false
---



**Duration:** Sept 14–20, 2025

**Focus:** Mastering Vue component fundamentals before starting the capstone (capstone begins Week 3).

### You will learn to

- Create Single File Components (SFCs) structured with `<template>`, `<script setup lang="ts">`, and `<style scoped>` sections.
- Use Vue’s **Composition API** basics – `ref`, `reactive`, `computed` – and understand template ref unwrapping (refs don’t need `.value` *in templates*).
- Apply core directives in templates:
  `v-bind` (`:` shorthand) and `v-on` (`@` shorthand) with modifiers (e.g. `.prevent`);
  conditional rendering with `v-if` vs. `v-show`;
  list rendering with `v-for` (and stable `:key`);
  two-way binding with `v-model` for form inputs.
- Design clean **component APIs** with strictly typed **props** and **emits** (no `any`). Understand one-way data flow (**props down, events up**) and how to use `defineProps` / `defineEmits` in `<script setup>`.
- Compose interfaces with **slots**: use default slots for flexible content, named slots for specific layout regions, and basic **scoped slots** to pass data from child to parent slot content.

> *Deferred to later weeks:* lifecycle hooks, provide/inject, global state with Pinia, advanced slot patterns.

---

## Lab (W2): Reusable Card & Input (Typed)

**Due:** Sept 20, 2025

**Build**

- **`Card.vue`**
  Props: `title: string`, `variant?: 'elevated'|'flat'`, `as?: 'article'|'section'|'div'`
  Emits: `'confirm'`, `'close'`
  Slots: `header` (named), **default** (body), `footer` (named, **scoped** exposes `{ confirm }`)

- **`TextInput.vue`**
  Implements the `v-model` contract with `modelValue: string` and `update:modelValue`.

**Demonstrate**

- A parent view using two `<Card>`s (flat/elevated) with custom header/footer content.
- Inside one Card, a small form using `TextInput.vue` with `v-model` binding; display live value.
- Use `@submit.prevent`, `v-for` with stable `:key`, and `v-if`/`v-show`.

**Deliverables**

- Repo: `webapp-w2-[your-username]`
- Components: `Card.vue`, `TextInput.vue`, demo view (`App.vue` or `pages/ComponentsDemo.vue`)
- All props/emits **typed** (no `any`)

---

## Reading List

**Course Textbook**
- Simone Cuomo, *Vue.js 3 for Beginners* (Packt, 2024) — eBook or Paperback.

**Primary Documentation (Vue 3)**
- Components Basics
- Props
- Events (`defineEmits`)
- Component `v-model`
- Slots (default, named, scoped)
- Reactivity Fundamentals (`ref`, `reactive`, `computed`)
- Template Syntax (`v-bind`, `v-on`, `v-if`, `v-show`, `v-for`, `v-model`)
- SFCs & `<script setup>` (with TypeScript)

**Supplemental**
- Class & Style Bindings (`:class`, `:style`)
- Form Input Bindings (`v-model` modifiers: `.lazy`, `.number`, `.trim`)
- Style Scoping (`<style scoped>`, CSS Modules)

---

## Single File Component Anatomy

Vue **Single File Components (SFCs)** are `.vue` files that encapsulate a component’s template, logic, and styles in one place.

**Example – Basic SFC structure**

```vue
<!-- HelloWorld.vue -->
<template>
  <p class="greeting">{{ message }}</p>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const message = ref('Hello World!')
</script>

<style scoped>
.greeting {
  color: red;
  font-weight: bold;
}
</style>
````

**Notes**

* `<script setup>` auto-exposes top-level variables to the template (no `return` needed).
* `lang="ts"` enables TypeScript in the component.
* `<style scoped>` prevents style leakage to other components.
* Shorthands: `:` → `v-bind:`, `@` → `v-on:`. Prefer binding expressions for non-string values (e.g. `:disabled="true"`).

---

## Composition API Basics (Reactivity)

Key tools: **`ref()`**, **`reactive()`**, **`computed()`**.

* `ref(v)` → a reactive box with `.value = v`. In **templates**, refs are auto-unwrapped (no `.value`).
* `reactive(obj)` → a deeply reactive proxy of an object/array/Map/Set.
* `computed(fn)` → a cached ref that re-evaluates when dependencies change.

**Example – `ref`, `reactive`, `computed`**

```vue
<script setup lang="ts">
import { ref, reactive, computed } from 'vue'

const count = ref(0)

const state = reactive({
  name: 'Vue 3',
  colors: ['blue', 'green', 'purple']
})

const doubleCount = computed(() => count.value * 2)

function increment() {
  count.value++
}
</script>

<template>
  <div>
    <p>{{ state.name }} count is {{ count }}</p>
    <p>Double count is {{ doubleCount }}</p>
    <button @click="increment">Add 1</button>
  </div>
</template>
```

---

## Core Directives in Templates

* **`v-bind` (`:`)** – bind attributes/props
* **`v-on` (`@`)** – listen to events (use modifiers like `.prevent`, `.stop`, `.enter`)
* **`v-if` / `v-else-if` / `v-else`** – conditional render (adds/removes from DOM)
* **`v-show`** – toggle visibility via CSS (does not remove from DOM)
* **`v-for`** – list render (use stable `:key`)
* **`v-model`** – two-way bind form inputs

**Example – Toggle & list with form**

```vue
<script setup lang="ts">
import { ref } from 'vue'

const showList = ref(true)
const newItem = ref('')
const items = ref<string[]>(['First task', 'Another task'])

function addItem() {
  if (newItem.value.trim()) {
    items.value.push(newItem.value.trim())
    newItem.value = ''
  }
}
function removeItem(index: number) {
  items.value.splice(index, 1)
}
</script>

<template>
  <button @click="showList = !showList">
    {{ showList ? 'Hide' : 'Show' }} List
  </button>

  <div v-if="showList">
    <ul>
      <li v-for="(item, idx) in items" :key="item">
        {{ idx + 1 }}. {{ item }}
        <button @click="removeItem(idx)">Remove</button>
      </li>
    </ul>
  </div>
  <div v-else>
    <em>*(List is hidden)*</em>
  </div>

  <form @submit.prevent="addItem">
    <input v-model="newItem" placeholder="Enter new item" />
    <button type="submit">Add</button>
  </form>
</template>
```

**Notes**

* Use `v-if` when you **want to mount/unmount**; use `v-show` for **frequent toggles** without DOM teardown.
* Always provide a **stable `:key`** in `v-for` to aid efficient updates.

---

## Designing Component APIs: Props & Emits

* **Props**: data **into** the child; read-only inside the child.
* **Emits**: events **out** of the child; parent listens and updates its own state.

**TypeScript in `<script setup>`**

```vue
<script setup lang="ts">
interface CounterProps { initial: number }
const props = defineProps<CounterProps>()

interface CounterEmits { (e: 'increment', newValue: number): void }
const emit = defineEmits<CounterEmits>()
</script>
```

**Example – Prop down, Event up**

```vue
<!-- CounterButton.vue -->
<template>
  <button @click="$emit('increment')">
    Count is {{ count }}. Click to add 1.
  </button>
</template>
<script setup lang="ts">
const props = defineProps<{ count: number }>()
</script>
```

```vue
<!-- Parent usage -->
<CounterButton :count="currentCount" @increment="currentCount++" />
```

**Notes**

* Child should **not mutate** props; emit an event instead and let the parent update its state.
* With TS, `defineProps<{ ... }>()` and `defineEmits<{ ... }>()` give compile-time checks.

---

## Slots: Content Distribution

* **Default slot**: unnamed `<slot>` for arbitrary content.
* **Named slots**: `<slot name="...">`, filled with `<template #name>...</template>`.
* **Scoped slots**: child passes data to parent slot via attributes on `<slot>`; parent receives via destructuring.

**Default slot**

```vue
<!-- FancyButton.vue -->
<template>
  <button class="fancy-btn"><slot /></button>
</template>
```

```vue
<!-- Parent -->
<FancyButton>Click me!</FancyButton>
```

**Named slots**

```vue
<!-- BaseLayout.vue -->
<template>
  <div class="container">
    <header><slot name="header" /></header>
    <main><slot /></main>
    <footer><slot name="footer" /></footer>
  </div>
</template>
```

```vue
<!-- Parent -->
<BaseLayout>
  <template #header><h1>Page Title</h1></template>
  <p>Main content...</p>
  <template #footer><p>© 2025 MyCompany</p></template>
</BaseLayout>
```

**Scoped slot (slot props)**

```vue
<!-- ChildComponent.vue -->
<template>
  <div>
    <slot :user="currentUser" :logout="logoutFn" />
  </div>
</template>
```

```vue
<!-- Parent -->
<ChildComponent>
  <template #default="{ user, logout }">
    <p>Welcome, {{ user.name }}.</p>
    <button @click="logout">Logout</button>
  </template>
</ChildComponent>
```

---

## Full Example: Reusable `Card` & `TextInput`

### `Card.vue`

```vue
<!-- Card.vue -->
<script setup lang="ts">
import { computed } from 'vue'

interface CardProps {
  title: string
  variant?: 'flat' | 'elevated'
  as?: 'div' | 'section' | 'article'
}
interface CardEmits {
  (e: 'confirm'): void
  (e: 'close'): void
}
const props = defineProps<CardProps>()
const emit = defineEmits<CardEmits>()

const tag = computed(() => props.as || 'div')

function confirmAction() { emit('confirm') }
function closeAction() { emit('close') }
</script>

<template>
  <component :is="tag" class="card" :class="props.variant">
    <div class="card-header" v-if="$slots.header || props.title">
      <slot name="header">
        <h3>{{ props.title }}</h3>
      </slot>
      <button class="close-btn" @click="closeAction">×</button>
    </div>

    <div class="card-body">
      <slot />
    </div>

    <div class="card-footer">
      <slot name="footer" :confirm="confirmAction">
        <button class="confirm-btn" @click="confirmAction">OK</button>
      </slot>
    </div>
  </component>
</template>

<style scoped>
.card {
  border: 1px solid #ddd;
  padding: 1em;
  border-radius: 4px;
}
.card.elevated { box-shadow: 2px 2px 8px rgba(0,0,0,0.15); }
.card.flat { border: none; background: #f9f9f9; }
.card-header, .card-footer {
  display: flex; justify-content: space-between; align-items: center;
}
.card-header { border-bottom: 1px solid #eee; margin-bottom: 0.5em; padding-bottom: 0.5em; }
.card-footer { border-top: 1px solid #eee; margin-top: 0.5em; padding-top: 0.5em; }
.close-btn {
  background: transparent; border: none; font-size: 1.2em; line-height: 1; cursor: pointer;
}
.confirm-btn {
  background: #409eff; color: #fff; border: none; padding: 0.4em 0.8em; border-radius: 3px; cursor: pointer;
}
</style>
```

### `TextInput.vue`

```vue
<!-- TextInput.vue -->
<template>
  <input
    class="text-input"
    :value="modelValue"
    :placeholder="placeholder"
    @input="onInput"
  />
</template>

<script setup lang="ts">
const props = defineProps<{ modelValue: string; placeholder?: string }>()
const emit = defineEmits<{ (e: 'update:modelValue', value: string): void }>()

function onInput(e: Event) {
  emit('update:modelValue', (e.target as HTMLInputElement).value)
}
</script>

<style scoped>
.text-input {
  padding: 0.4em; border: 1px solid #ccc; border-radius: 3px;
}
.text-input:focus {
  outline: none; border-color: #409eff;
}
</style>
```

### `App.vue` (Parent Demo)

```vue
<!-- App.vue -->
<template>
  <!-- Card 1: Form card (can be hidden with close) -->
  <Card
    v-if="showFormCard"
    variant="flat"
    title="Add Item"
    @close="showFormCard = false"
    class="demo-card"
  >
    <form @submit.prevent="addItem">
      <TextInput v-model="newItem" placeholder="New item..." />
      <button type="submit">Add</button>
    </form>

    <p v-show="newItem">Preview: {{ newItem }}</p>

    <ul>
      <li v-for="(it, idx) in items" :key="it">
        {{ idx + 1 }}. {{ it }}
      </li>
    </ul>

    <template #footer="{ confirm }">
      <button @click="confirm()" :disabled="!newItem">Confirm Add</button>
    </template>
  </Card>

  <!-- Card 2: Confirmation card -->
  <Card
    v-if="!confirmed"
    variant="elevated"
    title="Please Confirm"
    @confirm="onConfirm"
    @close="onClose"
    class="demo-card"
  >
    <p>Do you agree to the terms and conditions?</p>
    <!-- Uses Card&apos;s default footer (OK button) -->
  </Card>

  <div v-else class="confirmation-message">
    ✅ Confirmation received!
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import Card from './Card.vue'
import TextInput from './TextInput.vue'

const showFormCard = ref(true)
const newItem = ref('')
const items = ref<string[]>([])

const confirmed = ref(false)

function addItem() {
  if (newItem.value.trim()) {
    items.value.push(newItem.value.trim())
    newItem.value = ''
  }
}
function onConfirm() { confirmed.value = true }
function onClose() { confirmed.value = true }
</script>

<style>
.demo-card { margin: 1em 0; max-width: 420px; }
.confirmation-message {
  padding: 1em; border: 2px solid green; color: green;
}
</style>
```

### What this demonstrates

* **Props**: `variant`, `title`, `as`, `placeholder`, `modelValue`
* **Emits**: `confirm`, `close`, `update:modelValue`
* **Slots**: default, named `header`/`footer`, and **scoped** footer (`{ confirm }`)
* **Directives**: `v-if`/`v-else`, `v-show`, `v-for` + `:key`, `v-model`, `@submit.prevent`, `@click`
* **Reactivity**: `ref` state updates re-render UI
* **SFC & Composition API**: `<script setup>` + TypeScript for clear, typed APIs

```
::contentReference[oaicite:0]{index=0}
```


---

**Back to [Week 2 Plan](../w2/)**
