---
title: "Week 4 - Reading Notes"
description: "Reading notes and key concepts for Week 4"
date: 2025-09-28T00:00:00+02:00
lastmod: 2025-09-28T00:00:00+02:00
draft: false
weight: 104
toc: true
seo:
  title: "Week 4 - Reading Notes"
  description: "Reading notes and key concepts for Week 4"
  canonical: ""
  noindex: false
---

# Vue.js: Template Syntax & Core Directives

**Duration:** September 28 – October 4, 2025
**Focus:** Vue template syntax and core directives
**Level:** Intermediate (Vue 3, `<script setup>`)

---

## Learning Objectives
By the end of this week, you will be able to:
- Master Vue template syntax and directives
- Implement data binding with `v-bind` and `v-model`
- Use `v-for` for list rendering with proper keys
- Handle events and conditional rendering

---

## Prerequisites & Setup
- Node.js 18+
- New project: `npm create vue@latest` → choose **TypeScript (optional)** and **Pinia (optional)**
- Run: `npm install && npm run dev`

---

## 1) Template Syntax

### Interpolation & Expressions
- Basic: `{{ username }}`
- Simple expressions only (no statements/assignments): `{{ fullName.toUpperCase() }}`
- One-way only—does **not** update the source.

```vue
<template>
  <h2>Welcome, {{ user.firstName }} {{ user.lastName }}</h2>
  <p>Uppercased: {{ user.firstName.toUpperCase() }}</p>
  <!-- Avoid heavy logic in templates; move to computed() -->
</template>
```

### Directive Overview
Common directives and shorthands:
- `v-bind:` → `:` attribute/class/style binding
- `v-on:` → `@` event binding
- `v-if` / `v-else-if` / `v-else` conditional blocks
- `v-show` CSS visibility toggle
- `v-for` list rendering (requires `:key`)
- `v-model` two-way binding (inputs/components)
- `v-text`, `v-html` (⚠ XSS risk with `v-html`)
- `v-once` render once; `v-memo` memoize subtrees (advanced)

### Template Refs & DOM Access
```vue
<script setup lang="ts">
import { ref, onMounted } from 'vue'
const inputEl = ref<HTMLInputElement | null>(null)

onMounted(() => {
  inputEl.value?.focus()
})
</script>

<template>
  <input ref="inputEl" placeholder="Autofocus via ref" />
</template>
```

### Computed in Templates
```vue
<script setup>
import { ref, computed } from 'vue'
const first = ref('Ada')
const last = ref('Lovelace')
const full = computed(() => `${first.value} ${last.value}`)
</script>

<template>
  <p>{{ full }}</p>
</template>
```

> **Best practice:** keep templates declarative; push derivations into `computed()`.

---

## 2) Data Binding

### Attribute, Class & Style Binding (`v-bind` / `:`)
```vue
<template>
  <!-- attribute binding -->
  <img :src="avatarUrl" :alt="username" />

  <!-- class binding -->
  <div :class="{ active: isActive, error: hasError }"></div>
  <div :class="['badge', variant]"></div>

  <!-- style binding -->
  <div :style="{ color: themeColor, fontSize: size + 'px' }"></div>
</template>
```

### Two-way Binding (`v-model`)
Modifiers: `.trim`, `.number`, `.lazy`
```vue
<template>
  <input v-model.trim="email" placeholder="email" />
  <input v-model.number="age" type="number" />
  <textarea v-model.lazy="bio" />
</template>
```

### Custom `v-model` on Components
Conventions in Vue 3: `modelValue` prop + `update:modelValue` emit.
(Or use `defineModel()` macro in `<script setup>`.)

```vue
<!-- Parent.vue -->
<script setup>
import TextField from './TextField.vue'
import { ref } from 'vue'
const title = ref('')
</script>
<template>
  <TextField v-model="title" label="Title" />
</template>
```

```vue
<!-- TextField.vue -->
<script setup>
const props = defineProps<{ label?: string, modelValue: string }>()
const emit = defineEmits<{ (e:'update:modelValue', v:string): void }>()
</script>
<template>
  <label>
    {{ label }}
    <input :value="props.modelValue" @input="e => emit('update:modelValue', (e.target as HTMLInputElement).value)"/>
  </label>
</template>
```

**Multiple models**: `v-model:title`, `v-model:checked` → props `title`, `checked`; emits `update:title`, `update:checked`.

### Event Handling (`@` shorthand)
- Modifiers: `.stop`, `.prevent`, `.self`, `.capture`, `.once`, `.passive`
```vue
<button @click.prevent="submit()">Save</button>
<form @submit.prevent="submit">
  <input @keyup.enter="submit" />
</form>
```

---

## 3) Conditional Rendering

### `v-if` / `v-else-if` / `v-else`
```vue
<template>
  <p v-if="status === 'loading'">Loading…</p>
  <p v-else-if="status === 'error'">Something went wrong</p>
  <p v-else>Done!</p>
</template>
```

### `v-show` vs `v-if`
- `v-if`: conditional mount/unmount (higher cost, no DOM when false)
- `v-show`: toggles `display: none` (lower cost to toggle, initial render cost)

### Template Fragments & Groups
Group multiple nodes under a condition using `<template>`:
```vue
<template>
  <template v-if="loggedIn">
    <nav>…</nav>
    <aside>…</aside>
  </template>
</template>
```

### Keys for Efficient Updates
- Use stable, unique keys (e.g., `id`) to preserve component state.
- To force re-render, change `:key` deliberately.

---

## 4) List Rendering

### Arrays & Objects
```vue
<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }} — {{ todo.done ? '✓' : '✗' }}
    </li>
  </ul>

  <div v-for="(val, key, idx) in stats" :key="key">{{ idx }}. {{ key }}: {{ val }}</div>
</template>
```

