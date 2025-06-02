# 🧠 React Hooks Guide (Beginner to Intermediate)

---

## 📋 Cheat Sheet Summary

| Hook                  | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| `useState`            | Add local state to function components              |
| `useEffect`           | Run side effects like API calls                     |
| `useContext`          | Access data from React Context                      |
| `useRef`              | Store mutable value without causing re-renders      |
| `useMemo`             | Optimize performance by memoizing values            |
| `useCallback`         | Memoize functions to avoid unnecessary re-creations |
| `useReducer`          | Manage complex state logic                          |
| `useLayoutEffect`     | Like `useEffect`, but fires before paint            |
| `useImperativeHandle` | Customize what refs expose                          |
| `useDebugValue`       | Label custom hooks in React DevTools                |

---

## 1. `useState`

**What it does:** Adds state to functional components.

**Syntax:**

```js
const [count, setCount] = useState(initialValue);
```

**Example:**

```jsx
const Counter = () => {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>Clicked {count} times</button>;
};
```

**Gotchas:**

* State updates are asynchronous.
* Don’t update state directly.

**When to use:**

* For simple, local UI state.

---

## 2. `useEffect`

**What it does:** Performs side effects (e.g., fetching data, setting timers).

**Syntax:**

```js
useEffect(() => {
  // effect
  return () => {
    // cleanup (optional)
  };
}, [dependencies]);
```

**Example:**

```jsx
useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]);
```

**Gotchas:**

* Forgetting cleanup functions (especially with subscriptions).
* Missing or incorrect dependencies.

**When to use:**

* Whenever you need to sync with external systems.

---

## 3. `useContext`

**What it does:** Accesses the current value from a React Context.

**Syntax:**

```js
const value = useContext(MyContext);
```

**Example:**

```jsx
const Theme = () => {
  const theme = useContext(ThemeContext);
  return <div style={{ background: theme.background }}>Hello</div>;
};
```

**Gotchas:**

* Requires a `<Context.Provider>` above in the tree.

**When to use:**

* To avoid prop drilling and share global data.

---

## 4. `useRef`

**What it does:** Stores a mutable value that persists across renders.

**Syntax:**

```js
const myRef = useRef(initialValue);
```

**Example:**

```jsx
const inputRef = useRef();

useEffect(() => {
  inputRef.current.focus();
}, []);

return <input ref={inputRef} />;
```

**Gotchas:**

* Changing `.current` doesn’t cause re-renders.

**When to use:**

* For DOM manipulation or timer IDs.

---

## 5. `useMemo`

**What it does:** Memoizes the result of a calculation to avoid recomputation.

**Syntax:**

```js
const memoizedValue = useMemo(() => computeValue(a, b), [a, b]);
```

**Example:**

```jsx
const filteredList = useMemo(() => list.filter(item => item.active), [list]);
```

**Gotchas:**

* Overusing it can hurt readability and performance.

**When to use:**

* For expensive calculations or derived data.

---

## 6. `useCallback`

**What it does:** Memoizes a function reference.

**Syntax:**

```js
const memoizedCallback = useCallback(() => { doSomething(); }, [dependencies]);
```

**Example:**

```jsx
const handleClick = useCallback(() => {
  console.log('Clicked');
}, []);
```

**Gotchas:**

* Don't use without dependencies; can cause stale closures.

**When to use:**

* When passing callbacks to optimized child components.

---

## 7. `useReducer`

**What it does:** Alternative to `useState` for complex state logic.

**Syntax:**

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

**Example:**

```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'increment': return { count: state.count + 1 };
    default: return state;
  }
}

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

**Gotchas:**

* Use when state logic involves multiple sub-values.

**When to use:**

* For complex state or shared logic between components.

---

## 8. `useLayoutEffect`

**What it does:** Like `useEffect`, but runs synchronously **after DOM mutations but before paint**.

**Syntax:**

```js
useLayoutEffect(() => {
  // do something synchronously
}, [dependencies]);
```

**When to use:**

* For reading layout and measuring DOM elements before the browser paints.

**Gotchas:**

* Can block painting if overused.

---

## 9. `useImperativeHandle`

**What it does:** Customizes the value exposed by `ref` in parent components.

**Syntax:**

```js
useImperativeHandle(ref, () => ({ customMethod }));
```

**Example:**

```jsx
forwardRef((props, ref) => {
  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus()
  }));

  return <input ref={inputRef} />;
});
```

**When to use:**

* With `forwardRef` to expose custom methods.

---

## 10. `useDebugValue`

**What it does:** Displays a label for custom hooks in React DevTools.

**Syntax:**

```js
useDebugValue(value);
```

**When to use:**

* Inside custom hooks, mainly for debugging.

---

## 🛠 Custom Hook Example

```js
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const saved = localStorage.getItem(key);
    return saved ? JSON.parse(saved) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}
```

---

## 🌐 React Router Hooks

### `useNavigate`

* For programmatic navigation

```js
const navigate = useNavigate();
navigate('/profile');
```

### `useParams`

* Get route parameters (e.g. `/user/:id`)

```js
const { id } = useParams();
```

### `useLocation`

* Get the current location object

```js
const location = useLocation();
console.log(location.pathname);
```

---

## ✅ Best Practices

* Keep hook calls at the **top level** of your component.
* Always define the **correct dependency array**.
* Extract logic into **custom hooks** for reuse.
* Don’t over-optimize with `useMemo` and `useCallback`.
* Use `useReducer` for **complex state management**.
* Use `React DevTools` to inspect hooks and context.

---

Save this file in `.md` or export as `.docx` for structured notes.
