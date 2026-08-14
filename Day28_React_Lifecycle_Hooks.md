# Day 28 - React Component Lifecycle & Hooks
*Wed, 5 Aug 2026*

## Component Lifecycle

Every React class component has lifecycle methods — these can be called to control the component's behavior at different stages. They're divided into **3 parts**:

1. **Mounting** — called when components are created
2. **Updating** — called when components are updated via state/props
3. **Unmounting** — called when components are being removed from the DOM (used for cleanup: closing DB/API connections, destroying objects)

### Mounting Methods (in order)

```
constructor
static getDerivedStateFromProps
render
componentDidMount
```

### Updating Methods (in order)

```
getDerivedStateFromProps
render()
shouldComponentUpdate()
getSnapshotBeforeUpdate
componentDidUpdate
```

### Unmounting Method

```
componentWillUnmount()
```

---
## Method Details

### `render()`
- Reads props and state, returns JSX
- The **only required** lifecycle method — always called; the others are optional and only run if defined

### `componentDidMount()`
- Called once all the component and its child components have rendered to the DOM
- The standard place to call an API and fetch data from a server

### `static getDerivedStateFromProps()`
- Called when state changes need to depend on props
- Runs on **every** render, whether triggered by:
  - New props from the parent
  - A state change within the component (via `setState()`)

### `shouldComponentUpdate()`
- Controls whether the component re-renders on an update
- Defaults to `true`
- Returning `false` **stops** the component from re-rendering for that update

### `getSnapshotBeforeUpdate(prevProps, prevState)`
- Called right before the DOM is updated (the point where the virtual DOM is about to sync with the real DOM)
- **Must** be used together with `componentDidUpdate()`
- Accepts the previous props and previous state, and returns a snapshot value

```jsx
getSnapshotBeforeUpdate(prevProps, prevState) {
    return snapshotValue;
}

componentDidUpdate(prevProps, prevState, snapshot) {
    console.log(snapshot);
}
```

### Lab Exercises
- **Lab 1:** Print the previous props and updated props using `getSnapshotBeforeUpdate`
- **Lab 2:** Take a text box, and on button click show an alert with `"hello" + (text box content)`

---
## React Hooks

Predefined functions that give class-component features (and alternate ways to use them) inside **functional** components.

### The 5 Core Hooks

1. **useState**
2. **useEffect**
3. **useContext**
4. **useRef**
5. **useReducer** — for managing complex state

### Why Hooks

- No need to deal with the `this` keyword in JS
- No need to bind event handlers like in class components
- Classes are complex to write, and make hot-reloading unreliable
- Class components have no clean, standard way to reuse or share logic between components

### Rules for Using Hooks

1. Must be used **inside functional components only**
2. Must be called at the **top level** (not nested inside logic)
3. **Cannot** be used inside loops or conditionals

---
## 1. `useState` Hook

Accepts a single initial value for a state variable, and returns **two** values:
1. The current state value
2. A function to update that state

```jsx
const [count, setCount] = useState(0);
```

- Makes event handling much simpler in functional components
- Lets you maintain state directly in a functional component

## 2. `useEffect` Hook

Used to perform **side effects**, such as:
- Updating the DOM
- Fetching data from a server/API

Accepts a function ("effect") that runs on mount, update, or unmount, depending on how it's called.

### Syntax

```jsx
useEffect(<function>, [dependencies]);
```

### Three Usage Patterns

| Syntax | Behavior |
|---|---|
| `useEffect(<function>)` | Runs on **every** render |
| `useEffect(<function>, [])` | Runs **only once**, like `componentDidMount` |
| `useEffect(<function>, [state, props])` | Runs whenever the listed state/props are updated |

```jsx
// Example: search product by name — re-fetch whenever "name" changes
useEffect(() => {
    axios.get(`/api/products?name=${name}`);
}, [name]);
```

> By default, `useEffect(<fn>, [])` runs once on mount and does NOT re-run for subsequent state updates — this is the equivalent of `componentDidMount` in a class component.

### Class Component vs Hooks — Lifecycle Equivalents

| Class Component Method | Functional Component (Hooks) Equivalent |
|---|---|
| `constructor` | `useState` initial value |
| `componentDidMount` | `useEffect(fn, [])` |
| `componentDidUpdate` | `useEffect(fn, [dependencies])` |
| `componentWillUnmount` | `useEffect(fn, [])` — return a cleanup function |
| `render` | The function component body itself |