### Updates & Reactivity
- Mutations like `push`, `splice` are reactive in Vue 3.
- Avoid using array index as `:key`.
- When replacing arrays, assign a **new** array (e.g., from a computed filter) to trigger updates.

### Filtering & Sorting (use `computed`)
```vue
<script setup>
import { ref, computed } from 'vue'
const q = ref('')
const sortBy = ref<'name' | 'score'>('name')
const students = ref([
  { id: 1, name: 'Ava', score: 91 },
  { id: 2, name: 'Ben', score: 76 },
  { id: 3, name: 'Cy',  score: 88 },
])

const visible = computed(() => {
  const base = students.value.filter(s => s.name.toLowerCase().includes(q.value.toLowerCase()))
  return [...base].sort((a,b) => sortBy.value === 'name' ? a.name.localeCompare(b.name) : b.score - a.score)
})
</script>

<template>
  <input v-model="q" placeholder="Search" />
  <select v-model="sortBy">
    <option value="name">Name</option>
    <option value="score">Score</option>
  </select>
  <ul>
    <li v-for="s in visible" :key="s.id">{{ s.name }} — {{ s.score }}</li>
  </ul>
</template>
```

---

## Live Demo Component (Brings it Together)
```vue
<!-- Demo.vue -->
<script setup>
import { ref, computed } from 'vue'
const title = ref('Tasks')
const newTodo = ref('')
const showDone = ref(true)
const todos = ref([
  { id: 1, text: 'Install Vue', done: true },
  { id: 2, text: 'Build demo', done: false },
])
const remaining = computed(() => todos.value.filter(t => !t.done).length)

function add() {
  const text = newTodo.value.trim()
  if (!text) return
  todos.value.push({ id: Date.now(), text, done: false })
  newTodo.value = ''
}
</script>

<template>
  <h2>{{ title }} ({{ remaining }} remaining)</h2>
  <input v-model.trim="newTodo" @keyup.enter="add" placeholder="New task" />
  <button @click="add">Add</button>

  <label><input type="checkbox" v-model="showDone" /> Show completed</label>

  <ul>
    <li v-for="t in todos" :key="t.id" v-show="showDone || !t.done">
      <input type="checkbox" v-model="t.done" />
      <span :class="{ 'line-through': t.done }">{{ t.text }}</span>
    </li>
  </ul>
</template>

<style scoped>
.line-through { text-decoration: line-through; }
</style>
```

---

## Lab Activity (90–120 min)
**Lab: Smart Roster with Filters**
1. Fetch or seed a `students` array `{ id, name, major, gpa, year }`.
2. Build controls: search by name, filter by `major`, min GPA slider, sort by `name`/`gpa`.
3. Render with `v-for`, use stable `:key`.
4. Show stats via `computed`: total, visible, average GPA of visible.
5. Use `v-show` to toggle expanded details per row.
6. Bonus: extract `<RosterRow>` child with a custom `v-model:expanded`.

**Deliverables**: working UI + README with design choices.

---

## Homework (Due Oct 4, 23:59 Asia/Baghdad)
1. **Custom `TagInput` Component**
   - API: `v-model` of `string[]`, emits `add`, `remove`.
   - Features: add on Enter, backspace to remove last, prevent duplicates.
   - Tests: show example usage in a parent component.
2. **List Tools**
   - Given a products array, implement `computed` filters (query, category, price range) and sorting.

---

## Quiz (Short Check)
1. Difference between `v-if` and `v-show`? When choose each?
2. Why must `v-for` have a `:key` and what makes a good key?
3. What do `.lazy`, `.trim`, `.number` do on `v-model`?
4. Show how to define a component that supports `v-model` (prop + emit names).
5. Why avoid complex expressions directly in templates?
6. What happens if you use array index as key and reorder items?

---

## Rubric (Labs & Homework)
- **Correctness (40%)**: directives used appropriately; state updates reactive
- **Code Quality (30%)**: computed for derived state; small, focused components
- **UX (20%)**: accessibility (labels), keyboard flows, clear feedback
- **Docs (10%)**: concise README, assumptions, screenshots/gifs

---

## Pitfalls & Best Practices
- Do **not** put `v-if` and `v-for` on the same element; wrap with `<template>` or compute filtered list.
- Prefer `computed` over inline heavy logic.
- Avoid index keys; use stable identifiers.
- Be cautious with `v-html` (sanitize or avoid).
- Keep components stateless where possible; lift state to parent for shared data.

---

## Cheat Sheet (Quick Reference)
- `{{ expr }}` — interpolate expression
- `:attr="expr"` — bind attribute
  `:class="{ on: flag }"`, `:class="['a', cls]`
  `:style="{ color, fontSize: size+'px' }"`
- `@event="handler"` — bind event
  Modifiers: `.stop` `.prevent` `.self` `.capture` `.once` `.passive`
- `v-model="state"` — two-way input binding
  Modifiers: `.trim` `.number` `.lazy`
  Components: prop `modelValue`, emit `update:modelValue`
- `v-if / v-else-if / v-else` — mount/unmount
  `v-show` — toggle visibility (CSS)
- `v-for="(item, i) in list" :key="item.id"` — render lists
- `<template>` — group without extra DOM
- Re-render trick: change `:key`

---

## Extension (Optional)
- Explore `<KeepAlive>` with dynamic components to preserve state across toggles.
- Try the `defineModel()` macro to simplify custom v-models in `<script setup>`.
- Move list data to Pinia store and persist to `localStorage`.

---

## Submission
- Push code to a repo (GitHub/GitLab) and include a README with instructions.
- Submit the repo URL + a 30–60s screen recording (gif/video) demonstrating core features.

