# Digital Menu App

A Vue 3 application built with Vite to manage a fictional snack bar menu.
The system allows adding itens, filtering by category, viewing a dynamic summary, and removing products.

---

## Getting Started

### Install dependencies

```bash
npm install
```

### Run in development

```bash
npm run dev
```

The app will be available at the address shown by Vite (usually http://localhost:5173).

---

### Build for production

```bash
npm run build
```

---

## Features

* Add menu itens with name, price, category, and availability
* Display itens as cards
* Visual highlight for unavailable itens
* Filter by category with active filter highlight
* Dynamic summary showing:

  * total itens
  * available itens
  * average price
* Remove itens from the menu

---

## Component Structure

* **App.vue**
  Main component responsible for managing state, calculations, and communication between components

* **MenuForm.vue**
  Form to add new itens

* **MenuFilters.vue**
  Category filter buttons

* **MenuItens.vue**
  Displays item cards and handles item removal

---

## Vue Concepts Used

### `ref`

Used in `src/App.vue` to store main application state:

* `itens`
* `filtroAtual`

---

### `computed`

Used in `src/App.vue` for derived data:

* `itensFiltrados` → filters itens based on selected category
* `totalDisponiveis` → counts available itens
* `precoMedioVisivel` → calculates average price of visible itens

---

### `onMounted`

Used in `src/App.vue` to load initial itens when the component is mounted.

---

### `reactive`

Used in `src/components/MenuForm.vue` to control form fields.

---

### `props`

Used to pass data from parent to child components:

* `MenuFilters.vue` receives categories and current filter
* `MenuItens.vue` receives itens

---

### `emit`

Used for child-to-parent communication:

* `MenuForm.vue` emits `add-item`
* `MenuFilters.vue` emits `change-filter`
* `MenuItens.vue` emits `remove-item`

---

### `v-model`

Used in `MenuForm.vue` to bind form fields to reactive state.

---

### `v-for`

Used to render lists:

* categories in `MenuFilters.vue`
* itens in `MenuItens.vue`

---

### `v-if` / `v-else`

Used in `MenuItens.vue` to display itens or an empty state message.

---

### Dynamic classes

Used to change styles based on state:

* active filter in `MenuFilters.vue`
* unavailable item in `MenuItens.vue`

---

## Notes

`App.vue` acts as the single source of truth, managing all data.
Child components receive data via props and communicate back using emit.
